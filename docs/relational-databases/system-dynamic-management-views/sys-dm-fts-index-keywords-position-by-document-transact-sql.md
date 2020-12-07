---
description: dm_fts_index_keywords_position_by_document (Transact-sql)
title: dm_fts_index_keywords_position_by_document (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document
- sys.dm_fts_index_keywords_position_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords_position_by_document dynamic management view
ms.assetid: 0d70184f-baa2-411b-a32d-a4c5af890edd
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 0b14ccbe7643ed56e18dc79b2a72e27867d63454
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474958"
---
# <a name="sysdm_fts_index_keywords_position_by_document-transact-sql"></a>dm_fts_index_keywords_position_by_document (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  インデックス付きドキュメント内のキーワード位置情報を返します。  
  
## <a name="syntax"></a>構文  
  
```  
sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>引数  
 db_id ('*database_name*')  
 [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md)関数の呼び出し。 この関数は、データベース名を受け取り、データベース ID を返します。この ID は、指定されたデータベースを検索するために使用 dm_fts_index_keywords_position_by_document ます。  
  
 object_id ('*table_name*')  
 [OBJECT_ID ()](../../t-sql/functions/object-id-transact-sql.md)関数の呼び出し。 この関数は、テーブル名を受け取り、検査するフルテキストインデックスが含まれているテーブルのテーブル ID を返します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列|データ型|説明|  
|------------|---------------|-----------------|  
|キーワード (keyword)|**varbinary (128)**|キーワードを表すバイナリ文字列。|  
|display_term|**nvarchar (4000)**|キーワードの人間が判読できる形式。 この形式は、フルテキストインデックスに格納されている内部形式から派生します。|  
|column_id|**int**|現在のキーワードがフルテキストインデックスを作成した列の ID。|  
|document_id|**bigint**|現在の用語のフルテキストインデックスが作成されたドキュメントまたは行の ID。 この ID は、そのドキュメントまたは行のフルテキストキー値に対応します。|  
|position|**int**|ドキュメント内のキーワードの位置。|  
  
## <a name="remarks"></a>解説  
 DMV を使用して、インデックス付きドキュメント内のインデックス付けされた単語の場所を特定します。 この DMV を使用すると、 **dm_fts_index_keywords_by_document システム** がフルテキストインデックスに含まれていることを示す場合に問題のトラブルシューティングを行うことができますが、これらの単語を使用してクエリを実行すると、ドキュメントは返されません。  
  
## <a name="permissions"></a>アクセス許可  
 フルテキスト インデックスに含まれる列に対する SELECT 権限と、CREATE FULL TEXT CATALOG 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、サンプルデータベースのテーブルのフルテキストインデックスからキーワードを返し `Production.Document` `AdventureWorks` ます。  
  
```  
USE AdventureWorks2012;  
GO   
  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
);   
GO  
```  
  
 次のクエリ例のように、他の columns_id に述語を追加して、場所をさらに分離することができます。  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
)  
WHERE document_id = 7 AND display_term = 'performance';  
```  
  
## <a name="see-also"></a>参照  
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)   
 [フルテキストインデックスのパフォーマンスの向上](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [フルテキスト検索およびセマンティック検索関数 &#40;Transact-sql&#41;](../../relational-databases/system-functions/full-text-search-and-semantic-search-functions-transact-sql.md)   
 [Transact-sql&#41;&#40;のフルテキスト検索とセマンティック検索の動的管理ビューおよび関数 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Transact-sql&#41;&#40;のフルテキスト検索およびセマンティック検索ストアドプロシージャ ](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [検索プロパティリストを使用したドキュメントプロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
