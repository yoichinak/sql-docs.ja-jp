---
title: Azure Kubernetes Service (AKS) プライベート クラスターのビッグ データ クラスター (BDC) の管理
titleSuffix: SQL Server Big Data Cluster
description: Azure Kubernetes Service (AKS) プライベート クラスターの SQL Server ビッグ データ クラスター (BDC) を管理する方法について説明します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 442f5def7e1378b750460cfc6860e780b1dcfd80
ms.sourcegitcommit: fe5dedb2a43516450696b754e6fafac9f5fdf3cf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/31/2020
ms.locfileid: "89202232"
---
# <a name="manage-big-data-cluster-in-aks-private-cluster"></a>AKS プライベート クラスターのビッグ データ クラスターを管理する

この記事では、Azure で SQL Server ビッグ データ クラスター (BDC) を含む Azure Kubernetes Service (AKS) プライベート クラスターを管理する方法について説明します。

[プライベート クラスターの作成](/azure/aks/private-clusters/)に関する記事で説明されているように、AKS プライベート クラスターの API サーバー エンドポイントにはパブリック IP アドレスがありません。 API サーバーを管理するには、AKS クラスターの Azure Virtual Network (VNet) にアクセスできる VM を使用します。

## <a name="azure-vm---same-vnet"></a>Azure VM - 同じ VNet

最も簡単な方法は、AKS クラスターと同じ VNet に Azure VM をデプロイすることです。

1. AKS クラスターと同じ VNet に Azure VM をデプロイします。 これは、*ジャンプボックス*とも呼ばれます。
1. その VM に接続して、[SQL Server 2019 のビッグ データ ツールをインストール](deployment-guidance.md#install-sql-server-2019-big-data-tools)します。

セキュリティのため、API サーバーの許可された IP 範囲に対して AKS の機能を使用して、(AKS コントロール プレーン上の) API サーバーへのアクセスを制限します。 制限付きアクセスでは、特定の IP アドレス (ジャンプボックス VM や管理 VM など) または開発者グループ用の IP アドレス範囲、およびファイアウォールのパブリック フロントエンド IP アドレスを使用できます。

## <a name="other-options"></a>その他のオプション

ジャンプボックスを使用する以外に、次のような方法もあります。

* 別のネットワーク内の VM を使用し、VNet に対して[仮想ネットワーク ピアリング](/azure/virtual-network/virtual-network-peering-overview)を設定します。

* [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) 接続または [VPN Gateway](/azure/vpn-gateway/vpn-gateway-about-vpngateways) 接続。

   これらの方法の詳細については、「[プライベート クラスターに接続するための選択肢](/azure/aks/private-clusters#options-for-connecting-to-the-private-cluster)」を参照してください。

* サービスが [Azure Standard Load Balancer](/azure/aks/load-balancer-standard) の背後で実行されている場合は、そのサービスを [Azure Private Link](/azure/private-link/private-link-service-overview#limitations) に対して有効にすることができます。 Azure Private Link を使用すると、他の Azure VNet からのプライベート アクセスを有効にすることができます。

* ハイブリッド シナリオでは、[Azure ExpressRoute](/azure/expressroute/expressroute-introduction) または [VPN Gateway](/azure/vpn-gateway/vpn-gateway-about-vpngateways) 接続を設定することもできます。

## <a name="next-steps"></a>次のステップ

[Azure Data Studio を使用して SQL Server ビッグ データ クラスターに接続する](connect-to-big-data-cluster.md)