---
title: Microsoft ビジネス インテリジェンス (BI) ツールでの分析とレポート
description: データ分析とレポートに対応するワークロード、およびこれらのワークロードに最も適した Microsoft BI ツールについて説明します。
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.prod: reporting-services
ms.technology: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.custom: seodec18
ms.date: 07/22/2020
ms.openlocfilehash: d6880689d05328b09c4f50b87ef8182c1c927afa
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891212"
---
# <a name="analysis-and-reporting-with-microsoft-business-intelligence-bi-tools"></a>Microsoft ビジネス インテリジェンス (BI) ツールでの分析とレポート

適切なビジネス インテリジェンス ツールを選択することは困難な場合があります。 さまざまな Microsoft 製品を確認し、ニーズに最も合う製品を見つけてください。

次の表は、データ分析とレポートに対応するワークロードを、これらのワークロードに最も適した Microsoft BI ツールに関連付けます。 製品に関する詳細については、表内の製品リンクをクリックしてください。  
  
 ツールの概要を確認し、どのツールが適しているかを判断するには、「[Microsoft Business Intelligence (BI) ツールの概要](https://download.microsoft.com/download/D/2/0/D20E1C5F-72EA-4505-9F26-FEF9550EFD44/Introducing_Microsoft_BI_Tools.docx)」を参照してください。

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。
  
|ワークロード|User|Excel ベースの BI ツール|SharePoint ベースの BI ツール|SharePoint Online ベースの BI ツール|Power BI ベースの BI ツール|SQL Server ベースの BI ツール|  
|---------------|----------|-|-|--------------|-|-|  
|**セルフサービス BI**|アナリスト/エンド ユーザー||||||  
|パブリック データと企業データの検出とアクセスの簡素化||[Excel 2016](https://support.office.com/article/What-s-new-in-Excel-2016-for-Windows-5fdb9208-ff33-45b6-9e08-1f5cdb3a6c73?ui=en-US&rs=en-US&ad=US)|||[Azure Data Catalog](https://azure.microsoft.com/services/data-catalog/)||  
|強力なデータ モデルの作成||[Power Pivot](https://support.office.com/article/Power-Pivot-Overview-and-Learning-f9001958-7901-4caa-ad80-028a6d2432ed?ui=en-US&rs=en-US&ad=US)|||[Power BI Desktop](/power-bi/fundamentals/desktop-get-the-desktop)||  
|セルフサービスの予測分析の実行||||||[Excel 用データ マイニング アドイン](/previous-versions/sql/2014/analysis-services/data-mining-client-for-excel-sql-server-data-mining-add-ins?view=sql-server-2014) |  
|データの視覚化と探索||[Power View](https://support.office.com/article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e)<br /><br /> [3D マップ](https://support.office.com/article/Visualize-your-data-in-3D-Maps-ce6b1d5c-4602-4dae-b487-91ec0268e75d)|||[Power BI Desktop](/power-bi/fundamentals/desktop-get-the-desktop)||  
|自然言語クエリを使用した問い合わせの実施|||||[Q & A](/power-bi/consumer/end-user-q-and-a)|
|モバイル デバイスを使用したレポートのアクセス||||[HTML 5 (< 10 MB ファイルの表示をサポート)](create-deploy-and-manage-mobile-and-paginated-reports.md)<br /><br /> | [HTML 5 (< 250 MB ファイルの表示をサポート)](https://go.microsoft.com/fwlink/p/?LinkId=391854)<br /><br /> [iOS デバイス上の Power BI モバイル アプリ](/power-bi/consumer/mobile/mobile-iphone-app-get-started)<br /><br /> [Android デバイス上の Power BI モバイル アプリ](/power-bi/consumer/mobile/mobile-android-app-get-started) <br /><br /> [Windows 10 用 Power BI モバイル アプリ](/power-bi/consumer/mobile/mobile-windows-10-phone-app-get-started)|  
|コラボレーションと共有|||[SharePoint サイト](/sharepoint/getting-started)|[SharePoint チーム サイト](https://go.microsoft.com/fwlink/?LinkId=391850)|[Power BI サイト](/power-bi/service-how-to-collaborate-distribute-dashboards-reports)||  
|**企業 BI**|IT プロフェッショナル||||||  
|多次元/表形式ビジネス モデルの作成||||||[Analysis Services](/analysis-services/analysis-services-overview)|  
|アドホック データ視覚エフェクトの作成|||[SharePoint 用の Power View](https://go.microsoft.com/fwlink/?LinkId=391858)||||  
|ダッシュボードの作成|||[SharePoint ダッシュボード](https://go.microsoft.com/fwlink/?LinkId=391859)<br /><br /> [PerformancePoint Services](/SharePoint/administration/performancepoint-services-overview)||[Power BI のダッシュボード](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/)||  
|運用レポートの作成||||||*[Reporting Services](create-deploy-and-manage-mobile-and-paginated-reports.md)|  
|カスタム レポートと埋め込みレポートの作成|||||[Power BI Embedded](create-deploy-and-manage-mobile-and-paginated-reports.md)|  
|**Advanced Analytics**|データ サイエンティスト||||||  
|セルフサービスの予測分析の実行||||||[Excel 用データ マイニング アドイン](/previous-versions/sql/2014/analysis-services/data-mining-client-for-excel-sql-server-data-mining-add-ins?view=sql-server-2014) |  
|データ マイニング アルゴリズムの使用||||||[Analysis Services 内でのデータ マイニング](/analysis-services/data-mining/data-mining-ssas)<br/><br/>[SQL Server R サービス](../machine-learning/r/sql-server-r-services.md?viewFallbackFrom=sql-server-ver15)|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
