---
description: dm_fts_active_catalogs (Transact-sql)
title: dm_fts_active_catalogs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_active_catalogs_TSQL
- dm_fts_active_catalogs
- dm_fts_active_catalogs_TSQL
- sys.dm_fts_active_catalogs
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_active_catalogs dynamic management view
ms.assetid: 40ab5453-040c-4d2e-bb49-e340cf90c3ee
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4545e37733448d1c26b19567c05463b014482d10
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454930"
---
# <a name="sysdm_fts_active_catalogs-transact-sql"></a>dm_fts_active_catalogs (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  サーバー上でいくつかの作成アクティビティが進行中のフルテキストカタログに関する情報を返します。  
  
> [!NOTE]
>  次の列は、の将来のバージョンで削除される予定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です: is_paused、previous_status、previous_status_description、row_count_in_thousands、状態、status_description、および worker_count。 新しい開発作業ではこれらの列を使用しないようにし、現在これらの列を使用しているアプリケーションの変更を検討してください。  
  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|アクティブなフルテキストカタログを含むデータベースの ID。|  
|**catalog_id**|**int**|アクティブなフルテキストカタログの ID。|  
|**memory_address**|**varbinary (8)**|このフルテキストカタログに関連する作成アクティビティに割り当てられたメモリバッファーのアドレス。|  
|**name**|**nvarchar(128)**|アクティブなフルテキスト カタログの名前。|  
|**is_paused**|**bit**|アクティブなフルテキストカタログの作成が一時停止されているかどうかを示します。|  
|**status**|**int**|フルテキストカタログの現在の状態です。 次のいずれかになります。<br /><br /> 0 = 初期化中<br /><br /> 1 = 準備完了<br /><br /> 2 = 一時停止<br /><br /> 3 = 一時エラー<br /><br /> 4 = 再マウントが必要<br /><br /> 5 = シャットダウン<br /><br /> 6 = バックアップ用に休止<br /><br /> 7 = カタログを使用してバックアップを実行する<br /><br /> 8 = カタログが破損しています|  
|**status_description**|**nvarchar(120)**|アクティブなフルテキスト カタログの現在の状態に関する説明。|  
|**previous_status**|**int**|フルテキストカタログの以前の状態。 次のいずれかになります。<br /><br /> 0 = 初期化中<br /><br /> 1 = 準備完了<br /><br /> 2 = 一時停止<br /><br /> 3 = 一時エラー<br /><br /> 4 = 再マウントが必要<br /><br /> 5 = シャットダウン<br /><br /> 6 = バックアップ用に休止<br /><br /> 7 = カタログを使用してバックアップを実行する<br /><br /> 8 = カタログが破損しています|  
|**previous_status_description**|**nvarchar(120)**|アクティブなフルテキストカタログの以前の状態の説明です。|  
|**worker_count**|**int**|このフルテキストカタログを現在処理しているスレッドの数。|  
|**active_fts_index_count**|**int**|設定されているフルテキストインデックスの数。|  
|**auto_population_count**|**int**|このフルテキストカタログに対して自動作成が進行中のテーブルの数。|  
|**manual_population_count**|**int**|このフルテキストカタログの手動作成が進行中のテーブルの数。|  
|**full_incremental_population_count**|**int**|このフルテキストカタログに対して、完全作成または増分作成が進行中のテーブルの数。|  
|**row_count_in_thousands**|**int**|フルテキストカタログ内のすべてのフルテキストインデックスの推定行数 (1000 単位)。|  
|**is_importing**|**bit**|フルテキストカタログがインポートされているかどうかを示します。<br /><br /> 1 = カタログがインポートされています。<br /><br /> 2 = カタログがインポートされていません。|  
  
## <a name="remarks"></a>解説  
 Is_importing 列はで新しく追加されました [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 。  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
   
## <a name="physical-joins"></a>物理結合  
 ![この動的管理ビューの重要な結合](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-active-catalogs-1.gif "この動的管理ビューの重要な結合")  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|ソース|終了|リレーションシップ|  
|----------|--------|------------------|  
|dm_fts_active_catalogs。 database_id|dm_fts_index_population。 database_id|一対一|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|一対一|  
  
## <a name="examples"></a>例  
 次の例では、現在のデータベースのアクティブなフルテキストカタログに関する情報を返します。  
  
```  
SELECT catalog.name, catalog.is_importing, catalog.auto_population_count,  
  OBJECT_NAME(population.table_id) AS table_name,  
  population.population_type_description, population.is_clustered_index_scan,  
  population.status_description, population.completion_type_description,  
  population.queued_population_type_description, population.start_time,  
  population.range_count   
FROM sys.dm_fts_active_catalogs catalog   
CROSS JOIN sys.dm_fts_index_population population   
WHERE catalog.database_id = population.database_id   
AND catalog.catalog_id = population.catalog_id   
AND catalog.database_id = (SELECT dbid FROM sys.sysdatabases WHERE name = DB_NAME());  
GO  
```  
  
## <a name="see-also"></a>参照  
 
 [Transact-sql&#41;&#40;のフルテキスト検索とセマンティック検索の動的管理ビューおよび関数 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  
