---
title: Azure Kubernetes Service (AKS) プライベート クラスターへの BDC のデプロイ
titleSuffix: SQL Server Big Data Cluster
description: 高度なネットワーク (CNI) を備えた Azure Kubernetes Service (AKS) プライベート クラスターに SQL Server ビッグ データ クラスターをデプロイする方法について説明します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4a55d7f6c9c55891f8d1a7bf97d8834c9df4a796
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283121"
---
# <a name="deploy-bdc-in-azure-kubernetes-service-aks-private-cluster"></a>Azure Kubernetes Service (AKS) プライベート クラスターへの BDC のデプロイ

この記事では、Azure Kubernetes Service (AKS) プライベート クラスターに SQL Server ビッグ データ クラスターをデプロイする方法について説明します。 この構成では、エンタープライズ ネットワーク環境でのパブリック IP アドレスの使用が制限付きでサポートされます。

プライベート デプロイには次のような利点があります。

* パブリック IP アドレスを制限付きで使用できる
* アプリケーション サーバーとクラスターのノード プールの間のネットワーク トラフィックがプライベート ネットワークにのみ保持される
* 必須のエグレス トラフィックの構成を特定の要件に合わせてカスタマイズできる

この記事では、AKS プライベート クラスターを使用して、それぞれのセキュリティ文字列が適用されている間に パブリック IP アドレスの使用を制限する方法について説明します。

## <a name="deploy-private-bdc-cluster-with-aks-private-cluster"></a>AKS プライベート クラスターに BDC クラスターをデプロイする

最初に、[AKS プライベート クラスター](/azure/aks/private-clusters)を作成して、API サーバーとノード プールの間のネットワーク トラフィックがプライベート ネットワークにのみ保持されるようにします。 コントロール プレーンまたは API サーバーは、AKS プライベート クラスターで内部 IP アドレスを持ちます。

このセクションでは、高度なネットワーク (CNI) を備えた Azure Kubernetes Service (AKS) プライベート クラスターに BDC クラスターをデプロイする方法について説明します。

## <a name="create-a-private-aks-cluster-with-advanced-networking"></a>高度なネットワークが有効になっているプライベート AKS クラスターを作成する

```console

export REGION_NAME=<your Azure region >
export RESOURCE_GROUP=< your resource group name >
export SUBNET_NAME=aks-subnet
export VNET_NAME=bdc-vnet
export AKS_NAME=< your aks private cluster name >
 
az group create -n $RESOURCE_GROUP -l $REGION_NAME
 
az network vnet create \
    --resource-group $RESOURCE_GROUP \
    --location $REGION_NAME \
    --name $VNET_NAME \
    --address-prefixes 10.0.0.0/8 \
    --subnet-name $SUBNET_NAME \
    --subnet-prefix 10.1.0.0/16
 

SUBNET_ID=$(az network vnet subnet show \
    --resource-group $RESOURCE_GROUP \
    --vnet-name $VNET_NAME \
    --name $SUBNET_NAME \
    --query id -o tsv)
 
echo $SUBNET_ID
## will be displayed something similar as the following: 
/subscriptions/xxxx-xxxx-xxx-xxxx-xxxxxxxx/resourceGroups/your-bdc-rg/providers/Microsoft.Network/virtualNetworks/your-aks-vnet/subnets/your-aks-subnet
```

### <a name="create-aks-private-cluster-with-advanced-networking-cni"></a>高度なネットワーク (CNI) を備えた AKS プライベート クラスターを作成する

次の手順に進むには、Standard Load Balancer を使用して AKS クラスターをプロビジョニングし、プライベート クラスター機能を有効にする必要があります。 コマンドは次のようになります。 

```console
az aks create \
    --resource-group $RESOURCE_GROUP \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.2.0.10 \
    --service-cidr 10.2.0.0/24 \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

デプロイが正常に完了したら、`<MC_yourakscluster>` リソース グループにアクセスして、`kube-apiserver` がプライベート エンドポイントであることを確認します。 たとえば、次のセクションを参照してください。

## <a name="connect-to-an-aks-cluster"></a>AKS クラスターに接続する

```console
az aks get-credentials -n $AKS_NAME -g $RESOURCE_GROUP
```

## <a name="build-big-data-cluster-bdc-deployment-profile"></a>ビッグ データ クラスター (BDC) のデプロイ プロファイルを作成する

AKS クラスターに接続したら、BDC のデプロイを開始できます。環境変数を準備して、デプロイを開始します。 

```console
azdata bdc config init --source aks-dev-test --target private-bdc-aks --force
```

BDC カスタム デプロイ プロファイルを生成および構成する:

```console
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.docker.imageTag=2019-CU6-ubuntu-16.04"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.storage.data.className=default"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.storage.logs.className=default"

azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/control.json -j "$.spec.endpoints[1].serviceType=NodePort"

azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -c private-bdc-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].serviceType=NodePort"
```

## <a name="deploy-private-sql-server-big-data-cluster-with-ha"></a>HA を使用してプライベート SQL Server ビッグ データ クラスターを展開する

[高可用性 (HA) を使用して SQL Server ビッグ データ クラスター (SQL-BDC) を展開する](deployment-high-availability.md)場合は、`aks-dev-test-ha` デプロイ プロファイルを使用します。 デプロイが正常に完了した後は、同じ `kubectl get svc` コマンドを使用して追加の `master-secondary-svc` サービスが作成されていることを確認できます。 `ServiceType` を `NodePort` として構成する必要があります。 他の手順は、前のセクションで説明したものと同様です。

次の例では、`ServiceType` を `NodePort` として設定しています。

```console
azdata bdc config replace -c private-bdc-aks /bdc.json -j "$.spec.resources.master.spec.endpoints[1].serviceType=NodePort"
```

## <a name="deploy-bdc-in-aks-private-cluster"></a>AKS プライベート クラスターに BDC をデプロイする

```console
export AZDATA_USERNAME=<your bdcadmin username>
export AZDATA_PASSWORD=< your bdcadmin password>

azdata bdc create --config-profile private-bdc-aks --accept-eula yes
```

## <a name="check-deployment-status"></a>展開の状態を確認する

デプロイには数分かかります。デプロイの状態は、次のコマンドを使って確認できます。 

```console
kubectl get pods -n mssql-cluster -w
```

## <a name="check-the-service-status"></a>サービスの状態を確認する

次のコマンドを使用してサービスを確認します。 外部 IP を使用せずにすべてが正常であることを確認します。

```console
kubectl get services -n mssql-cluster
```

[AKS プライベート クラスターの BDC を管理する](private-manage.md)方法を確認してから、[BDC クラスターに接続する](connect-to-big-data-cluster.md)次のステップに進みます。

[GitHub の SQL Server Samples リポジトリ](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/private-aks)にある、このシナリオ用の自動化スクリプトを確認してください。

## <a name="next-steps"></a>次のステップ

[プライベート クラスターを管理する](private-manage.md)

[プライベート BDC クラスターのエグレス トラフィックを制限する](private-restrict-egress-traffic.md)

[Azure Data Studio を使用して SQL Server ビッグ データ クラスターに接続する](connect-to-big-data-cluster.md)
