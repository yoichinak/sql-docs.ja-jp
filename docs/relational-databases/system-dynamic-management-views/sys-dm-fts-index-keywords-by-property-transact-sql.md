---
description: sys.dm_fts_index_keywords_by_property (Transact-SQL)
title: dm_fts_index_keywords_by_property (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_index_keywords_by_property
- dm_fts_index_keywords_by_property_TSQL
- sys.dm_fts_index_keywords_by_property
- sys.dm_fts_index_keywords_by_property_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- search property lists [SQL Server], viewing keywords by property
- full-text search [SQL Server], viewing keywords
- sys.dm_fts_index_keywords_by_property dynamic management view
ms.assetid: fa41e052-a79a-4194-9b1a-2885f7828500
author: pmasl
ms.author: pelopes
ms.openlocfilehash: bcb2864644941786244b19f0a3aa08dc25f7dca6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447576"
---
# <a name="sysdm_fts_index_keywords_by_property-transact-sql"></a>sys.dm_fts_index_keywords_by_property (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたテーブルのフルテキストインデックスに含まれるプロパティ関連のすべてのコンテンツを返します。 これには、そのフルテキストインデックスに関連付けられている検索プロパティリストによって登録されたすべてのプロパティに属するすべてのデータが含まれます。  
  
 IFilters は、インデックス時にによって出力された登録済みプロパティと、各インデックス付きドキュメントのすべてのプロパティの正確なコンテンツを確認できる動的管理関数です dm_fts_index_keywords_by_property。  
  
 **すべてのドキュメント レベルのコンテンツ (プロパティに関連するコンテンツを含む) を表示するには**  
  
-   [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
 **上位レベルのフルテキスト インデックス情報を表示するには**  
  
-   [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
> [!NOTE]  
>  検索プロパティリストの詳細については、「検索 [プロパティリストを使用したドキュメントプロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.dm_fts_index_keywords_by_property  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>引数  
 db_id ('*database_name*')  
 [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md)関数の呼び出し。 この関数は、データベース名を受け取り、データベース ID を返します。この ID は、指定されたデータベースを検索するために使用 dm_fts_index_keywords_by_property ます。 場合 *database_name* は省略すると、現在のデータベース ID が返されます。  
  
 object_id ('*table_name*')  
 [OBJECT_ID ()](../../t-sql/functions/object-id-transact-sql.md)関数の呼び出し。 この関数は、テーブル名を受け取り、検査するフルテキストインデックスが含まれているテーブルのテーブル ID を返します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列|データ型|説明|  
|------------|---------------|-----------------|  
|キーワード (keyword)|**nvarchar (4000)**|フルテキスト インデックスに格納されているキーワードの 16 進数表記です。<br /><br /> 注: 0 Xff は、ファイルまたはデータセットの末尾を示す特殊文字を表します。|  
|display_term|**nvarchar (4000)**|キーワードの人間が判読できる形式。 この形式は、フルテキストインデックスに格納されている内部形式から派生します。<br /><br /> 注: 0 Xff は、ファイルまたはデータセットの末尾を示す特殊文字を表します。|  
|column_id|**int**|現在のキーワードがフルテキストインデックスを作成した列の ID。|  
|document_id|**int**|現在の用語のフルテキストインデックスが作成されたドキュメントまたは行の ID。 この ID は、そのドキュメントまたは行のフルテキストキー値に対応します。|  
|property_id|**int**|OBJECT_ID ('*table_name*') パラメーターで指定したテーブルのフルテキストインデックス内の検索プロパティの内部プロパティ ID。<br /><br /> 特定のプロパティが検索プロパティ リストに追加されると、Full-Text Engine はプロパティを登録し、このプロパティ リストに固有の内部プロパティ ID を、そのプロパティに割り当てます。 内部プロパティ ID (整数) は、特定の検索プロパティリストに対して一意です。 特定のプロパティを複数の検索プロパティ リストに登録した場合、検索プロパティ リストごとに異なる内部プロパティ ID が割り当てられる可能性があります。<br /><br /> 注: 内部プロパティ ID は、プロパティを検索プロパティリストに追加するときに指定されるプロパティ整数識別子とは異なります。 詳細については、「 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)」を参照してください。<br /><br /> Property_id とプロパティ名の間の関連付けを表示するには、次のようにします。<br />                    [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)|  
  
## <a name="remarks"></a>解説  
 この動的管理ビューでは、次のような質問に答えることができます。  
  
-   指定された DocID の特定のプロパティにどのようなコンテンツが格納されますか。  
  
-   特定のプロパティが、インデックス付きの文書間でどの程度一般的か。  
  
-   指定されたプロパティを実際に含むドキュメント これは、特定の検索プロパティへのクエリによって、見つかると想定していたドキュメントが返されなかった場合に役立ちます。  
  
 フルテキスト キー列が整数データ型 (推奨されるデータ型) の場合、document_id はベース テーブルのフルテキスト キー値に直接マップされます。  
  
 一方、フルテキスト キー列で整数データ型以外のデータ型が使用されている場合は、document_id はベース テーブルのフルテキスト キーを表しません。 この場合、dm_fts_index_keywords_by_property によって返されるベーステーブル内の行を識別するには、 [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)によって返された結果と共にこのビューを結合する必要があります。 結合する前に、ストアドプロシージャの出力を一時テーブルに格納する必要があります。 その後、dm_fts_index_keywords_by_property の document_id 列を、このストアドプロシージャによって返される DocId 列に結合できます。 **Timestamp**列はによって自動生成されるため、挿入時に値を受け取ることはできません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 そのため、 **timestamp** 列は、 **varbinary (8)** 列に変換する必要があります。 次の例では、これらの手順を示します。 この例では、 *table_id* はテーブルの id、 *database_name* はデータベースの名前、 *table_name* はテーブルの名前です。  
  
```  
USE database_name;  
GO  
CREATE TABLE #MyTempTable   
   (  
      docid INT PRIMARY KEY ,  
      [key] INT NOT NULL  
   );  
DECLARE @db_id int = db_id(N'database_name');  
DECLARE @table_id int = OBJECT_ID(N'table_name');  
INSERT INTO #MyTempTable EXEC sp_fulltext_keymappings @table_id;  
SELECT * FROM sys.dm_fts_index_keywords_by_property   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>アクセス許可  
 フルテキスト インデックスに含まれる列に対する SELECT 権限と、CREATE FULL TEXT CATALOG 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、`Author` サンプル データベースの `Production.Document` テーブルのフルテキスト インデックスにある `AdventureWorks` プロパティからキーワードが返されます。 この例では、 `KWBPOP` **dm_fts_index_keywords_by_property**によって返されるテーブルの別名を使用します。 この例では、内部結合を使用して、 [registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md) と [sys. fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)の列を結合します。  
  
```  
-- Once the full-text index is configured to support property searching  
-- on the Author property, return any keywords indexed for this property.  
USE AdventureWorks2012;  
GO   
SELECT KWBPOP.* FROM   
   sys.dm_fts_index_keywords_by_property( DB_ID(),   
   object_id('Production.Document') ) AS KWBPOP  
   INNER JOIN  
      sys.registered_search_properties AS RSP ON(   
         (KWBPOP.property_id = RSP.property_id)   
         AND (RSP.property_name = 'Author') )  
   INNER JOIN  
      sys.fulltext_indexes AS FTI ON(   
         (FTI.[object_id] = object_id('Production.Document'))   
         AND (RSP.property_list_id = FTI.property_list_id) );  
GO  
```  
  
## <a name="see-also"></a>参照  
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)   
 [フルテキストインデックスのパフォーマンスの向上](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [sp_fulltext_keymappings &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [dm_fts_index_keywords_by_document &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)   
 [dm_fts_index_keywords &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [registered_search_properties &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [registered_search_property_lists &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [検索プロパティ リストを使用したドキュメント プロパティの検索](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
