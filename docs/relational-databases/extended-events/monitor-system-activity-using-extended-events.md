---
title: 拡張イベントを使用したシステムの使用状況の監視
description: 拡張イベントを Event Tracing for Windows と共に使用して、システムの使用状況を監視します。 CREATE EVENT SESSION、ALTER EVENT SESSION、および DROP EVENT SESSION について説明します。
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
helpviewer_keywords:
- xe
- extended events [SQL Server], monitoring system activity
ms.assetid: d83ad88f-818c-49fe-a9a9-299f704fca53
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c0c573d3271346e8e42fa0fb1a06fba0b20a136
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866783"
---
# <a name="monitor-system-activity-using-extended-events"></a>拡張イベントを使用したシステムの使用状況の監視

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  この手順は、拡張イベントを Event Tracing for Windows (ETW) と共に使用してシステムの使用状況を監視する方法を示します。 また、CREATE EVENT SESSION、ALTER EVENT SESSION、DROP EVENT SESSION の各ステートメントの使用方法についても説明します。  
  
 この作業には、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のクエリ エディターを使用した次の手順の実行も含まれます。 この手順では、コマンド プロンプトを使用して ETW コマンドを実行することも必要です。  
  
### <a name="to-monitor-system-activity-using-extended-events"></a>拡張イベントを使用してシステムの使用状況を監視するには  
  
1.  クエリ エディターで次のステートメントを実行してイベント セッションを作成し、2 つのイベントを追加します。 checkpoint_begin と checkpoint_end のイベントは、データベース チェックポイントの開始時と終了時に起動されます。  
  
    ```  
    CREATE EVENT SESSION test0  
    ON SERVER  
    ADD EVENT sqlserver.checkpoint_begin,  
    ADD EVENT sqlserver.checkpoint_end  
    WITH (MAX_DISPATCH_LATENCY = 1 SECONDS)  
    go  
    ```  
  
2.  32 バケットのバケット ターゲットを追加して、データベース ID に基づいたチェックポイントの数をカウントします。  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.histogram  
    (  
          SET slots = 32, filtering_event_name = 'sqlserver.checkpoint_end', source_type = 0, source = 'database_id'  
    )  
    go  
    ```  
  
3.  次のステートメントを実行して ETW ターゲットを追加します。 こうすると開始イベントと終了イベントを表示できるので、これを使用してチェックポイントの所要時間を判断できます。  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    ADD TARGET package0.etw_classic_sync_target  
    go  
    ```  
  
4.  次のステートメントを実行してセッションを開始し、イベント コレクションを開始します。  
  
    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = start  
    go  
    ```  
  
5.  次のステートメントを実行して 3 つのイベントを発生させます。  
  
    ```  
    USE tempdb  
          checkpoint  
    go  
    USE master  
          checkpoint  
          checkpoint  
    go  
    ```  
  
6.  次のステートメントを実行してイベント カウントを表示します。  
  
    ```  
    SELECT CAST(xest.target_data AS xml) Bucketizer_Target_Data_in_XML  
    FROM sys.dm_xe_session_targets xest  
    JOIN sys.dm_xe_sessions xes ON xes.address = xest.event_session_address  
    JOIN sys.server_event_sessions ses ON xes.name = ses.name  
    WHERE xest.target_name = 'histogram' AND xes.name = 'test0'  
    go  
    ```  
  
7.  コマンド プロンプトで、次のコマンドを実行すると ETW のデータが表示されます。  
  
    > [!NOTE]  
    >  **tracerpt** コマンドのヘルプを表示するには、コマンド プロンプトで「 `tracerpt /?`」と入力します。  
  
    ```  
    logman query -ets --- List the ETW sessions. This is optional.  
    logman update XE_DEFAULT_ETW_SESSION -fd -ets --- Flush the ETW log.  
    tracerpt %temp%\xeetw.etl -o xeetw.txt --- Dump the events so they can be seen.  
    ```  
  
8.  次のステートメントを実行してイベント セッションを停止し、サーバーから削除します。  

    ```  
    ALTER EVENT SESSION test0  
    ON SERVER  
    STATE = STOP  
    go  
  
    DROP EVENT SESSION test0  
    ON SERVER  
    go  
    ```  
  
## <a name="see-also"></a>参照  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [Extended Events Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [拡張イベントの動的管理ビュー](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [SQL Server 拡張イベント ターゲット](/previous-versions/sql/sql-server-2016/bb630339(v=sql.130))  
  
