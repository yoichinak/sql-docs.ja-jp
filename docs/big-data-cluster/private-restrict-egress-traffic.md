---
title: Azure Kubernetes Service (AKS) プライベート クラスターでビッグ データ クラスター (BDC) クラスターのエグレス トラフィックを制限する
titleSuffix: SQL Server Big Data Clusters
description: Azure Kubernetes Service (AKS) プライベート クラスターでビッグ データ クラスター (BDC) クラスターのエグレス トラフィックを制限する方法について説明します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 962e155b3b0b5906d36fa4d884be2af353cb25a9
ms.sourcegitcommit: 1126792200d3b26ad4c29be1f561cf36f2e82e13
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2020
ms.locfileid: "90076607"
---
# <a name="restrict-egress-traffic-of-big-data-clusters-bdc-clusters-in-azure-kubernetes-service-aks-private-cluster"></a>Azure Kubernetes Service (AKS) プライベート クラスターでビッグ データ クラスター (BDC) クラスターのエグレス トラフィックを制限する

AKS でプロビジョニングされる Standard SKU ロード バランサーは、既定でエグレス用に設定および使用されます。 ただし、パブリック IP が許可されていない場合、またはエグレスに追加のホップが必要な場合、既定の設定ではすべてのシナリオの要件を満たせない可能性があります。 クラスターでパブリック IP が許可されず、クラスターがネットワーク仮想アプライアンス (NVA) の内側に置かれている場合は、ユーザー定義のルート テーブルを定義します。

AKS クラスターでは既定で、管理と運用のために、制限なしのアウトバウンド (エグレス) インターネット アクセスが可能です。 AKS クラスター内のワーカー ノードは、次の例のように、特定のポートと完全修飾ドメイン名 (FQDN) にアクセスする必要があります。

* ワーカー ノードの OS セキュリティ更新プログラム。クラスターでは、Microsoft Container Registry (MCR) から基本システムのコンテナー イメージをプルする必要があります
* GPU 対応の AKS ワーカー ノードでは、ドライバーをインストールするために Nvidia のいくつかのエンドポイントにアクセスする必要があります
* (エンタープライズ レベルのコンプライアンスを実現するための) Azure Policy や、Azure Monitoring (と Container Insights の組み合わせ) などの Azure サービスと組み合わせて AKS を使用するシナリオ 
* Dev Space 対応のシナリオや、性質の似たその他のシナリオ

> [!NOTE]
> 現時点では、Azure Kubernetes Service (AKS) プライベート クラスターに BDC をデプロイするとき、この記事で言及したもの以外のシナリオでは、インバウンド依存関係はありません。すべてのアウトバウンド依存関係は、「[Azure Kubernetes Service (AKS) でクラスター ノードに対するエグレス トラフィックを制御する](/azure/aks/limit-egress-traffic)」で確認できます。

この記事では、高度なネットワークと UDR (ユーザー定義ルート) を使用して AKS プライベート クラスターに BDC をデプロイする方法、および、エンタープライズ レベルのネットワーク環境とのさらなる統合について説明します。

## <a name="use-azure-firewall-to-restrict-egress-traffic"></a>Azure ファイアウォールを使用してエグレス トラフィックを制限する

Azure Firewall では、この構成を簡略化するための Azure Kubernetes Service `(AzureKubernetesService)` FQDN タグが提供されています。

このタグの完全な情報については、「[Azure Firewall を使用してエグレス トラフィックを制限する](/azure/aks/limit-egress-traffic#restrict-egress-traffic-using-azure-firewall)」を参照してください。

次の図は、AKS プライベート クラスターでトラフィックがどのように制限されるかを示しています。 

:::image type="content" source="media/private-cluster-restrict-egress-traffic/aks-azure-firewall-egress.png" alt-text="AKS プライベート クラスターのファイアウォールとエグレス トラフィック":::

Azure Firewall を使用して基本的なアーキテクチャを設定するには、次のようにします。

1. リソース グループと VNet を作成する
2. Azure ファイアウォールを作成および設定する
3. ユーザー定義ルート テーブルを作成する
4. ファイアウォール規則の設定
5. サービス プリンシパル (SP) を作成する
6. AKS プライベート クラスターを作成する
7. BDC デプロイ プロファイルを作成する
8. BDC をデプロイする

以下の手順で詳細を示します。

## <a name="create-the-resource-group-and-vnet"></a>リソース グループと VNet を作成する

1. リソースを作成するための一連の環境変数を定義します。

   ```console
   export REGION_NAME=<region>
   export RESOURCE_GROUP=private-bdc-aksudr-rg
   export SUBNET_NAME=aks-subnet
   export VNET_NAME=bdc-vnet
   export AKS_NAME=bdcaksprivatecluster
   ```

1. リソース グループの作成

   ```azurecli
   az group create -n $RESOURCE_GROUP -l $REGION_NAME
   ```

1. VNet を作成します

   ```azurecli
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
   ```

## <a name="create-and-set-up-azure-firewall"></a>Azure Firewall を作成および設定する

1. リソースを作成するための一連の環境変数を定義します。

   ```console
   export FWNAME=bdcaksazfw
   export FWPUBIP=$FWNAME-ip
   export FWIPCONFIG_NAME=$FWNAME-config

   az extension add --name azure-firewall
   ```

1. ファイアウォール専用のサブネットを作成します

   > [!NOTE]
   > 作成後にファイアウォール名を変更することはできません

   ```azurecli
   az network vnet subnet create \
     --resource-group $RESOURCE_GROUP \
     --vnet-name $VNET_NAME \
     --name AzureFirewallSubnet \
     --address-prefix 10.3.0.0/24

    az network firewall create -g $RESOURCE_GROUP -n $FWNAME -l $REGION_NAME --enable-dns-proxy true

    az network public-ip create -g $RESOURCE_GROUP -n $FWPUBIP -l $REGION_NAME --sku "Standard"

    az network firewall ip-config create -g $RESOURCE_GROUP -f $FWNAME -n $FWIPCONFIG_NAME --public-ip-address $FWPUBIP --vnet-name $VNET_NAME
   ```

既定では、Azure によって、Azure のサブネット、仮想ネットワーク、およびオンプレミスのネットワーク間のトラフィックが自動的にルーティングされます。 

## <a name="create-user-defined-route-table"></a>ユーザー定義ルート テーブルを作成する

Azure Firewall へのホップを含むユーザー定義ルート (UDR) テーブルを作成します。

```azurecli

export SUBID= <your Azure subscription ID>
export FWROUTE_TABLE_NAME=bdcaks-rt
export FWROUTE_NAME=bdcaksroute
export FWROUTE_NAME_INTERNET=bdcaksrouteinet

export FWPUBLIC_IP=$(az network public-ip show -g $RESOURCE_GROUP -n $FWPUBIP --query "ipAddress" -o tsv)
export FWPRIVATE_IP=$(az network firewall show -g $RESOURCE_GROUP -n $FWNAME --query "ipConfigurations[0].privateIpAddress" -o tsv)

# Create UDR and add a route for Azure Firewall

az network route-table create -g $RESOURCE_GROUP --name $FWROUTE_TABLE_NAME

az network route-table route create -g $RESOURCE_GROUP --name $FWROUTE_NAME --route-table-name $FWROUTE_TABLE_NAME --address-prefix 0.0.0.0/0 --next-hop-type VirtualAppliance --next-hop-ip-address $FWPRIVATE_IP --subscription $SUBID

az network route-table route create -g $RESOURCE_GROUP --name $FWROUTE_NAME_INTERNET --route-table-name $FWROUTE_TABLE_NAME --address-prefix $FWPUBLIC_IP/32 --next-hop-type Internet
```

## <a name="set-up-firewall-rules"></a>ファイアウォール規則の設定 

```azurecli
# Add FW Network Rules

az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'apiudp' --protocols 'UDP' --source-addresses '*' --destination-addresses "AzureCloud.$REGION_NAME" --destination-ports 1194 --action allow --priority 100
az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'apitcp' --protocols 'TCP' --source-addresses '*' --destination-addresses "AzureCloud.$REGION_NAME" --destination-ports 9000
az network firewall network-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwnr' -n 'time' --protocols 'UDP' --source-addresses '*' --destination-fqdns 'ntp.ubuntu.com' --destination-ports 123

# Add FW Application Rules

az network firewall application-rule create -g $RESOURCE_GROUP -f $FWNAME --collection-name 'aksfwar' -n 'fqdn' --source-addresses '*' --protocols 'http=80' 'https=443' --fqdn-tags "AzureKubernetesService" --action allow --priority 100
```

次のコマンドを使用して、以前に BDC をデプロイした AKS クラスターにユーザー定義ルート テーブル (UDR) を関連付けることができます。

```azurecli
az network vnet subnet update -g $RESOURCE_GROUP --vnet-name $VNET_NAME --name $SUBNET_NAME --route-table $FWROUTE_TABLE_NAME
```

## <a name="create--configure-service-principal-sp"></a>サービス プリンシパル (SP) を作成および構成する

この手順では、サービス プリンシパルを作成し、仮想ネットワークにアクセス許可を割り当てる必要があります。

次の例を参照してください。 

```azurecli
# Create SP and Assign Permission to Virtual Network

az ad sp create-for-rbac -n "bdcaks-sp" --skip-assignment

APPID=<your service principal ID >
PASSWORD=< your service principal password >
VNETID=$(az network vnet show -g $RESOURCE_GROUP --name $VNET_NAME --query id -o tsv)

# Assign SP Permission to VNET

az role assignment create --assignee $APPID --scope $VNETID --role "Network Contributor"


RTID=$(az network route-table show -g $RESOURCE_GROUP -n $FWROUTE_TABLE_NAME --query id -o tsv)
az role assignment create --assignee $APPID --scope $RTID --role "Network Contributor"
```

## <a name="create-aks-cluster"></a>AKS クラスターの作成

次に、アウトバウンドの種類として `userDefinedRouting` を使用して AKS クラスターを作成します。

```azurecli
az aks create \
    --resource-group $RESOURCE_GROUP \
    --location $REGION_NAME \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --outbound-type userDefinedRouting \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.2.0.10 \
    --service-cidr 10.2.0.0/24 \
    --service-principal $APPID \
    --client-secret $PASSWORD \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

## <a name="build-big-data-cluster-bdc-deployment-profile"></a>ビッグ データ クラスター (BDC) のデプロイ プロファイルを作成する

カスタム プロファイルを使用して BDC クラスターを作成できます。 

```console
azdata bdc config init --source aks-dev-test --target private-bdc-aks --force
```

## <a name="generate-and-config-bdc-custom-deployment-profile"></a>BDC カスタム デプロイ プロファイルを生成および構成する: 
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

## <a name="deploy-bdc-in-aks-private-cluster"></a>AKS プライベート クラスターに BDC をデプロイする

```console
export AZDATA_USERNAME=<your bdcadmin username>
export AZDATA_PASSWORD=< your bdcadmin password>

azdata bdc create --config-profile private-bdc-aks --accept-eula yes
```

## <a name="use-third-party-firewall-instead-of-azure-firewall"></a>Azure Firewall の代わりにサード パーティのファイアウォールを使用する

AKS プライベート クラスターに BDC をデプロイする場合にエグレス トラフィックを制限するには、サード パーティのファイアウォールを使用します。 たとえば、[Azure Marketplace で "firewall" を検索](https://azuremarketplace.microsoft.com/marketplace/apps?search=firewall&page=1)してみてください。 サード パーティのファイアウォールは、より準拠した構成のプライベート デプロイ ソリューションで使用できます。 ファイアウォールでは、次のネットワーク規則を提供する必要があります。

* [AKS クラスターに必要なアウトバウンド ネットワーク規則および FQDN](/azure/aks/limit-egress-traffic#required-outbound-network-rules-and-fqdns-for-aks-clusters) のすべてと、ワイルドカードの HTTP/HTTPS エンドポイントおよび依存関係のすべて。修飾子の数と実際の要件に応じて、対象の AKS クラスターで変動する可能性があります。
* [ここ](/azure/aks/limit-egress-traffic#azure-global-required-network-rules)に記載されている、Azure Global に必要なネットワーク規則/FQDN/アプリケーション規則。
* [ここ](/azure/aks/limit-egress-traffic#optional-recommended-fqdn--application-rules-for-aks-clusters)に記載されている、AKS クラスターに対して推奨される省略可能な FQDN とアプリケーションの規則。 

[AKS プライベート クラスターで BDC を管理する](private-manage.md)方法を確認してから、[BDC クラスターに接続する](connect-to-big-data-cluster.md)次のステップに進んでください。

[GitHub の SQL Server Samples リポジトリ](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/private-aks)にある、このシナリオ用の自動化スクリプトを確認してください。

## <a name="next-steps"></a>次のステップ

[AKS プライベート クラスターでビッグ データ クラスターを管理する](private-manage.md)

[Azure Data Studio を使用して SQL Server ビッグ データ クラスターに接続する](connect-to-big-data-cluster.md)
