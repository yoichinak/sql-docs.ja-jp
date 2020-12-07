---
description: sys.dm_fts_index_keywords_by_document (Transact-SQL)
title: dm_fts_index_keywords_by_document (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_by_document_TSQL
- dm_fts_index_keywords_by_document_TSQL
- sys.dm_fts_index_keywords_by_document
- dm_fts_index_keywords_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- sys.dm_fts_index_keywords_by_document dynamic management function
- full-text search [SQL Server], viewing keywords
ms.assetid: 793b978b-c8a1-428c-90c2-a3e49d81b5c9
author: pmasl
ms.author: pelopes
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d9526c20757ca8f63c468f88c56e26de7ad2b1a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481969"
---
# <a name="sysdm_fts_index_keywords_by_document-transact-sql"></a>sys.dm_fts_index_keywords_by_document (Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  指定したテーブルに関連付けられているフルテキストインデックスのドキュメントレベルのコンテンツに関する情報を返します。  
  
 sys.dm_fts_index_keywords_by_document は動的管理関数です。  
  
 **上位レベルのフルテキスト インデックス情報を表示するには**  
  
-   [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
 **ドキュメントプロパティに関連するプロパティレベルのコンテンツに関する情報を表示するには**  
  
-   [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.dm_fts_index_keywords_by_document  
(   
    DB_ID('database_name'),     OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>引数  
 db_id ('*database_name*')  
 [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md)関数の呼び出し。 この関数は、データベース名を受け取り、データベース ID を返します。sys.dm_fts_index_keywords_by_document はこの ID を使用して指定されたデータベースを検索します。 場合 *database_name* は省略すると、現在のデータベース ID が返されます。  
  
 object_id ('*table_name*')  
 [OBJECT_ID ()](../../t-sql/functions/object-id-transact-sql.md)関数の呼び出し。 この関数は、テーブル名を受け取り、検査するフルテキストインデックスが含まれているテーブルのテーブル ID を返します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列|データ型|説明|  
|------------|---------------|-----------------|  
|キーワード (keyword)|**nvarchar (4000)**|フルテキスト インデックスに格納されているキーワードの 16 進数表記です。<br /><br /> 注: 0 Xff は、ファイルまたはデータセットの末尾を示す特殊文字を表します。|  
|display_term|**nvarchar (4000)**|キーワードの人間が判読できる形式。 この形式は、フルテキストインデックスに格納されている内部形式から派生します。<br /><br /> 注: 0 Xff は、ファイルまたはデータセットの末尾を示す特殊文字を表します。|  
|column_id|**int**|現在のキーワードがフルテキストインデックスを作成した列の ID。|  
|document_id|**int**|現在の用語のフルテキストインデックスが作成されたドキュメントまたは行の ID。 この ID は、そのドキュメントまたは行のフルテキストキー値に対応します。|  
|occurrence_count|**int**|**Document_id**によって示されるドキュメントまたは行の現在のキーワードが出現する回数。 '*Search_property_name*' が指定されている場合、occurrence_count は、ドキュメントまたは行内の指定された検索プロパティにおける現在のキーワードの出現回数のみを表示します。|  
  
## <a name="remarks"></a>解説  
 sys.dm_fts_index_keywords_by_document から返される情報は、特に次の項目を確認するのに役立ちます。  
  
-   フルテキストインデックスに含まれているキーワードの合計数。  
  
-   キーワードが特定のドキュメントまたは行の一部であるかどうか。  
  
-   フルテキストインデックス全体にキーワードが出現する回数それです：  
  
     ([SUM](../../t-sql/functions/sum-transact-sql.md)(**occurrence_count**) WHERE**キーワード** =*keyword_value* )  
  
-   特定のドキュメントまたは行にキーワードが出現する回数。  
  
-   特定のドキュメントまたは行に含まれているキーワードの数。  
  
 また、sys.dm_fts_index_keywords_by_document が提供する情報を使用して、特定のドキュメントまたは行に属しているすべてのキーワードを取得することもできます。  
  
 フルテキスト キー列が整数データ型 (推奨されるデータ型) の場合、document_id はベース テーブルのフルテキスト キー値に直接マップされます。  
  
 一方、フルテキスト キー列で整数データ型以外のデータ型が使用されている場合は、document_id はベース テーブルのフルテキスト キーを表しません。 この場合、dm_fts_index_keywords_by_document によって返されるベーステーブル内の行を識別するには、 [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)によって返された結果と共にこのビューを結合する必要があります。 結合する前に、ストアドプロシージャの出力を一時テーブルに格納する必要があります。 その後、dm_fts_index_keywords_by_document の document_id 列と、このストアド プロシージャから返される DocId 列を結合します。 **Timestamp**列はによって自動生成されるため、挿入時に値を受け取ることはできません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 そのため、 **timestamp** 列は、 **varbinary (8)** 列に変換する必要があります。 次の例では、これらの手順を示します。 この例では、 *table_id* はテーブルの id、 *database_name* はデータベースの名前、 *table_name* はテーブルの名前です。  
  
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
SELECT * FROM sys.dm_fts_index_keywords_by_document   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>アクセス許可  
 フルテキスト インデックスに含まれる列に対する SELECT 権限と、CREATE FULL TEXT CATALOG 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-displaying-full-text-index-content-at-the-document-level"></a>A. ドキュメント レベルでフルテキスト インデックス コンテンツを表示する  
 次の例では、サンプルデータベースのテーブルにあるドキュメントレベルのフルテキストインデックスの内容を表示し `HumanResources.JobCandidate` `AdventureWorks2012` ます。  
  
> [!NOTE]  
>  このインデックスを作成するには、「 `HumanResources.JobCandidate` [CREATE フルテキストインデックス &#40;transact-sql&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)」の表に示されている例を実行します。  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_by_document(db_id('AdventureWorks'),   
object_id('HumanResources.JobCandidate'));  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のフルテキスト検索とセマンティック検索の動的管理ビューおよび関数 ](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)   
 [dm_fts_index_keywords &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [dm_fts_index_keywords_by_property &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [sp_fulltext_keymappings &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [フルテキスト インデックスのパフォーマンスの向上](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)  
  
  
