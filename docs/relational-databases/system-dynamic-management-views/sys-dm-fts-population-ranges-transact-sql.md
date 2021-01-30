---
description: sys.dm_fts_population_ranges (Transact-sql)
title: sys.dm_fts_population_ranges (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.dm_fts_population_ranges
- sys.dm_fts_population_ranges_TSQL
- dm_fts_population_ranges_TSQL
- dm_fts_population_ranges
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_population_ranges dynamic management view
ms.assetid: 58d8564b-9c43-4965-a31c-2893890334ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 31465b18c9395a961a08a607648424b62c840c6a
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99106423"
---
# <a name="sysdm_fts_population_ranges-transact-sql"></a>sys.dm_fts_population_ranges (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在実行中のフルテキストインデックスの作成に関連する特定の範囲に関する情報を返します。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**memory_address**|**varbinary (8)**|フルテキストインデックスの作成のこの部分範囲に関連するアクティビティに割り当てられたメモリバッファーのアドレス。|  
|**parent_memory_address**|**varbinary (8)**|フルテキスト インデックス設定に関連するすべての範囲の親オブジェクトを表すメモリ バッファーのアドレス。|  
|**is_retry**|**bit**|値が1の場合、このサブ範囲はエラーが発生した行の再試行を行います。|  
|**session_id**|**smallint**|このタスクを現在処理しているセッションの ID。|  
|**processed_row_count**|**int**|この範囲によって処理された行の数。 転送の進行状況は保持され、すべてのバッチコミットではなく、5分ごとにカウントされます。|  
|**error_count**|**int**|対象となる範囲でエラーが発生した行の数。 転送の進行状況は保持され、すべてのバッチコミットではなく、5分ごとにカウントされます。|  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
SQL Database Basic、S0、S1 のサービス目標、およびエラスティックプール内のデータベースについて `Server admin` は、または `Azure Active Directory admin` アカウントが必要です。 その他のすべての SQL Database サービスの目的で `VIEW DATABASE STATE` は、データベースで権限が必要になります。   
 
## <a name="physical-joins"></a>物理結合  
 ![この動的管理ビューの重要な結合](../../relational-databases/system-dynamic-management-views/media/join-dm-fts-population-ranges-1.gif "この動的管理ビューの重要な結合")  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|差出人|終了|リレーションシップ|  
|----------|--------|------------------|  
|dm_fts_population_ranges dm_fts_population_ranges.parent_memory_address|dm_fts_index_population.memory_address|多対一|  
  
## <a name="see-also"></a>参照  
  [Transact-sql&#41;&#40;のフルテキスト検索とセマンティック検索の動的管理ビューおよび関数 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)  
  
  

