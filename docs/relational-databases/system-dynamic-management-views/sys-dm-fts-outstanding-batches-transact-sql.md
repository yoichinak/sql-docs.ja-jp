---
description: dm_fts_outstanding_batches (Transact-sql)
title: dm_fts_outstanding_batches (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_outstanding_batches
- dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches
dev_langs:
- TSQL
helpviewer_keywords:
- troubleshooting [SQL Server], full-text search
- sys.dm_fts_outstanding_batches dynamic management view
ms.assetid: c4d697ed-c906-4c28-b137-036a25e13c84
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 677a1b597ed9c759b4267d8f4fcd4c9a4263df23
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419736"
---
# <a name="sysdm_fts_outstanding_batches-transact-sql"></a>dm_fts_outstanding_batches (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  各フルテキストインデックスバッチに関する情報を返します。  
  
  |列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**int**|データベースの ID|  
|catalog_id|**int**|フルテキストカタログの ID|  
|table_id|**int**|フルテキスト インデックスを含むテーブル ID の ID。|  
|batch_id|**int**|バッチ ID|  
|memory_address|**varbinary (8)**|バッチ オブジェクトのメモリ アドレス。|  
|crawl_memory_address|**varbinary (8)**|クロールオブジェクトのメモリアドレス (親オブジェクト)|  
|memregion_memory_address|**varbinary (8)**|フィルターデーモンホストの送信共有メモリのメモリ領域のメモリアドレス (fdhost.exe)|  
|hr_batch|**int**|バッチの最新のエラーコード|  
|is_retry_batch|**bit**|これが再試行バッチであるかどうかを示します。<br /><br /> 0 = いいえ<br /><br /> 1 = はい|  
|retry_hints|**int**|バッチに必要な再試行の種類。<br /><br /> 0 = 再試行なし<br /><br /> 1 = マルチスレッドでの再試行<br /><br /> 2 = シングルスレッドの再試行<br /><br /> 3 = シングルスレッドおよびマルチスレッドでの再試行<br /><br /> 5 = マルチスレッドでの最終再試行<br /><br /> 6 = シングルスレッドでの最終再試行<br /><br /> 7 = シングルスレッドおよびマルチスレッドでの最終再試行|  
|retry_hints_description|**nvarchar(120)**|必要な再試行の種類の説明。<br /><br /> 再試行なし<br /><br /> MULTI THREAD RETRY<br /><br /> シングルスレッドの再試行<br /><br /> シングルスレッドとマルチスレッドの再試行<br /><br /> MULTI THREAD FINAL RETRY<br /><br /> シングルスレッドの最終再試行<br /><br /> 単一およびマルチスレッドの最終再試行|  
|doc_failed|**bigint**|バッチ内の失敗したドキュメントの数。|  
|batch_timestamp|**timestamp**|バッチの作成時に取得されたタイムスタンプ値|  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="examples"></a>例  
 次の例では、サーバーインスタンス内の各テーブルに対して現在処理されているバッチの数を調べます。  
  
```  
SELECT database_id, table_id, COUNT(*) AS batch_count FROM sys.dm_fts_outstanding_batches GROUP BY database_id, table_id ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のフルテキスト検索とセマンティック検索の動的管理ビューおよび関数 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)  
  
  
