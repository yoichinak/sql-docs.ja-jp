---
title: レポート サーバーのパフォーマンスの監視 | Microsoft Docs
description: レポート サーバーのパフォーマンスを監視してサーバー活動を評価し、傾向を観察し、ボトルネックを診断し、システム構成に関するデータを収集する方法について説明します。
ms.date: 02/12/2021
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- report servers [Reporting Services], performance
- counters [Reporting Services]
- monitoring performance [Reporting Services]
- SQL Server Reporting Services, performance
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: c1bc13d4-8297-4daf-bb19-4c1e5ba292a6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f24b3bb19150271532561d691a1ed1f4c89dfbc5
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101838090"
---
# <a name="monitoring-report-server-performance"></a>レポート サーバーのパフォーマンスの監視

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

  パフォーマンス監視ツールを使用してレポート サーバーのパフォーマンスを監視することにより、サーバーの利用状況の評価、傾向の監視、システムのボトルネックの診断、および現在のシステム構成で十分かどうかを判断するためのデータの収集を行うことができます。 サーバーのパフォーマンスを調整するには、レポート サーバー アプリケーション ドメインを再利用する頻度を指定します。 詳細については、「 [レポート サーバー アプリケーションで利用可能なメモリの構成](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)」を参照してください。  
  
## <a name="sources-of-performance-data"></a>パフォーマンス データのソース  
 システムの実行状況に関する包括的な情報を取得するには、各種のテクノロジとツールを組み合わせて使用します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server オペレーティング システムでは、以下のツールでパフォーマンス情報を提供します。  
  
-   タスク マネージャー  
  
-   イベント ビューアー  
  
-   パフォーマンス モニター  
  
 タスク マネージャーは、コンピューター上で現在実行されているプログラムおよびプロセスに関する情報を提供します。 タスク マネージャーを使用することで、レポート サーバーのパフォーマンスに関する重要な指標を監視することができます。 また、実行中のプロセスの利用状況を査定したり、CPU やメモリの使用状況に関するグラフやデータを参照することもできます。 タスク マネージャーの使用方法については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows の製品マニュアルを参照してください。  
  
 イベント ビューアーとパフォーマンス モニターは、レポートの処理やリソースの消費に関するログおよび警告を作成する際に使用できます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で生成される Windows イベントの詳細については、「 [Windows アプリケーション ログ](../../reporting-services/report-server/windows-application-log.md)」を参照してください。 パフォーマンス モニターの詳細については、この記事で後述する「Windows パフォーマンス カウンター」をご覧ください。  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md) や[拡張イベント](../../relational-databases/extended-events/extended-events.md)のような [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティでは、キャッシュおよびセッション管理に使用するレポート サーバー データベースと一時データベースに関する情報も提供されます。  
  
## <a name="windows-performance-counters"></a>Windows パフォーマンス カウンター  
 個々のパフォーマンス カウンターを監視することで、次のことが可能になります。  
  
-   予測される負荷をサポートするために必要なシステム要件を算出する。  
  
-   構成の変更やアプリケーションのアップグレードの影響を測定するために、パフォーマンスのベースラインを作成する。  
  
-   実際の負荷、または人為的に生成した負荷の下で、アプリケーションのパフォーマンスを監視する。  
  
-   ハードウェアのアップグレードがパフォーマンスに所定の効果をもたらしたかどうかを検証する。  
  
-   システム構成の変更がパフォーマンスに所定の効果をもたらしたかどうかを検証する。  

  
## <a name="reporting-services-performance-objects"></a>Reporting Services パフォーマンス オブジェクト  
SQL Server Reporting Services 2016 以降には、次のパフォーマンス オブジェクトが含まれます。  
  
-   レポート サーバーのパフォーマンスを監視するための **MSRS 2016 Web Service** および **MSRS 2016 Web Service SharePoint Mode**。 これらのパフォーマンス オブジェクトには複数のカウンターが含まれ、主に対話的なレポート表示操作によって開始されるレポート サーバー処理の追跡に使用されます。 これらのカウンターは、レポート サーバー Web サービスが停止またはリサイクルされた時点でリセットされます。  
  
-   スケジュール設定した操作、およびレポートの配信を監視するための **MSRS 2016 Windows Service** および **MSRS 2016 Windows Service SharePoint Mode**。 これらのパフォーマンス オブジェクトには複数のカウンターが含まれ、スケジュールされた操作を介して開始されるレポート処理の追跡に使用されます。 スケジュールされた操作には、サブスクリプションと配信、レポート実行スナップショット、およびレポート履歴が含まれます。  
  
-   HTTP 関連のイベントおよびメモリ管理を監視するための **ReportServer:Service** および **ReportServerSharePoint:Service** to monitor HTTP-related events および memory management. これらは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に固有のカウンターです。要求、接続、サインイン試行など、レポート サーバーにおける HTTP 関連のイベントが追跡されます。 このパフォーマンス オブジェクトには、メモリ管理に関連したカウンターも含まれています。  
  
 1 台のコンピューターに複数のレポート サーバー インスタンスが存在する場合、インスタンスをまとめて監視することも個別に監視することもできます。 カウンターを追加する場合は、監視対象に含めるインスタンスを選択してください。 パフォーマンス モニター (perfmon.msc) の使用およびカウンターの追加に関する詳細については、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [Windows パフォーマンス モニター](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc749249(v=ws.11))の製品ドキュメントを参照してください。  
  
## <a name="other-performance-counters"></a>その他のパフォーマンス カウンター  
 カスタム [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] パフォーマンス カウンターは、上記の Reporting Services パフォーマンス オブジェクトに対してのみ提供されます。 次の .NET Framework パフォーマンス オブジェクトにより、レポート サーバーに関する補足的なパフォーマンス監視データが提供されます。
 
 > [!NOTE]
 > Power BI Report Server および SQL Server Reporting Services 2017 以降には、Reporting Services パフォーマンス オブジェクトは含まれていません。 [.NET Framework パフォーマンス カウンター](/dotnet/framework/debug-trace-profile/performance-counters)を使用すると、レポート サーバーのパフォーマンスの監視が可能になります。 
 
|パフォーマンス オブジェクト|Notes|  
|------------------------|-----------|  
|**.NET CLR データ** および **.NET CLR メモリ**|Web ポータルでは、[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] パフォーマンス カウンターが使用されます。 詳細については、「[.NET アプリケーションのパフォーマンスとスケーラビリティの改善](https://www.microsoft.com/download/details.aspx?id=11711)」をダウンロードしてください。|  
|**処理**|ReportingServicesService のインスタンスでプロセス ID ごとの稼働時間を追跡するための **Elapsed Time** および **ID Process** パフォーマンス カウンターを追加します。|  
  
## <a name="sharepoint-events"></a>SharePoint のイベント  
 レポート サーバーを SharePoint 統合モードで実行しており、SharePoint 製品を使用するようにレポート環境を構成している場合は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のパフォーマンス オブジェクトだけでなく、SharePoint のイベントを構成することもできます。 このセクションでは、「SharePoint 統合モードにおけるレポート サーバーのイベント」を基に、SharePoint と統合されたレポート環境で役立てることのできる診断イベントについて確認します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [Performance Counters for the MSRS 2016 Web Service および MSRS 2016 Windows Service パフォーマンス オブジェクトのパフォーマンス カウンター &#40;ネイティブ モード&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-web-service-performance-objects.md)  
 レポート サーバー Web サービスで使用するパフォーマンス カウンターについて説明します。  
  
 [MSRS 2016 Web Service SharePoint モードと MSRS 2016 Windows Service SharePoint モード パフォーマンス オブジェクトのパフォーマンス カウンター &#40;SharePoint モード&#41;](../../reporting-services/report-server/performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)  
 レポート サーバー Windows サービスで使用するパフォーマンス カウンターについて説明します。  
  
 [ReportServer:Service と ReportServerSharePoint:Service パフォーマンス オブジェクトのパフォーマンス カウンター](../../reporting-services/report-server/performance-counters-reportserver-service-performance-objects.md)  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]における HTTP およびメモリに関連したパフォーマンス カウンターについて説明します。  
  
## <a name="see-also"></a>関連項目  
 [レポート サーバー アプリケーションで利用可能なメモリの構成](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)   
 [Reporting Services レポート サーバー (ネイティブ モード)](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Reporting Services ツール](../../reporting-services/tools/reporting-services-tools.md)  
