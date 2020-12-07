---
description: dm_fts_index_population (Transact-sql)
title: dm_fts_index_population (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_population
- dm_fts_index_population
- sys.dm_fts_index_population_TSQL
- dm_fts_index_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_population dynamic management view
ms.assetid: 82d1c102-efcc-4b60-9a5e-3eee299bcb2b
author: pmasl
ms.author: pelopes
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1fd871a3f0de84d5a6a36eff7262f71062ace3a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474959"
---
# <a name="sysdm_fts_index_population-transact-sql"></a>dm_fts_index_population (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で現在実行中の、フルテキスト インデックス作成およびセマンティック キー フレーズ作成に関する情報を返します。  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|設定されているフルテキストインデックスを含むデータベースの ID。|  
|**catalog_id**|**int**|フルテキスト インデックスを含む、フルテキスト カタログの ID。|  
|**table_id**|**int**|フルテキストインデックスが設定されるテーブルの ID。|  
|**memory_address**|**varbinary (8)**|アクティブな母集団を表すために使用される内部データ構造のメモリアドレス。|  
|**population_type**|**int**|設定の種類。 次のいずれかになります。<br /><br /> 1 = 完全作成<br /><br /> 2 = タイムスタンプに基づく増分作成<br /><br /> 3 = 追跡した変更の手動更新<br /><br /> 4 = 追跡された変更のバックグラウンド更新。|  
|**population_type_description**|**nvarchar(120)**|母集団の種類の説明。|  
|**is_clustered_index_scan**|**bit**|設定では、クラスター化されたインデックスでのスキャンが行われるかどうかを示します。|  
|**range_count**|**int**|この母集団が並列化されたサブ範囲の数。|  
|**completed_range_count**|**int**|処理が完了した範囲の数。|  
|**outstanding_batch_count**|**int**|この母集団の未処理のバッチの現在の数。 詳細については、「 [sys. dm_fts_outstanding_batches &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)」を参照してください。|  
|**status**|**int**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> 設定の状態。 注: 状態には一時的なものもあります。 次のいずれかになります。<br /><br /> 3 = 開始<br /><br /> 5 = 正常に処理中<br /><br /> 7 = 処理を停止しました<br /><br /> たとえば、この状態は、自動マージの進行中に発生します。<br /><br /> 11 = 作成が中止されました<br /><br /> 12 = セマンティック類似性抽出の処理|  
|**status_description**|**nvarchar(120)**|作成の状態の説明。|  
|**completion_type**|**int**|この作成が完了した方法の状態。|  
|**completion_type_description**|**nvarchar(120)**|入力候補の種類の説明。|  
|**worker_count**|**int**|この値は常に0です。|  
|**queued_population_type**|**int**|現在のインデックス設定の次に設定が行われる場合、追跡した変更に基づく設定の種類。|  
|**queued_population_type_description**|**nvarchar(120)**|実行する母集団の説明です (存在する場合)。 たとえば、CHANGE TRACKING = AUTO が設定されており、最初の完全設定が進行中の場合、この列には "Auto population" と表示されます。|  
|**start_time**|**datetime**|作成が開始された時刻。|  
|**incremental_timestamp**|**timestamp**|完全作成の開始タイムスタンプを表します。 その他のすべての母集団の種類では、この値は作成の進行状況を表す最後にコミットされたチェックポイントです。|  
  
## <a name="remarks"></a>解説  
 フルテキストインデックス作成に加えて統計的セマンティックインデックス作成が有効になっている場合、キーフレーズのセマンティック抽出と作成、およびドキュメントの類似性データの抽出は、フルテキストインデックス作成と同時に行われます。 ドキュメントの類似性のインデックスの作成は、後で2番目のフェーズで行われます。 詳細については、「 [セマンティック検索の管理と監視](../../relational-databases/search/manage-and-monitor-semantic-search.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="physical-joins"></a>物理結合  
 ![この動的管理ビューの重要な結合](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-index-population-1.gif "この動的管理ビューの重要な結合")  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|ソース|終了|リレーションシップ|  
|----------|--------|------------------|  
|dm_fts_active_catalogs。 database_id|dm_fts_index_population。 database_id|一対一|  
|dm_fts_active_catalogs.catalog_id|dm_fts_index_population.catalog_id|一対一|  
|dm_fts_population_ranges。 parent_memory_address|dm_fts_index_population.memory_address|多対一|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;のフルテキスト検索とセマンティック検索の動的管理ビューおよび関数 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

