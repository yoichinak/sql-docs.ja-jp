---
description: DQS の参照データ サービス
title: DQS の参照データ サービス
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ef217717-6d05-443e-af26-44dc745a349d
author: swinarko
ms.author: sawinark
ms.openlocfilehash: cd20a9ca7a25e1e00613ea5c87baa9eda41accc8
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726630"
---
# <a name="reference-data-services-in-dqs"></a>DQS の参照データ サービス

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  参照データとは、信頼されたパブリック ドメインで使用できる、またはプレミアム商用コンテンツ プロバイダーから提供される、関連または項目別のグローバル データ (エンタープライズの境界を超えるデータ) の正確で完全なセットを表します。  
  
 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) の Reference Data Service 機能を使用すると、サード パーティ参照データ プロバイダーをサブスクライブしたり、ビジネス データを高品質データに対して検証してビジネス データを簡単にクレンジングおよび強化することができます。 DQS 内から業界をリードするデータ品質サービス プロバイダーのサービスを使用して、クレンジング プロセス中にデータを標準化、修正、または強化できます。 たとえば、市外局番コードや郵便番号の一覧を参照データに対して使用して、顧客の住所を検証できます。  
  
 Reference Data Service 機能には、次の利点があります。  
  
-   参照データを使用すると、参照データをサード パーティ企業で保証されているデータと比較してデータの品質を確保できます。  
  
-   参照データ処理は、DQS ナレッジ ベースの構築およびデータ品質プロジェクトに組み込まれているので、包括的なデータ品質プロセスを確立できます。  
  
-   は、サードパーティ参照データプロバイダーから直接、または Azure Marketplace からの参照データの使用をサポートしています。  
  
##  <a name="using-reference-data-from-azure-marketplace"></a><a name="Marketplace"></a> Azure Marketplace から参照データを使用する  
 DQS では、Azure Marketplace の参照データを使用して、コンテンツプロバイダーが Marketplace を通じて参照データサービスを提供できるようにします。 Marketplace は、高品質データおよびアプリケーションの単一のマーケットプレイスと配信チャネルをクラウド サービスとして提供するマイクロソフトのサービスです。 Marketplace の詳細については、「 [Microsoft Azure Marketplace につい](https://azuremarketplace.microsoft.com/about) て (」を参照してください https://azuremarketplace.microsoft.com/about) 。
  
 Marketplace と DQS のシームレスな統合により、DQS 内からのデータ品質プロジェクトに関する情報の検出、検索、および取得に関連付けられている手順が簡素化されます。 このデータは DQS から使用され、DQS ユーザーはこのデータを使用して DQS、Marketplace、および参照データ サービス プロバイダーを革新的な方法で 1 つにまとめて、データの品質を高めることができます。  
  
 DQS でクレンジング アクティビティに Marketplace の参照データを使用するには、Marketplace アカウント キーが必要です。 Marketplace アカウント キーの作成は無料です。有料のデータセットをサブスクライブする場合にのみ料金がかかります。 無料のデータセットのサブスクライブと使用には料金はかかりません。 Marketplace アカウントキーの作成の詳細については、「 [アカウントの作成](/previous-versions/azure/ff717655(v=azure.100)) 」 (を参照してください https://go.microsoft.com/fwlink/?LinkId=212936) 。  
  
 また、DQS 内から次の Marketplace アクティビティを実行できます。  
  
-   Marketplace でデータセットを参照する。  
  
-   Marketplace アカウント キーを作成する。  
  
-   アカウント キーやデータ プロバイダーのサブスクリプションなど、Marketplace アカウントの詳細を管理する。  
  
 これらのアクティビティは、 **の** [構成] **画面の** [参照データ] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]タブで実行できます。  
  
##  <a name="using-reference-data-directly-from-the-third-party-reference-data-providers"></a><a name="Direct"></a> サード パーティ参照データ プロバイダーから参照データを直接使用する  
 インターネットに接続していないため Marketplace を使用できない場合は、DQS で組織のネットワーク内で使用できるデータ プロバイダーに直接接続することもできます。 ダイレクト オンライン サード パーティ参照データ プロバイダーの参照データを使用するには、DQS でデータ プロバイダーのレコードを作成する必要があります。  
  
##  <a name="how-to-cleanse-data-by-using-the-reference-data"></a><a name="HowToCleanse"></a> 参照データを使用してデータをクレンジングする方法  
 参照データを使用した DQS でのデータのクレンジングには、次の 3 つの手順が含まれます。  
  
1.  **DQS で参照データ プロバイダーの詳細を構成する**: DQS で参照データを使用する前に、DQS で参照データ サービスの詳細を構成する必要があります。  
  
    1.  Marketplace を使用している場合は、有効な Marketplace アカウントキーを指定し、Marketplace の [Data Services](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=data-services) データカテゴリを参照して、必要なプロバイダーをサブスクライブします。  
  
    2.  ダイレクト オンライン参照データ プロバイダーを使用する場合は、ダイレクト参照データ プロバイダーを DQS に追加してから使用する必要があります。  
  
     DQS での参照データ プロバイダーの詳細の構成は、1 つのデータ プロバイダーに対して 1 回だけ実行するアクティビティです。 DQS 管理者だけが、DQS で参照データ設定を構成できます。  
  
2.  **ナレッジ ベースのドメインまたは複合ドメインを参照データ サービスにマップする**: 手順 1. でサブスクライブまたは追加された適切な参照データ サービスに、ドメインまたは複合ドメインをマップします。  
  
3.  **データ品質プロジェクトでマップされたドメインをクレンジング アクティビティに使用する**: **クレンジング** アクティビティのデータ品質プロジェクトを作成しているときに、手順 2. で参照データ サービスにマップされたドメインまたは複合ドメインを含むナレッジ ベースを選択し、クレンジング アクティビティを実行します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|Marketplace またはダイレクト オンライン サード パーティ データ プロバイダーの参照データ サービスを使用するように DQS を構成する方法を説明します。|[参照データを使用する DQS の構成](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|ナレッジ ベースのドメインまたは複合ドメインを参照データ サービスにマップする方法を説明します。|[参照データへのドメインまたは複合ドメインのアタッチ](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|参照データ サービスを使用してデータをクレンジングする方法を説明します。|[参照データ &#40;外部&#41; のナレッジを使用したデータのクレンジング](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
  
