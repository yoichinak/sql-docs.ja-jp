---
description: sys.database_connection_stats (Azure SQL データベース)
title: sys.database_connection_stats
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.database_connection_stats
- database_connection_stats
- database_connection_stats_TSQL
- sys.database_connection_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_connection_stats
- database_connection_stats
ms.assetid: 5c8cece0-63b0-4dee-8db7-6b43d94027ec
author: markingmyname
ms.author: maghan
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 2a3d57bb4ba8c36778d3d4e552d9a69bd285db9e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542594"
---
# <a name="sysdatabase_connection_stats-azure-sql-database"></a>sys.database_connection_stats (Azure SQL データベース)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  データベース接続の [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 成功**connectivity**と失敗の概要を提供する、データベース接続イベントの統計が含まれます。 接続イベントの詳細については、「 [event_log &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md)」の「イベントの種類」を参照してください。  
  
|統計|種類|説明|  
|---------------|----------|-----------------|  
|**database_name**|**sysname**|データベースの名前です。|  
|**start_time**|**datetime2**|集計間隔の開始時刻を示す UTC 日時。 この時刻は常に 5 分の倍数です。 次に例を示します。<br /><br /> ' 2011-09-28 16:00:00 '<br />' 2011-09-28 16:05:00 '<br />' 2011-09-28 16:10:00 '|  
|**end_time**|**datetime2**|集計間隔の終了時刻を示す UTC 日時。 **End_time** は、同じ行の対応する **start_time** よりも常に5分後になります。|  
|**success_count**|**int**|成功した接続の数。|  
|**total_failure_count**|**int**|失敗した接続の合計数。 これは **connection_failure_count**、 **terminated_connection_count**、および **throttled_connection_count**の合計であり、デッドロックイベントは含まれていません。|  
|**connection_failure_count**|**int**|ログインの失敗数。|  
|**terminated_connection_count**|**int**|**_V11 にのみ適用さ [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] れます。_**<br /><br /> 終了した接続の数。|  
|**throttled_connection_count**|**int**|**_V11 にのみ適用さ [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] れます。_**<br /><br /> スロットルされた接続の数。|  
  
## <a name="remarks"></a>解説  
  
### <a name="event-aggregation"></a>イベント集計

 このビューのイベント情報は、5 分未満の間隔で収集および集計されます。 各カウント列は、特定の時間内に特定のデータベースについて発生した特定の接続イベントの回数を表します。  
  
 たとえば、2012 年 2 月 5 日 (UTC) の 11:00 から 11:05 までに、ユーザーがデータベース Database1 への接続に 7 回失敗した場合、この情報はこのビューの単一行に示されます。  
  
|**database_name**|**start_time**|**end_time**|**success_count**|**total_failure_count**|**connection_failure_count**|**terminated_connection_count**|**throttled_connection_count**|  
|------------------------|---------------------|-------------------|------------------------|-------------------------------|------------------------------------|---------------------------------------|--------------------------------------|  
|`Database1`|`2012-02-05 11:00:00`|`2012-02-05 11:05:00`|`0`|`7`|`7`|`0`|`0`|  
  
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
  
- このビューには [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 、発生する可能性があるすべてのデータベースエラーが含まれていません [。 event_log &#40;](../../relational-databases/system-catalog-views/sys-event-log-azure-sql-database.md)のイベントの種類で指定されたものだけが&#41;Azure SQL Database ます。  
  
- データセンター内でコンピューター障害が発生した場合は、 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 少量のデータがイベントテーブルに存在しない可能性があります。  
  
- DoSGuard によって IP アドレスがブロックされている場合は、その IP アドレスからの接続試行イベント情報を収集することができないため、このビューに表示されません。  
  
## <a name="permissions"></a>アクセス許可

 **Master**データベースへのアクセス権限を持つユーザーには、このビューに対する読み取り専用アクセス権があります。  
  
## <a name="example"></a>例

 次の例は、9/25/2011 の正午から 9/28/2011 (UTC) に正午に発生したデータベース接続の概要を返すための、database_connection_stats のクエリを示しています **。** 既定では、クエリの結果は **start_time** (昇順) に並べ替えられます。  
  
```sql
SELECT *  
FROM sys.database_connection_stats
WHERE start_time>='2011-09-25 12:00:00' and end_time<='2011-09-28 12:00:00';  
```  

## <a name="see-also"></a>参照

 [Azure SQL Database との接続に関する一般的な問題のトラブルシューティング](/azure/sql-database/sql-database-troubleshoot-common-connection-issues)  
  
  
