---
description: sys.dm_db_file_space_usage (Transact-SQL)
title: dm_db_file_space_usage (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_file_space_usage
- sys.dm_db_file_space_usage_TSQL
- sys.dm_db_file_space_usage
- dm_db_file_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_file_space_usage dynamic management view
ms.assetid: 148a5276-a8d5-49d2-8146-3c63d24c2144
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a56c3a17ec09bd45ef9d9efd632d58b190268943
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534790"
---
# <a name="sysdm_db_file_space_usage-transact-sql"></a>sys.dm_db_file_space_usage (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  データベース内の各データファイルの領域使用状況に関する情報を返します。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_db_file_space_usage**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|データベース ID。|  
|file_id|**smallint**|ファイル ID。<br /><br /> file_id は、 [sys. dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) の file_id と [sys.sysファイル](../../relational-databases/system-compatibility-views/sys-sysfiles-transact-sql.md)の fileid にマップされます。|  
|filegroup_id|**smallint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> ファイル グループ ID。|  
|total_page_count|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> データファイル内の総ページ数。|  
|allocated_extent_page_count|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> データファイル内の割り当てられたエクステント内のページの合計数。|  
|unallocated_extent_page_count|**bigint**|データファイル内の未割り当てエクステント内のページの合計数。<br /><br /> 割り当てられたエクステントの未使用ページは含まれません。|  
|version_store_reserved_page_count|**bigint**|バージョンストアに割り当てられた単一エクステント内のページの合計数。 バージョン ストア ページは、混合エクステントからは割り当てられません。<br /><br /> IAM ページは、常に混合エクステントから割り当てられるため、含まれていません。 PFS ページは、一定の範囲から割り当てられている場合に含まれます。<br /><br /> 詳しくは、「[sys.dm_tran_version_store &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md)」をご覧ください。|  
|user_object_reserved_page_count|**bigint**|データベース内のユーザーオブジェクトに対して、単一エクステントから割り当てられたページの合計数。 割り当て済みのエクステントの未使用ページは、この数に含まれません。<br /><br /> IAM ページは、常に混合エクステントから割り当てられるため、含まれていません。 PFS ページは、一定の範囲から割り当てられている場合に含まれます。<br /><br /> [Allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)カタログビューの total_pages 列を使用して、ユーザーオブジェクト内の各アロケーションユニットの予約済みページ数を返すことができます。 ただし、total_pages 列には IAM ページが含まれていることに注意してください。|  
|internal_object_reserved_page_count|**bigint**|ファイル内の内部オブジェクトに対して割り当てられる単一エクステント内の総ページ数。 割り当て済みのエクステントの未使用ページは、この数に含まれません。<br /><br /> IAM ページは、常に混合エクステントから割り当てられるため、含まれていません。 PFS ページは、一定の範囲から割り当てられている場合に含まれます。<br /><br /> 各内部オブジェクトのページ数を返すカタログビューまたは動的管理オブジェクトはありません。|  
|mixed_extent_page_count|**bigint**|ファイル内の割り当てられた混合エクステントに割り当てられたページと未割り当てページの合計数。 混合エクステントには、異なるオブジェクトに割り当てられたページが含まれます。 この数には、ファイル内のすべての IAM ページが含まれます。|
|modified_extent_page_count|**bigint**|**適用対象**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 以降。<br /><br />前回のデータベースの完全バックアップ以降に、ファイルの割り当てられたエクステントで変更されたページの総数。 差分バックアップが必要かどうかを判断するために、変更されたページ数を使用して、前回の完全バックアップ以降にデータベースの差分変更の量を追跡できます。|
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
|distribution_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 分布に関連付けられている一意の数値 id です。|  
  
## <a name="remarks"></a>解説  
 ページ数は常にエクステント レベルのものです。 したがって、ページ数の値は常に 8 の倍数になります。 グローバルアロケーションマップ (GAM) と共有グローバルアロケーションマップ (SGAM) のアロケーションページを含むエクステントには、単一エクステントが割り当てられます。 これらは、前に説明したページ数には含まれていません。 ページとエクステントの詳細については、「 [ページとエクステントのアーキテクチャガイド](../../relational-databases/pages-and-extents-architecture-guide.md)」を参照してください。 
  
 現在のバージョンストアの内容は、 [dm_tran_version_store](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md)にあります。 バージョンストアページは、グローバルリソースであるため、セッションおよびタスクレベルではなく、ファイルレベルで追跡されます。 セッションでバージョンを生成することもできますが、セッションが終了するときバージョンを削除することはできません。 バージョンストアのクリーンアップでは、特定のバージョンへのアクセスを必要とする実行時間が最も長いトランザクションを考慮する必要があります。 バージョンストアのクリーンアップに関連する実行時間が最も長いトランザクションを検出するには、 [dm_tran_active_snapshot_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md)の elapsed_time_seconds 列を表示します。  
  
 mixed_extent_page_count 列で変更が頻繁に行われる場合は、SGAM ページの使用頻度が高いことが考えられます。 この場合、PAGELATCH_UP 待機の数が多くなっていることがあります。またこの待機では、待機リソースが SGAM ページになっています。 詳細については、「 [sys. dm_os_waiting_tasks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-waiting-tasks-transact-sql.md)」、「 [dm_os_wait_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)」、および「 [dm_os_latch_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)」を参照してください。  
  
## <a name="user-objects"></a>ユーザーオブジェクト  
 ユーザーオブジェクトページカウンターには、次のオブジェクトが含まれています。  
  
-   ユーザー定義テーブルとインデックス  
  
-   システムテーブルとインデックス  
  
-   グローバル一時テーブルとインデックス  
  
-   ローカル一時テーブルとインデックス  
  
-   テーブル変数  
  
-   テーブル値関数で返されるテーブル  
  
## <a name="internal-objects"></a>内部オブジェクト  
 内部オブジェクトは tempdb にのみ存在します。 内部オブジェクトページカウンターには、次のオブジェクトが含まれています。  
  
-   カーソルまたはスプール操作の作業テーブルと、一時的なラージオブジェクト (LOB) ストレージ  
  
-   ハッシュ結合などの操作用の作業ファイル  
  
-   並べ替え実行結果  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|From|終了|リレーションシップ|  
|----------|--------|------------------|  
|sys.dm_db_file_space_usage.database_id、file_id|sys.dm_io_virtual_file_stats.database_id、file_id|一対一|  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="examples"></a>例  
  
### <a name="determing-the-amount-of-free-space-in-tempdb"></a>tempdb の使用可能な空き領域の確認  
 次のクエリは、 **tempdb**内のすべてのデータファイルで使用可能な空きページと合計空き領域 (mb) の合計数を返します。  
  
```sql
USE tempdb;  
GO  
SELECT SUM(unallocated_extent_page_count) AS [free pages],   
(SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]  
FROM sys.dm_db_file_space_usage;  
```  

### <a name="determining-the-amount-of-space-used-by-user-objects"></a>ユーザーオブジェクトが使用する領域の量を決定する  
 次のクエリを実行すると、tempdb のユーザー オブジェクトにより使用されるページ数の合計と領域の合計 (MB 単位) が返されます。  
  
```sql  
USE tempdb;  
GO  
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],  
(SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]  
FROM sys.dm_db_file_space_usage;
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;データベース関連の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [dm_db_task_space_usage &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
