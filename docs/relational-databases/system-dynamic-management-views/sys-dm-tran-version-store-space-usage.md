---
description: sys.dm_tran_version_store_space_usage (Transact-sql)
title: sys.dm_tran_version_store_space_usage (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c36dce670a89883b436421ae26c36d54308f2457
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99132095"
---
# <a name="sysdm_tran_version_store_space_usage-transact-sql"></a>sys.dm_tran_version_store_space_usage (Transact-sql)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

各データベースのバージョンストアレコードで使用される tempdb 内の領域の合計を表示するテーブルを返します。 **sys.dm_tran_version_store_space_usage** は、個々のバージョンストアレコード間を移動せず、データベースごとに tempdb で使用される集計バージョンストア領域を返すため、効率的で実行コストがかかりません。
  
バージョン管理された各レコードは、追跡情報や状態情報と共に、バイナリデータとして格納されます。 データベース テーブル内のレコードと同様、バージョン ストア レコードは 8,192 バイトのページに格納されます。 レコードが 8,192 バイトを超える場合は、2 つのレコードに分割されます。  
  
バージョン付きのレコードはバイナリとして格納されるため、異なるデータベースからの異なる照合順序に関する問題はありません。 **Sys.dm_tran_version_store_space_usage** を使用すると、SQL Server インスタンス内のデータベースのバージョンストアの使用領域に基づいて、tempdb のサイズを監視および計画できます。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|データベースのデータベース ID。|  
|**reserved_page_count**|**bigint**|データベースのバージョンストアレコードの tempdb に予約されているページの合計数。|  
|**reserved_space_kb**|**bigint**|データベースのバージョンストアレコードの tempdb で使用されている合計領域 (kb 単位)。|  
  
## <a name="permissions"></a>アクセス許可  
で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   

## <a name="examples"></a>例  
次のクエリを使用すると、インスタンス内の各データベースのバージョンストアによって、tempdb で消費された領域を調べることができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 
  
```sql  
SELECT 
  DB_NAME(database_id) as 'Database Name',
  reserved_page_count,
  reserved_space_kb 
FROM sys.dm_tran_version_store_space_usage;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Database Name            reserved_page_count reserved_space_kb  
------------------------ -------------------- -----------  
msdb                      0                    0             
AdventureWorks2016        10                   80             
AdventureWorks2016DW      0                    0             
WideWorldImporters        20                   160             
```
 
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
