---
description: sys.event_log (Azure SQL データベース)
title: sys.event_log (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- event_log
- sys.event_log_TSQL
- event_log_TSQL
- sys.event_log
dev_langs:
- TSQL
helpviewer_keywords:
- event_log
- sys.event_log
ms.assetid: ad5496b5-e5c7-4a18-b5a0-3f985d7c4758
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 67c111b15728f92e3a6f0ac8dac830fe32f2f8da
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892402"
---
# <a name="sysevent_log-azure-sql-database"></a>sys.event_log (Azure SQL データベース)

[!INCLUDE[Azure SQL Database](../../includes/applies-to-version/asdb.md)]

  成功した [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] データベース接続、接続エラー、およびデッドロックを返します。 この情報を使用して、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] でのデータベースの利用状況の追跡またはトラブルシューティングを行うことができます。  
  
> [!CAUTION]  
> 多数のデータベースまたは多数のログインがあるインストールでは、sys.event_log のアクティビティによって、パフォーマンスや CPU 使用率が制限され、場合によってはログインエラーが発生する可能性があります。 Sys.event_log のクエリは、問題に寄与する可能性があります。 Microsoft はこの問題の解決に取り組んでいます。 その間、この問題の影響を軽減するために、sys.event_log のクエリを制限します。 NewRelic SQL Server プラグインのユーザーは、追加の構成情報について、 [Microsoft Azure SQL Database プラグインのチューニング & パフォーマンスの微調整](https://discuss.newrelic.com/t/microsoft-azure-sql-database-plugin-tuning-performance-tweaks/30729) に関するページにアクセスする必要があります。  
  
 ビューには `sys.event_log` 、次の列が含まれています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|データベースの名前です。 接続が失敗し、ユーザーがデータベース名を指定していない場合、この列は空白です。|  
|**start_time**|**datetime2**|集計間隔の開始時刻を示す UTC 日時。 集計イベントの場合、時刻は常に 5 分単位になります。 次に例を示します。<br /><br /> ' 2011-09-28 16:00:00 '<br />' 2011-09-28 16:05:00 '<br />' 2011-09-28 16:10:00 '|  
|**end_time**|**datetime2**|集計間隔の終了時刻を示す UTC 日時。 集計イベントの場合、 **End_time** は、同じ行の対応する **start_time** よりも常に5分後になります。 集計されていないイベントの場合、 **start_time** と **end_time** はイベントの実際の UTC 日時と同じになります。|  
|**event_category**|**nvarchar (64)**|このイベントを生成した上位レベルのコンポーネント。<br /><br /> 使用可能な値の一覧については、「 [イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) 」を参照してください。|  
|**event_type**|**nvarchar (64)**|イベントの種類。<br /><br /> 使用可能な値の一覧については、「 [イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) 」を参照してください。|  
|**event_subtype**|**int**|発生したイベントのサブタイプ。<br /><br /> 使用可能な値の一覧については、「 [イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) 」を参照してください。|  
|**event_subtype_desc**|**nvarchar (64)**|イベントのサブタイプの説明。<br /><br /> 使用可能な値の一覧については、「 [イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) 」を参照してください。|  
|**severity**|**int**|エラーの重大度。 次のいずれかの値になります。<br /><br /> 0 = 情報<br />1 = 警告<br />2 = エラー|  
|**event_count**|**int**|指定された期間内に、指定されたデータベースでこのイベントが発生した回数 (**start_time** および **end_time**)。|  
|**description**|**nvarchar(max)**|イベントの詳細な説明。<br /><br /> 使用可能な値の一覧については、「 [イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) 」を参照してください。|  
|**additional_data**|**XML**|*注: Azure SQL Database V12 では、この値は常に NULL です。V12 のデッドロックイベントを取得する方法については、「 [例](#Deadlock) 」を参照してください。*<br /><br /> **デッドロック**イベントの場合は、この列にデッドロックグラフが表示されます。 他の種類のイベントの場合、この列は NULL になります。 |  
  
##  <a name="event-types"></a><a name="EventTypes"></a> イベントの種類

 このビューの各行によって記録されるイベントは、カテゴリ (**event_category**)、イベントの種類 (**event_type**)、およびサブタイプ (**event_subtype**) によって識別されます。 次の表に、このビューで収集されるイベントの種類を示します。  
  
 **接続**カテゴリのイベントについては、[sys.database_connection_stats] ビューで概要情報を確認できます。  
  
> [!NOTE]  
> このビューには、発生する可能性のあるすべての [!INCLUDE[ssSDS](../../includes/sssds-md.md)] データベース イベントが表示されるわけではなく、この表に示されているイベントのみが表示されます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] の今後のリリースで他のカテゴリ、イベントの種類、およびサブタイプが報告対象として追加される可能性はあります。  
  
|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|**severity**|**description**|  
|-------------------------|---------------------|------------------------|------------------------------|------------------|---------------------|  
|**できる**|**connection_successful**|0|**connection_successful**|0|データベースに正常に接続されました。|  
|**できる**|**connection_failed**|0|**invalid_login_name**|2|ログイン名がこのバージョンの SQL Server では無効です。|  
|**できる**|**connection_failed**|1|**windows_auth_not_supported**|2|Windows ログインは、このバージョンの SQL Server ではサポートされていません。|  
|**できる**|**connection_failed**|2|**attach_db_not_supported**|2|サポートされていないデータベース ファイルのアタッチをユーザーが要求しました。|  
|**できる**|**connection_failed**|3|**change_password_not_supported**|2|サポートされていないユーザー ログインのパスワード変更をユーザーが要求しました。|  
|**できる**|**connection_failed**|4|**login_failed_for_user**|2|ユーザーのログインに失敗しました。|  
|**できる**|**connection_failed**|5|**login_disabled**|2|ログインが無効でした。|  
|**できる**|**connection_failed**|6|**failed_to_open_db**|2|*注: Azure SQL Database V11 にのみ適用されます。*<br /><br /> データベースを開くことができませんでした。 データベースが存在しないこと、またはデータベースを開くための認証が不足していることが原因で発生する場合があります。|  
|**できる**|**connection_failed**|7|**blocked_by_firewall**|2|クライアントの IP アドレスからサーバーにアクセスすることが許可されていません。|  
|**できる**|**connection_failed**|8|**client_close**|2|*注: Azure SQL Database V11 にのみ適用されます。*<br /><br /> 接続の確立時にクライアントがタイムアウトした可能性があります。 接続タイムアウトを増やしてください。|  
|**できる**|**connection_failed**|9|**ブート**|2|*注: Azure SQL Database V11 にのみ適用されます。*<br /><br /> データベースで再構成が行われていたため、接続に失敗しました。|  
|**できる**|**connection_terminated**|0|**idle_connection_timeout**|2|*注: Azure SQL Database V11 にのみ適用されます。*<br /><br /> システム定義のしきい値より長く接続のアイドル状態が続いています。|  
|**できる**|**connection_terminated**|1|**ブート**|2|*注: Azure SQL Database V11 にのみ適用されます。*<br /><br /> データベース再構成が原因で、セッションが終了しました。|  
|**できる**|**調整**|*\<reason code>*|**reason_code**|2|*注: Azure SQL Database V11 にのみ適用されます。*<br /><br /> 要求が調整されています。  調整理由コード: *\<reason code>* 。 詳細については、「 [エンジン調整](/previous-versions/azure/dn338079(v=azure.100))」を参照してください。|  
|**できる**|**throttling_long_transaction**|40549|**long_transaction**|2|*注: Azure SQL Database V11 にのみ適用されます。*<br /><br /> トランザクションが長時間実行されているため、セッションを終了しました。 トランザクションを短くしてください。 詳細については、「 [リソースの制限](/previous-versions/azure/dn338081(v=azure.100))」を参照してください。|  
|**できる**|**throttling_long_transaction**|40550|**excessive_lock_usage**|2|*注: Azure SQL Database V11 にのみ適用されます。*<br /><br /> 取得したロックの数が多すぎるため、セッションを終了しました。 1 つのトランザクションで読み取る行または変更する行の数を減らしてください。 詳細については、「 [リソースの制限](/previous-versions/azure/dn338081(v=azure.100))」を参照してください。|  
|**できる**|**throttling_long_transaction**|40551|**excessive_tempdb_usage**|2|*注: Azure SQL Database V11 にのみ適用されます。*<br /><br /> TEMPDB の使用量が多すぎるため、セッションを終了しました。 クエリを変更して一時テーブルの使用領域を減らしてください。 詳細については、「 [リソースの制限](/previous-versions/azure/dn338081(v=azure.100))」を参照してください。|  
|**できる**|**throttling_long_transaction**|40552|**excessive_log_space_usage**|2|*注: Azure SQL Database V11 にのみ適用されます。*<br /><br /> トランザクション ログの使用領域が多すぎるため、セッションを終了しました。 1 回のトランザクションで変更する行を減らしてください。 詳細については、「 [リソースの制限](/previous-versions/azure/dn338081(v=azure.100))」を参照してください。|  
|**できる**|**throttling_long_transaction**|40553|**excessive_memory_usage**|2|*注: Azure SQL Database V11 にのみ適用されます。*<br /><br /> メモリの使用量が多すぎるため、セッションを終了しました。 クエリを変更して、処理する行を減らしてください。 詳細については、「 [リソースの制限](/previous-versions/azure/dn338081(v=azure.100))」を参照してください。|  
|**双発**|**deadlock**|0|**deadlock**|2|デッドロックが発生しました。|  
  
## <a name="permissions"></a>アクセス許可

 **Master**データベースへのアクセス権限を持つユーザーには、このビューに対する読み取り専用アクセス権があります。  
  
## <a name="remarks"></a>解説  
  
### <a name="event-aggregation"></a>イベント集計

 このビューのイベント情報は、5 分未満の間隔で収集および集計されます。 **Event_count**列は、特定の期間内に特定のデータベースに対して特定の**event_type**と**event_subtype**が発生した回数を表します。  
  
> [!NOTE]  
> デッドロックなど、一部のイベントは集計されません。 これらのイベントの場合、 **event_count** は1と **start_time** になり、 **end_time** はイベントが発生した実際の UTC 日時と同じになります。  
  
 たとえば、2012 年 2 月 5 日 (UTC) の 11:00 から 11:05 までに、無効なログイン名が原因でユーザーがデータベース Database1 への接続に 7 回失敗した場合、この情報はこのビューの単一行に示されます。  
  
|**database_name**|**start_time**|**end_time**|**event_category**|**event_type**|**event_subtype**|**event_subtype_desc**|**severity**|**event_count**|**description**|**additional_data**|  
|------------------------|---------------------|-------------------|-------------------------|---------------------|------------------------|------------------------------|------------------|----------------------|---------------------|--------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`connectivity`|`connection_failed`|`4`|`login_failed_for_user`|`2`|`7`|`Login failed for user.`|`NULL`|  
  
### <a name="interval-start_time-and-end_time"></a>間隔の start_time と end_time  
 イベントが集計間隔に含まれるのは、イベントが*on* **start_time**の_後_、またはその後に発生してから、その間隔の**end_time** _前_です。 たとえば、`2012-10-30 19:25:00.0000000` に発生したイベントは、下に示す例では 2 つ目の間隔にのみ含まれます。  
  
```
start_time                    end_time  
2012-10-30 19:20:00.0000000   2012-10-30 19:25:00.0000000  
2012-10-30 19:25:00.0000000   2012-10-30 19:30:00.0000000  
```

### <a name="data-updates"></a>データの更新

 このビューのデータは時間の経過に伴って累計されます。 一般的に、データは集計間隔の開始から 1 時間以内で累計されますが、すべてのデータがビューに表示されるまでに、最大 24 時間かかることもあります。 その間に、1 つの行内の情報が定期的に更新されることがあります。  
  
### <a name="data-retention"></a>データ保有期間

 このビューのデータは、最大で30日間保持されます。データベースの数や、各データベースが生成する一意のイベントの数によっては、それよりも少ない場合があります。 この情報をより長期間にわたって保持するには、データを別のデータベースにコピーします。 ビューの最初のコピーを行った後に、そのビューの行がデータの累積に伴って更新されることがあります。 データのコピーを最新の状態に保つには、定期的に行のテーブル スキャンを行うことにより、既存の行のイベント数の増加を検出し、新しい行を特定して (開始時刻と終了時刻を使用して一意の行を識別できます)、これらの更新内容をデータのコピーに反映させます。  
  
### <a name="errors-not-included"></a>含まれないエラー

 このビューには、接続およびエラーに関する情報がすべて含まれていないことがあります。  
  
- このビューには [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 、発生する可能性があるすべてのデータベースエラーが含まれているわけではなく、このトピックの [イベントの種類](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md#EventTypes) で指定されているものだけです。  
- データセンター内でコンピューター障害が発生した場合は、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 少量のデータがイベントテーブルに存在しない可能性があります。  
- DoSGuard によって IP アドレスがブロックされている場合は、その IP アドレスからの接続試行イベント情報を収集することができないため、このビューに表示されません。  
  
## <a name="examples"></a>例  
  
### <a name="simple-examples"></a>簡単な例

 次のクエリは、2011 年 9 月 25 日の正午から 2011 年 9 月 28 日の正午 (UTC) までに発生したすべてのイベントを返します。 既定では、クエリの結果は **start_time** (昇順) に並べ替えられます。  

```sql
SELECT * FROM sys.event_log
WHERE start_time >= '2011-09-25 12:00:00'
    AND end_time <= '2011-09-28 12:00:00';  
```

次のクエリは、データベース Database1 のすべてのデッドロックイベントを返します (Azure SQL Database V11 にのみ適用されます)。  

```sql
SELECT * FROM sys.event_log
WHERE event_type = 'deadlock'
    AND database_name = 'Database1';  
```

<a name="Deadlock"></a> 次のクエリは、データベース Database1 のすべてのデッドロックイベントを返します (Azure SQL Database V12 にのみ適用されます)。  

```sql
WITH CTE AS (  
       SELECT CAST(event_data AS XML)  AS [target_data_XML]  
   FROM sys.fn_xe_telemetry_blob_target_read_file('dl', null, null, null)  
)  
SELECT target_data_XML.value('(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
target_data_XML.query('/event/data[@name=''xml_report'']/value/deadlock') AS deadlock_xml,  
target_data_XML.query('/event/data[@name=''database_name'']/value').value('(/value)[1]', 'nvarchar(100)') AS db_name  
FROM CTE  
```

次のクエリは、2011 年 9 月 25 日 (UTC) の 10:00 から 11:00 までに発生した SQL ワーカー スレッド イベントに対するハード調整を返します。  

```sql
SELECT * FROM sys.event_log
WHERE event_type = 'throttling'
    AND event_subtype = 4194307
    AND start_time >= '2011-09-25 10:00:00'
    AND end_time <= '2011-09-25 11:00:00';  
```

### <a name="db-scoped-extended-event"></a>DB-Scoped 拡張イベント

 次のサンプルコードを使用して、データベーススコープの拡張イベント (XEvent) セッションを設定します。  

```sql
IF EXISTS  
    (SELECT * from sys.database_event_sessions  
        WHERE name = 'azure_monitor_deadlock_session')  
BEGIN  
    ALTER EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE  
        DROP TARGET package0.ring_buffer;  
  
    DROP EVENT SESSION azure_monitor_deadlock_session  
        ON DATABASE;  
END  
  
CREATE EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    ADD EVENT sqlserver.database_xml_deadlock_report  
    ADD TARGET package0.ring_buffer  
    (  
        SET max_memory = 2048, max_events_limit = 10  
    )  
    WITH (STARTUP_STATE = ON,  
          EVENT_RETENTION_MODE = ALLOW_SINGLE_EVENT_LOSS);  
  
ALTER EVENT SESSION azure_monitor_deadlock_session  
    ON DATABASE  
    STATE = START;  
```

### <a name="check-for-deadlock"></a>デッドロックを確認する

次のクエリを使用して、デッドロックが発生していないかどうかを確認します。  

```sql
WITH CTE AS (  
    SELECT CAST(xet.target_data AS XML)  AS [target_data_XML]  
        FROM            sys.dm_xe_database_session_targets AS xet  
             INNER JOIN sys.dm_xe_database_sessions        AS xe  
                 ON (xe.address = xet.event_session_address)  
        WHERE xe.name = 'azure_monitor_deadlock_session'  
)  
, CTE2 AS (  
    SELECT  
            T2.EventData.query('.').value(  
                '(/event/@timestamp)[1]', 'DateTime2') AS Timestamp,  
            T2.EventData.query('.').query(  
                '(/event/data/value/deadlock)[1]')     AS deadlock_xml  
        FROM CTE  
            CROSS Apply [target_data_XML].nodes(  
                '/RingBufferTarget/event') AS T2(EventData)  
)  
SELECT * FROM CTE2;  
```

## <a name="see-also"></a>参照

 [Azure SQL データベースでの拡張イベント](/azure/azure-sql/database/xevent-db-diff-from-svr)  
