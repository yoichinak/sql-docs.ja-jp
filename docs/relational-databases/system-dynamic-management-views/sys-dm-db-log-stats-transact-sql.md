---
description: sys.dm_db_log_stats (Transact-SQL)
title: dm_db_log_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_log_stats_TSQL
- sys.dm_db_log_stats
- sys.dm_db_log_stats_TSQL
- dm_db_log_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_log_stats dynamic management function
ms.assetid: ''
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 98c8b45ccde39b7155443b1ef7fabd994f6b26ab
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550306"
---
# <a name="sysdm_db_log_stats-transact-sql"></a>sys.dm_db_log_stats (Transact-SQL)   
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

概要レベルの属性と、データベースのトランザクションログファイルに関する情報を返します。 この情報は、トランザクションログの正常性の監視と診断に使用します。   
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
 sys.dm_db_log_stats ( database_id )
```  
  
## <a name="arguments"></a>引数  

*database_id* |NULL | **既定**

データベースの ID を示します。 `database_id` が `int`です。 有効な入力値は、データベースの ID 番号、 `NULL` 、または `DEFAULT` です。 既定値は、`NULL` です。 `NULL` と `DEFAULT` は、現在のデータベースのコンテキストでは同等の値です。  
組み込み関数 [DB_ID](../../t-sql/functions/db-id-transact-sql.md) を指定できます。 データベース名を指定せずにを使用する場合は、 `DB_ID` 現在のデータベースの互換性レベルが90以上である必要があります。

  
## <a name="tables-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id    |**int**    |データベース ID |  
|recovery_model |**nvarchar(60)**   |   データベースの復旧モデル。 次の値を指定できます。 <br /> SIMPLE<br /> BULK_LOGGED <br /> FULL |  
|log_min_lsn    |**nvarchar(24)**   |   トランザクションログの現在の開始 [ログシーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 。|  
|log_end_lsn    |**nvarchar(24)**   |   トランザクションログに記録されている最後のログレコードの[ログシーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 。|  
|current_vlf_sequence_number    |**bigint** |   実行時の現在の [仮想ログファイル (列)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) のシーケンス番号。|  
|current_vlf_size_mb    |**float**  |   現在の [仮想ログファイル (値)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) のサイズ (MB 単位)。|   
|total_vlf_count    |**bigint** |   トランザクションログ内の [仮想ログファイル (vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) の合計数。 |  
|total_log_size_mb  |**float**  |   トランザクションログの合計サイズ (MB)。 |  
|active_vlf_count   |**bigint** |   トランザクションログ内のアクティブな [仮想ログファイル (vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) の合計数。|  
|active_log_size_mb |**float**  |   アクティブなトランザクションログの合計サイズ (MB)。|  
|log_truncation_holdup_reason   |**nvarchar(60)**   |   ログの切り捨てホールドアップ理由。 値は、  `log_reuse_wait_desc` の列と同じ `sys.databases` です。  (これらの値の詳細については、「 [トランザクションログ](../../relational-databases/logs/the-transaction-log-sql-server.md)」を参照してください)。 <br />次の値を指定できます。 <br />NOTHING<br />CHECKPOINT<br />LOG_BACKUP<br />ACTIVE_BACKUP_OR_RESTORE<br />ACTIVE_TRANSACTION<br />DATABASE_MIRRORING<br />レプリケーション<br />DATABASE_SNAPSHOT_CREATION<br />LOG_SCAN<br />AVAILABILITY_REPLICA<br />OLDEST_PAGE<br />XTP_CHECKPOINT<br />その他の一時的な |  
|log_backup_time    |**datetime**   |   トランザクションログの最後のバックアップ時刻。|   
|log_backup_lsn |**nvarchar(24)**   |   最後のトランザクションログバックアップ [ログシーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|   
|log_since_last_log_backup_mb   |**float**  |   最後のトランザクションログバックアップ [ログシーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)以降のログサイズ (MB)。|  
|log_checkpoint_lsn |**nvarchar(24)**   |   最後のチェックポイント [ログシーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)。|  
|log_since_last_checkpoint_mb   |**float**  |   最後のチェックポイント [ログシーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)からのログサイズ (MB)。|  
|log_recovery_lsn   |**nvarchar(24)**   |   データベースの復旧 [ログシーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) 。 `log_recovery_lsn`チェックポイント lsn の前にが発生した場合 `log_recovery_lsn` は、最も古いアクティブなトランザクション LSN、それ以外の場合 `log_recovery_lsn` はチェックポイント lsn です。|  
|log_recovery_size_mb   |**float**  |   ログ復旧 [ログシーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch)以降のログサイズ (MB)。|  
|recovery_vlf_count |**bigint** |   フェールオーバーまたはサーバーの再起動があった場合に、回復する [仮想ログファイル (vlf)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) の合計数。 |  


## <a name="remarks"></a>解説
`sys.dm_db_log_stats`セカンダリレプリカとして可用性グループに参加しているデータベースに対して実行する場合は、上記で説明したフィールドのサブセットのみが返されます。  現在、 `database_id` `recovery_model` `log_backup_time` セカンダリデータベースに対して実行すると、、、およびのみが返されます。   

## <a name="permissions"></a>アクセス許可  
データベースの権限が必要です `VIEW DATABASE STATE` 。   
  
## <a name="examples"></a>例  

### <a name="a-determining-databases-in-a-ssnoversion-instance-with-high-number-of-vlfs"></a>A. 多数 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の vlf を持つインスタンス内のデータベースの特定   
次のクエリでは、ログファイルに 100 Vlf を超えるデータベースが返されます。 多数の Vlf が、データベースの起動、復元、および復旧時間に影響を与える可能性があります。

```sql  
SELECT name AS 'Database Name', total_vlf_count AS 'VLF count' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id) 
WHERE total_vlf_count  > 100;
```   

### <a name="b-determining-databases-in-a-ssnoversion-instance-with-transaction-log-backups-older-than-4-hours"></a>B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4 時間を経過したトランザクションログバックアップを使用してインスタンス内のデータベースを特定する   
次のクエリでは、インスタンス内のデータベースの最後のログバックアップ時刻を決定します。

```sql  
SELECT name AS 'Database Name', log_backup_time AS 'last log backup time' 
FROM sys.databases AS s
CROSS APPLY sys.dm_db_log_stats(s.database_id); 
```

## <a name="see-also"></a>参照  
[動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
[Transact-sql&#41;&#40;データベース関連の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)   
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)    
  
