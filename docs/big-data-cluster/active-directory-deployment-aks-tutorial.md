---
title: Active Directory で Azure Kubernetes Services (AKS) に展開する - チュートリアル
titleSuffix: SQL Server Big Data Cluster
description: Azure Kubernetes Services (AKS) に AD モードで SQL Server ビッグ データ クラスターを展開する方法について説明します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 11/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b24a83e1647b0e32aff3ce19ad69a0fdc9405b0e
ms.sourcegitcommit: 0f484f32709a414f05562bbaafeca9a9fc57c9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632955"
---
# <a name="tutorial-deploy-sql-server-big-data-clusters-in-ad-mode-on-azure-kubernetes-services-aks"></a>チュートリアル:Azure Kubernetes Services (AKS) に AD モードで SQL Server ビッグ データ クラスターを展開する

この記事では、参照アーキテクチャを使用して、SQL Server ビッグ データ クラスター (BDC) を Active Directory 認証モードで展開する方法について説明します。 参照アーキテクチャを使用すれば、オンプレミスの Active Directory ドメインサービス (AD DS) を Azure に拡張することができます。 [Azure アーキテクチャ センター](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-extend-domain)から [Azure の構成要素](https://github.com/mspnp/template-building-blocks/wiki/Install-Azure-Building-Blocks)と一緒に展開できます。

## <a name="prerequisites"></a>前提条件

SQL Server ビッグ データ クラスターを展開する前に、次のことを行う必要があります。

* 管理用の Azure VM にアクセスします。 この VM には、BDC を展開する Azure Virtual Network (VNet) へのアクセス権が必要です。 同じ VNet 上に、または [ピアリングされた VNet](/azure/virtual-network/virtual-network-manage-peering) 上に存在する必要があります。
* 管理 VM 上に[ビッグ データ ツールをインストール](deploy-big-data-tools.md)します。
* オンプレミスの AD コントローラーに [Active Directory 認証モード](active-directory-prerequisites.md)でクラスターを展開する準備をします。

## <a name="create-aks-subnet"></a>AKS サブネットを作成する

1. 環境変数の設定

   ```console
   export REGION_NAME=< your Azure Region >
   export RESOURCE_GROUP=<your resource group >
   export SUBNET_NAME=aks-subnet
   export VNet_NAME= adds-vnet
   export AKS_NAME= <your aks cluster name>
   ```

1. AKS サブネットを作成します

   ```console
   SUBNET_ID=$(az network vnet subnet show \
    --resource-group $RESOURCE_GROUP \
    --vnet-name $VNet_NAME \
    --name $SUBNET_NAME \
    --query id -o tsv)
   ```

次のスクリーンショットは、アーキテクチャ内の VNet にサブネットを配置する計画を示しています。

:::image type="content" source="media/active-directory-deployment-aks/ad-in-aks-diagram.png" alt-text="AD および SQL Server ビッグ データ クラスターを含む AKS クラスター":::

## <a name="create-an-aks-private-cluster"></a>AKS プライベート クラスターを作成する

次のコマンドを使用すれば、AKS プライベート クラスターを展開できます。 プライベート クラスターが不要な場合は、コマンド内の `--enable-private-cluster` パラメーターを削除します。 その他の要件については、[Azure Kubernetes (AKS) クラスターを展開する方法](/azure/aks/tutorial-kubernetes-deploy-cluster)に関するページを参照してください。

```azurecli
az aks create \
    --resource-group $RESOURCE_GROUP \
    --name $AKS_NAME \
    --load-balancer-sku standard \
    --enable-private-cluster \
    --network-plugin azure \
    --vnet-subnet-id $SUBNET_ID \
    --docker-bridge-address 172.17.0.1/16 \
    --dns-service-ip 10.3.0.10 \
    --service-cidr 10.3.0.0/24 \
    --node-vm-size Standard_D13_v2 \
    --node-count 2 \
    --generate-ssh-keys
```

AKS クラスターを展開したら、[その AKS クラスターに接続](/azure/aks/tutorial-kubernetes-deploy-cluster#connect-to-cluster-using-kubectl)します。

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>ドメイン コントローラーの逆引き DNS エントリを確認する

AD モードで AKS クラスターへの BDC の展開を開始する前に、DNS サーバーに登録されている **A レコード** と **PTR レコード** (逆引き DNS エントリ) の両方が、ドメイン コントローラー自体に含まれていることを確認します。

この設定を確認するには、`nslookup` コマンドを実行するか、または [PowerShell スクリプト](troubleshoot-ad-reverse-lookup-zone.md)を実行して、逆引き DNS エントリ (PTR レコード) が構成されているかどうかを確認します。

## <a name="create-bdc-deployment-profile"></a>BDC 展開プロファイルを作成する

次のコマンドを実行すると、展開プロファイルが作成されます。

```console
azdata bdc config init --source kubeadm-prod  --target bdc-ad-aks
```

展開プロファイルのパラメーターを設定するには、次のコマンドを利用します。

### <a name="controljson"></a>control.json

```console
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.storage.data.className=default"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.storage.logs.className=default"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[1].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[0].dnsName=controller.contoso.com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.spec.endpoints[1].dnsName=proxys.contoso.com"

# security settings 
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.dnsIpAddresses=[\"192.168.0.4\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.domainControllerFullyQualifiedDns=[\"ad1.contoso.com\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.domainDnsName=contoso.com"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -p bdc-ad-aks/control.json -j "$.security.activeDirectory.clusterUsers=[\"bdcusersgroup\"]"
```

### <a name="bdcjson"></a>bdc.json

```console
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=master.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=mastersec.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.master.spec.endpoints[1].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=gateway.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].serviceType=NodePort"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=approxy.contoso.com"
azdata bdc config replace -p bdc-ad-aks/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].serviceType=NodePort"
```

## <a name="initiate-deployment"></a>展開を開始する

次のコマンドを実行すると、BDC の展開が開始されます。

```console
azdata bdc create --config-profile bdc-ad-aks --accept-eula yes
```

## <a name="next-steps"></a>次のステップ

[Azure Data Studio を使用して SQL Server ビッグ データ クラスターに接続する](connect-to-big-data-cluster.md)

[チュートリアル:SQL Server ビッグ データ クラスターにサンプル データを読み込む](tutorial-load-sample-data.md)