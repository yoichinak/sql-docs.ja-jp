---
title: Active Directory で Azure Kubernetes Services (AKS) に展開する
titleSuffix: SQL Server Big Data Cluster
description: SQL Server ビッグ データ クラスターを AD モードで Azure Kubernetes Services (AKS) に展開する方法の概念および計画情報について説明します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 11/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3f6b3ce5f6a594e5be385ee1f7ea7d1c03c1f92a
ms.sourcegitcommit: 0f484f32709a414f05562bbaafeca9a9fc57c9ed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632970"
---
# <a name="deploy-sql-server-big-data-clusters-in-ad-mode-on-azure-kubernetes-services-aks"></a>Azure Kubernetes Services (AKS) に AD モードで SQL Server ビッグ データ クラスターを展開する

SQL Server ビッグ データ クラスターでは、**ID およびアクセス管理 (IAM)** 用の [Active Directory (AD) 展開モード](deploy-active-directory.md)をサポートしています。 **Azure Kubernetes Service (AKS)** 用の IAM は困難なものでした。これは、Microsoft ID プラットフォームで広くサポートされている OAuth 2.0 や OpenID Connect などの業界標準のプロトコルが SQL Server ではサポートされていないためです。  

この記事では、[Azure Kubernetes Service (AKS)](/azure/aks/intro-kubernetes) にビッグ データ クラスター (BDC) を展開するときに、AD モードで展開する方法について説明します。 

## <a name="architecture-topologies"></a>アーキテクチャ トポロジ

**Active Directory Domain Services (AD DS)** は、多くのオンプレミス インスタンスで実行される場合と[同じ方法で](/windows-server/identity/ad-ds/deploy/virtual-dc/adds-on-azure-vm)、Azure 仮想マシン (VM) 上でも実行されます。  Azure 内で新しいドメイン コントローラーを昇格したら、仮想ネットワーク用のプライマリおよびセカンダリ DNS サーバーを設定し、オンプレミスの DNS サーバーをいずれも降格します (この場合はターシャリ以降に降格されます)。 AD 認証を使用すると、Linux 上のドメインに参加しているクライアントは、そのドメインの資格情報と Kerberos プロトコルを使用して [SQL Server の認証を受ける](../linux/sql-server-linux-active-directory-auth-overview.md)ことができます。

BDC を AD モードで AKS に展開するには、いくつかの方法があります。  この記事では、実装および既存のエンタープライズレベルのアーキテクチャとの統合がより簡単な以下の 2 つの方法について説明します。

* **オンプレミスの Active Directory ドメインを Azure に拡張します。** この方法を使用すると、Active Directory Domain Services (AD DS) を Azure 上で使用することにより分散型の認証サービスを、[ご利用の Active Directory 環境で実現することができます](/azure/architecture/reference-architectures/identity/adds-extend-domain)。 クラウドからオンプレミスの AD DS に認証要求を送り返すことによって発生する待機時間を短縮するには、オンプレミスの Active Directory Domain Services (AD DS) をレプリケートします。 このソリューションが一般的に使用されるのは、ご利用のアプリケーションにオンプレミスでホストされる部分と Azure でホストされる部分があり、かつ認証要求のやりとりが必要な場合となります。

   このソリューションを展開する手順については、[こちらの参照アーキテクチャ](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-extend-domain)を参照してください。

* **Active Directory Domain Services (AD DS) リソース フォレストを Azure に拡張します。** このアーキテクチャでは、オンプレミスの AD フォレストによって信頼される新しいドメインを Azure 内に作成します。 このアーキテクチャは、[Azure 内のドメインからオンプレミスのフォレストへの一方向の信頼](/azure/architecture/reference-architectures/identity/adds-forest)を示しています。

   この信頼により、オンプレミスのユーザーは Azure のドメイン内のリソースにアクセスできるようになります。 このソリューションを展開する手順については、[こちらの参照アーキテクチャ](https://github.com/mspnp/identity-reference-architectures/tree/master/adds-forest)を参照してください。

前述の参照アーキテクチャを使用すれば、ランディング ゾーンを作成できます。これには、ゼロから展開されるすべてのリソース、または既存のアーキテクチャに基づいて適用される追加の対応策が含まれます。 これらの参照アーキテクチャに加えて、ご利用のターゲット VNet またはピアリングされた VNet に保持されている別個のサブネットの AKS クラスターに BDC を展開する必要があります。

次の図は、一般的なアーキテクチャを表しています。

:::image type="content" source="media/active-directory-deployment-aks/ad-in-aks-diagram.png" alt-text="AD および SQL Server ビッグ データ クラスターを含む AKS クラスター":::

## <a name="recommendations"></a>Recommendations

以下の推奨事項は、AKS に AD モードで BDC を展開するほとんどの場合に適用されます。 各コンポーネントには、エンタープライズレベルのアーキテクチャとの統合を強化するためのガイダンスを提供するのに使用可能なオプションが記述されています。

### <a name="networking-recommendations"></a>ネットワークの推奨事項

いくつかの重要なコンポーネントを使用すれば、オンプレミスの環境を Azure に接続することができます。

* **Azure VPN Gateway**: VPN ゲートウェイは、特定の種類の仮想ネットワーク ゲートウェイで、パブリック インターネットを介して Azure 仮想ネットワークとオンプレミスの場所の間で暗号化されたトラフィックを送信するために使用されます。 Azure Virtual Network ゲートウェイとローカル Virtual Network ゲートウェイの両方を使用します。 構成方法については、「[VPN ゲートウェイとは](/azure/vpn-gateway/vpn-gateway-about-vpngateways)」を参照してください。
* **Azure ExpressRoute**: ExpressRoute 接続はパブリックなインターネットを経由しないため、インターネット経由の一般的な接続に比べて、安全性と信頼性が高く、待機時間も短く、高速です。 接続オプションを選択すると、SKU に応じて、ソリューションの待機時間、パフォーマンス、および SLA レベルに影響が及びます。 詳細については、「[ExpressRoute の仮想ネットワーク ゲートウェイについて](/azure/expressroute/expressroute-about-virtual-network-gateways)」をご覧ください。

ほとんどのお客様は、ジャンプボックスまたは [Azure Bastion](/azure/bastion/bastion-overview) を使用して、他の Azure インフラストラクチャにアクセスします。 **Azure Private Link** を使用すると、ご利用の仮想ネットワーク内のプライベート エンドポイントを介して Azure PaaS Services (このシナリオの AKS など) やその他の Azure でホストされるサービスに安全にアクセスすることができます。 仮想ネットワークとサービスの間のトラフィックは、Microsoft のバックボーン ネットワークを経由するので、パブリック インターネットに公開されることがなくなります。 また、独自のプライベート リンク サービスを仮想ネットワークに作成し、そのサービスを顧客に非公開で配信することもできます。

### <a name="active-directory-and-azure-recommendation"></a>Active Directory と Azure の推奨事項

オンプレミスの AD DS で、ユーザー アカウントに関する情報を格納し、同じネットワーク上の他の承認されたユーザーがこの情報にアクセスできるようにするには、セキュリティ境界に含まれているユーザー、コンピューター、アプリケーション、またはその他のリソースに関連付けられている ID を認証します。 大部分のハイブリッドのシナリオでは、ユーザー認証は、オンプレミスの AD DS 環境への VPN Gateway または ExpressRoute 接続を経由して実行されます。  

AD モードでの BDC の展開の場合、[オンプレミスの Active Directory を Azure に統合する](/azure/architecture/reference-architectures/identity/)ためのソリューションを使用するには、次の前提条件を満たす必要があります。

* ご利用のオンプレミスの Active Directory で提供されている組織単位 (OU) 内にユーザー、グループ、コンピューターの各アカウントを作成するための[特定のアクセス許可が AD アカウントに用意されている](active-directory-prerequisites.md)。
* [内部 DNS を解決するための](active-directory-dns-reconciliation.md) DNS サーバー。 これには、このドメイン内の名前を持つ DNS サーバー内の **A (前方参照)** および **PTR (逆引き参照)** レコードの両方が含まれている必要があります。 BDC 展開プロファイルにドメイン DNS 設定を指定します。  

## <a name="next-steps"></a>次の手順

[チュートリアル: Azure Kubernetes Services (AKS) に AD モードで SQL Server ビッグ データ クラスターを展開する](active-directory-deployment-aks-tutorial.md)
