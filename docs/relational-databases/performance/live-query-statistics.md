---
title: '[ライブ クエリ統計] | Microsoft Docs'
description: SQL Server Management Studio でアクティブ クエリのライブ実行プランを表示する方法について説明します。 実行統計値を利用し、クエリ パフォーマンス問題をデバッグします。
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query statistics [SQL Server] live query stats
- live query statistics
- debugging [SQL Server], live query stats
- statistics [SQL Server], live query statistics
- query profiling
- lightweight query profiling
- lightweight profiling
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753e
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: fe6467cbe5cc915b876b9efa6b8afd9ff59e2bbd
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890783"
---
# <a name="live-query-statistics"></a>[ライブ クエリ統計]
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、アクティブ クエリのライブ実行プランを表示できます。 このライブ クエリ プランでは、[クエリ プラン演算子](../../relational-databases/showplan-logical-and-physical-operators-reference.md)間の制御フローとして、クエリ実行プロセスをリアルタイムで洞察できます。 ライブ クエリ プランには、全体的なクエリ進捗状況と演算子レベルのランタイム実行統計が表示されます。生成された行の数、経過時間、演算子の進捗状況などです。このデータはクエリの完了を待つことなくリアルタイムで利用できるため、これらの実行統計はクエリ パフォーマンス問題のデバッグで非常に役立ちます この機能は [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 以降のバージョンで使用できますが、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] でも動作します。  

> [!NOTE]
> 内部的には、ライブ クエリ統計では、[sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md) DMV を利用します。
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降) および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
> [!WARNING]  
> この機能は、主にトラブルシューティングの目的で使用されます。 この機能を利用すると、特に [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] で、全体的なクエリ パフォーマンスがやや遅くなることがあります。 詳細については、「[クエリ プロファイリング インフラストラクチャ](../../relational-databases/performance/query-profiling-infrastructure.md)」を参照してください。  
> この機能は [Transact-SQL デバッガー](../../ssms/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md)と共に利用できます。  
  
## <a name="to-view-live-query-statistics-for-one-query"></a>1 つのクエリのライブ クエリ統計を表示するには 
  
1.  ライブ クエリ実行プランを表示するには、ツール メニューで、 **[ライブ クエリ統計を含む]** アイコンをクリックします。  
  
     ![ツールバーの [ライブ クエリ統計] ボタン](../../relational-databases/performance/media/livequerystatstoolbar.png "ツールバーの [ライブ クエリ統計] ボタン")  
  
     [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で選択したクエリを右クリックし、 **[ライブ クエリ統計を含める]** をクリックしてライブ クエリ実行プランを表示することもできます。  
  
     ![ポップアップ メニューの [ライブ クエリ統計] ボタン](../../relational-databases/performance/media/livequerystatsmenu.png "ポップアップ メニューの [ライブ クエリ統計] ボタン")  
  
2.  クエリを実行します。 ライブ クエリ プランには、経過時間や進捗状況など、全体的なクエリ進捗状況と演算子レベルのランタイム実行統計がクエリ プラン演算子に対して表示されます。 クエリ実行の進捗中は、クエリ進捗状況情報と実行統計が定期的に更新されます。 この情報を利用して全体的なクエリ実行プロセスを理解し、実行時間の長いクエリ、無限に実行されるクエリ、tempdb オーバーフローを引き起こすクエリ、タイムアウト問題をデバッグします。  
  
     ![表示プランの [ライブ クエリ統計] ボタン](../../relational-databases/performance/media/livequerystatsplan.png "表示プランの [ライブ クエリ統計] ボタン")  
  
## <a name="to-view-live-query-statistics-for-any-query"></a>任意のクエリのライブ クエリ統計を表示するには 

ライブ実行プランは、 **[プロセス]** または **[アクティブなコストの高いクエリ]** テーブルの任意のクエリを右クリックすることで、 **[利用状況モニター](../../relational-databases/performance-monitor/activity-monitor.md)** からもアクセスできます。  
  
 ![利用状況モニターでの [ライブ クエリ統計] ボタン](../../relational-databases/performance/media/livequerystatsactmon.png "利用状況モニターでの [ライブ クエリ統計] ボタン")  
  
## <a name="remarks"></a>解説  
 ライブ クエリ統計でクエリの進捗状況に関する情報を記録するには、この統計プロファイル インフラストラクチャを有効にする必要があります。 バージョンによっては、オーバーヘッドが大きくなる可能性があります。 このオーバーヘッドの詳細については、「[クエリ プロファイリング インフラストラクチャ](../../relational-databases/performance/query-profiling-infrastructure.md)」を参照してください。
  
## <a name="permissions"></a>アクセス許可  
**[ライブ クエリ統計]** 結果ページに値を設定するにはデータベース レベルの `SHOWPLAN` アクセス許可が必要です。クエリを実行するには必要なすべてのアクセス許可が必要です。
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でライブ統計を表示するには、サーバーレベルの `VIEW SERVER STATE` アクセス許可が必要です。  
[!INCLUDE[ssSDS](../../includes/sssds-md.md)] の Premium 階層でライブ統計を表示するには、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] の Standard 階層と Basic 階層でライブ統計を表示するには、**サーバー管理者**または **Azure Active Directory 管理者**のアカウントが必要です。
  
## <a name="see-also"></a>参照  
 [実行プラン](../../relational-databases/performance/execution-plans.md)    
 [クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md)    
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [パフォーマンス監視およびチューニング ツール](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [利用状況モニターを開く方法 &#40;SQL Server Management Studio&#41;](../../relational-databases/performance-monitor/open-activity-monitor-sql-server-management-studio.md)     
 [利用状況モニター](../../relational-databases/performance-monitor/activity-monitor.md)     
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [プラン表示の論理操作と物理操作のリファレンス](../../relational-databases/showplan-logical-and-physical-operators-reference.md)     
 [クエリ プロファイリング インフラストラクチャ](../../relational-databases/performance/query-profiling-infrastructure.md)