---
title: SQL Server Profiler の実行
titleSuffix: SQL Server Profiler
description: SQL Server Profiler を開始できるプログラムとメニュー、トレース出力で使用される接続コンテキスト、テンプレート、フィルターについて説明します。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 07/07/2017
ms.openlocfilehash: d3b8bc77f5d4fd2bd549c253b8a64cfa86c6132c
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2020
ms.locfileid: "88713770"
---
# <a name="run-sql-server-profiler"></a>SQL Server Profiler の実行

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

さまざまなシナリオでのトレース出力の収集をサポートするために、いくつかの異なる方法で [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を実行できます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、Windows 10 の **[スタート]** メニューや[!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーの **[ツール]** メニューから起動できるほか、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] から起動することもできます。  
  
最初に [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を起動し、 **[ファイル]** メニューから **[新しいトレース]** を選択すると、 **[サーバーへの接続]** ダイアログ ボックスが表示されるので、接続先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定できます。  
## <a name="to-start-sql-server-profiler-from-the-windows-10-start-menu"></a>Windows 10 の [スタート] メニューから SQL Server Profiler を起動するには  
-  Windows の **[スタート]** アイコンをクリックするか、Windows キーを押して、「SQL Server Profiler 17」と入力し始めます。 **[SQL Server Profiler 17]** タイルが表示されたら、それをクリックします。   

## <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>データベース エンジン チューニング アドバイザーで SQL Server Profiler を起動するには  
-  [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーで、 **[ツール]** メニューの **[SQL Server Profiler]** をクリックします。  

## <a name="to-start-sql-server-profiler-in-sql-server-management-studio"></a>SQL Server Management Studio で SQL Server Profiler を開始するには  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の複数の場所から開始できます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を起動すると、その時点の接続コンテキスト、トレース テンプレート、およびフィルター コンテキストが読み込まれます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、各 SQL Server Profiler セッションがそれぞれのインスタンスで開始されます。Profiler は、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] をシャットダウンしても引き続き実行されます。  
### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>[ツール] メニューから SQL Server Profiler を起動するには  
-  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の **[ツール]** メニューで、 **[SQL Server Profiler]** をクリックします。  

### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>クエリ エディターから SQL Server Profiler を起動するには  
- クエリ エディター内で右クリックし、 **[SQL Server Profiler でクエリをトレース]** を選択します。  

  > [!NOTE]  
  >  接続コンテキストはエディター接続、トレース テンプレートは TSQL_SPs、適用されているフィルターは SPID = query window SPID です。  
    
### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>利用状況モニターから SQL Server Profiler を起動するには  
- 利用状況モニターで、 **[プロセス]** ウィンドウをクリックし、プロファイルするプロセスを右クリックします。次に、 **[SQL Server Profiler のトレース プロセス]** をクリックします。  

    > [!NOTE]  
    >  プロセスを選択したときに、利用状況モニターが開いていた場合、接続コンテキストはオブジェクト エクスプローラー接続になります。 トレース テンプレートはサーバーの種類に応じた既定値になります。SPID は、選択されたプロセスの SPID と等しくなります。  
    
## <a name="net-framework-security"></a>.NET Framework のセキュリティ  
- Windows 認証モードでは、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を実行するユーザー アカウントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続するアクセス許可を持っている必要があります。  
- [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]でトレースを実行するには、ユーザーが ALTER TRACE 権限も持っている必要があります。  

## <a name="next-steps"></a>次のステップ  
 [SQL Server Profiler の概要](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Management Studio の使用 [SQL Server]](../../ssms/sql-server-management-studio-ssms.md?view=sql-server-ver15)