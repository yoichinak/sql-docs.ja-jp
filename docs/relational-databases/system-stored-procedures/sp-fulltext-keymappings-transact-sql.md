---
description: sp_fulltext_keymappings (Transact-SQL)
title: sp_fulltext_keymappings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_keymappings_TSQL
- sp_fulltext_keymappings
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], key column
- sp_fulltext_keymappings
- full-text indexes [SQL Server], troubleshooting
ms.assetid: 2818fa42-072d-4664-a2f7-7ec363b51d81
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cfac86a5cb8000203873f2434212bf2b50749a6d
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810098"
---
# <a name="sp_fulltext_keymappings-transact-sql"></a>sp_fulltext_keymappings (Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  ドキュメント識別子 (DocIds) とフルテキストキー値の間のマッピングを返します。 DocId 列には、フルテキストインデックスが作成されたテーブルの特定のフルテキストキー値にマップされる **bigint** 整数の値が格納されます。 検索条件に一致する DocId 値は、Full-Text Engine からデータベース エンジンに渡され、そこでクエリ対象のベース テーブルのフルテキスト キー値にマップされます。 フルテキストキー列は、テーブルの1つの列に必要な一意のインデックスです。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_fulltext_keymappings { table_id | table_id, docid | table_id, NULL, key }  
```  
  
#### <a name="parameters"></a>パラメーター  
 *table_id*  
 フルテキスト インデックスが設定されたテーブルのオブジェクト ID。 無効な *table_id*を指定すると、エラーが返されます。 テーブルのオブジェクト ID を取得する方法の詳細については、「 [OBJECT_ID &#40;transact-sql&#41;](../../t-sql/functions/object-id-transact-sql.md)」を参照してください。  
  
 *docid*  
 キー値に対応する内部ドキュメント識別子 (DocId)。 *docid* 値が無効な場合、結果は返されません。  
  
 *key*  
 指定したテーブルからのフルテキスト キー値。 *key* 値が無効な場合、結果は返されません。 フルテキストキー値の詳細については、「 [フルテキストインデックスの管理](../search/create-and-manage-full-text-indexes.md)」を参照してください。  
  
> [!IMPORTANT]  
>  1 つ、2 つ、または 3 つのパラメーターを使用する方法の詳細については、後の「解説」を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 [なし] :  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|DocId|**bigint**|キー値に対応する内部ドキュメント識別子 (DocId) 列。|  
|キー|*|指定したテーブルからのフルテキスト キー値。<br /><br /> マッピング テーブルにフルテキスト キーが存在しない場合は、空の行セットが返されます。|  
  
 <sup>*</sup> キーのデータ型は、ベーステーブルのフルテキストキー列のデータ型と同じです。  
  
## <a name="permissions"></a>アクセス許可  
 この関数はパブリックであり、特別な権限は必要ありません。  
  
## <a name="remarks"></a>注釈  
 次の表に、1 つ、2 つ、または 3 つのパラメーターを使用した場合の効果を示します。  
  
|このパラメーターリスト...|次の結果がある...|  
|--------------------------|----------------------|  
|*table_id*|*Table_id*パラメーターのみで呼び出された場合、sp_fulltext_keymappings は、指定されたベーステーブルからすべてのフルテキストキー (キー) 値と、各キーに対応する DocId を返します。 これには削除保留中のキーが含まれます。<br /><br /> この機能は、さまざまな問題をトラブルシューティングする場合に便利です。 特に、選択したフルテキスト キーが整数データ型でないときに、フルテキスト インデックス コンテンツを確認する場合に役立ちます。 これには、sp_fulltext_keymappings の結果を **sys.dm_fts_index_keywords_by_document**の結果と結合する必要があります。 詳細については、「 [sys.dm_fts_index_keywords_by_document &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)」を参照してください。<br /><br /> ただし、通常は、可能であれば特定のフルテキスト キーまたは DocId を指定するパラメーターを指定して sp_fulltext_keymappings を実行することをお勧めします。 これは、キー マップ全体を返すよりもはるかに効率的です。特に、キー マップ全体を返すとパフォーマンスが大幅に低下する可能性がある、非常に大きなテーブルの場合に有効です。|  
|*table_id*、 *docid*|*Table_id*と*docid*のみが指定されている場合、 *docid*は null 以外で、指定されたテーブル内の有効な docid を指定する必要があります。 この機能は、カスタム フルテキスト キーを、特定のフルテキスト インデックスの DocId に対応するベース テーブルから切り離す場合に役立ちます。|  
|*table_id*、NULL、 *キー*|3つのパラメーターが存在する場合は、2番目のパラメーターを NULL にする必要があります。また、 *キー* を null にすることはできません。また、指定したテーブルから有効なフルテキストキー値を指定します。 この機能は、特定のフルテキスト キーに対応する DocId をベース テーブルから切り離す場合に役立ちます。|  
  
 次のいずれかの条件に該当する場合は、エラーが返されます。  
  
-   無効な *table_id*を指定しています。  
  
-   テーブルにフルテキスト インデックスが設定されていない場合。  
  
-   NULL 以外の値が許可されるパラメーターについて NULL が検出された場合。  
  
## <a name="examples"></a>例  
  
> [!NOTE]  
>  このセクションの例では、 `Production.ProductReview` サンプル データベースの [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] テーブルを使用します。 このインデックスを作成するには、「 `ProductReview` [CREATE フルテキストインデックス &#40;transact-sql&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)」の表に示されている例を実行します。  
  
### <a name="a-obtaining-all-the-key-and-docid-values"></a>A. すべてのキーと DocId 値を取得する  
 次の例では、 [DECLARE](../../t-sql/language-elements/declare-local-variable-transact-sql.md) ステートメントを使用してローカル変数を作成 `@table_id` し、テーブルの ID を `ProductReview` その値として割り当てます。 この例で**sp_fulltext_keymappings**は、 `@table_id` *table_id*パラメーターにを指定して sp_fulltext_keymappings を実行します。  
  
> [!NOTE]  
>  *Table_id*パラメーターのみを指定して**sp_fulltext_keymappings**を使用することは、小さなテーブルに適しています。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id;  
GO  
  
```  
  
 この例では、次のようにテーブルからすべての DocIds とフルテキストキーが返されます。  
  
| TABLE | docid | key |
| ----- | ----- | --- |
|`1`|`1`|`1`|  
|`2`|`2`|`2`|  
|`3`|`3`|`3`|  
|`4`|`4`|`4`|  
  
### <a name="b-obtaining-the-docid-value-for-a-specific-key-value"></a>B. 特定のキー値の DocId 値を取得する  
 次の例では、DECLARE ステートメントを使用してローカル変数 `@table_id`を作成し、 `ProductReview` テーブルの ID をその値として割り当てます。 この例で**sp_fulltext_keymappings**は、 `@table_id` *table_id*パラメーターにを指定し、 *docid*パラメーターに NULL を指定し、*キー*パラメーターに4を指定して sp_fulltext_keymappings を実行します。  
  
> [!NOTE]  
>  小さなテーブルに適した*table_id*指しだけで**sp_fulltext_keymappings**を使用します。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id, NULL, 4;  
GO  
  
```  
  
 この例では、次の結果が返されます。  
  
| TABLE | docid | key |
| ----- | ----- | --- |
|`4`|`4`|`4`|  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のフルテキスト検索およびセマンティック検索ストアドプロシージャ ](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
