---
description: fulltext_indexes (Transact-sql)
title: fulltext_indexes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_indexes
- fulltext_indexes_TSQL
- sys.fulltext_indexes_TSQL
- sys.fulltext_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_indexes catalog view
- full-text indexes [SQL Server], properties
ms.assetid: 7fc10fdc-370f-4927-bba0-b76108a7508e
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2b57b7f507e5721647ca44b7f75388fc5ce8de57
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88401658"
---
# <a name="sysfulltext_indexes-transact-sql"></a>fulltext_indexes (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  表形式オブジェクトのフルテキスト インデックスごとに 1 行のデータを保持します。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|このフルテキストインデックスが属しているオブジェクトの ID です。|  
|**unique_index_id**|**int**|フルテキストインデックスを行に関連付けるために使用される、対応する一意の非フルテキストインデックスの ID。|  
|**fulltext_catalog_id**|**int**|フルテキスト インデックスが存在するフルテキスト カタログの ID です。|  
|**is_enabled**|**bit**|1 = フルテキストインデックスが現在有効になっています。|  
|**change_tracking_state**|**char (1)**|変更の追跡の状態。<br /><br /> M = 手動<br /><br /> A = 自動<br /><br /> O = オフ|  
|**change_tracking_state_desc**|**nvarchar(60)**|変更の追跡の状態に関する説明です。<br /><br /> MANUAL<br /><br /> AUTO<br /><br /> OFF|  
|**has_crawl_completed**|**bit**|フルテキスト インデックスが完了した最新のクロール (作成) です。|  
|**crawl_type**|**char (1)**|現在または最近のクロールの種類。<br /><br /> F = フルクロール<br /><br /> I = タイムスタンプに基づく増分クロール<br /><br /> U = 通知に基づく更新クロール<br /><br /> P = フル クロールが一時停止された状態|  
|**crawl_type_desc**|**nvarchar(60)**|現在または最新のクロールの種類に関する説明です。<br /><br /> FULL_CRAWL<br /><br /> INCREMENTAL_CRAWL<br /><br /> UPDATE_CRAWL<br /><br /> PAUSED_FULL_CRAWL|  
|**crawl_start_date**|**datetime**|現在または最新のクロールの開始日付です。<br /><br /> NULL = None。|  
|**crawl_end_date**|**datetime**|現在または最近のクロールの終了。<br /><br /> NULL = None。|  
|**incremental_timestamp**|**binary (8)**|次回の増分クロールに使用するタイムスタンプ値です。<br /><br /> NULL = None。|  
|**stoplist_id**|**int**|このフルテキストインデックスに関連付けられている [ストップリスト](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md) の ID。|  
|**data_space_id**|**int**|このフルテキストインデックスが置かれているファイルグループ。|  
|**property_list_id**|**int**|このフルテキストインデックスに関連付けられている検索プロパティリストの ID。 NULL は、フルテキストインデックスに関連付けられている検索プロパティリストがないことを示します。 この検索プロパティリストの詳細情報を取得するには、 [registered_search_property_lists &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md) カタログビューを使用します。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="examples"></a>例  
 次の例では、`HumanResources.JobCandidate` サンプル データベースの `AdventureWorks2012` テーブルのフルテキスト インデックスを使用します。 この例では、テーブルのオブジェクト ID、検索プロパティリストの ID、およびフルテキストインデックスによって使用されるストップリストのストップリスト ID が返されます。  
  
> [!NOTE]  
>  このフルテキストインデックスを作成するコード例については、「 [transact-sql&#41;&#40;のフルテキストインデックスの作成 ](../../t-sql/statements/create-fulltext-index-transact-sql.md)」の「例」のセクションを参照してください。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT object_id, property_list_id, stoplist_id FROM sys.fulltext_indexes  
    where object_id = object_id('HumanResources.JobCandidate');   
GO  
```  
  
## <a name="see-also"></a>参照  
 [fulltext_index_fragments &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)   
 [fulltext_index_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [fulltext_index_catalog_usages &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)   
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [フルテキスト インデックスの作成と管理](../../relational-databases/search/create-and-manage-full-text-indexes.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
  
