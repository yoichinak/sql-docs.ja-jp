---
description: sp_help_fulltext_columns_cursor (Transact-sql)
title: sp_help_fulltext_columns_cursor (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns_cursor
- sp_help_fulltext_columns_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns_cursor
ms.assetid: 26054e76-53b7-4004-8d48-92ba3435e9d7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 60cc0643d08ca46aef4fc77803e3a277a0b3ab5f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535384"
---
# <a name="sp_help_fulltext_columns_cursor-transact-sql"></a>sp_help_fulltext_columns_cursor (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  カーソルを使用して、フルテキストインデックス作成用に指定された列を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、 [fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) カタログビューを使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_fulltext_columns_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @cursor_return = ] @cursor_variable OUTPUT`**Cursor**型の出力変数を入力します。 結果として得られるカーソルは、読み取り専用のスクロール可能な動的カーソルです。  
  
`[ @table_name = ] 'table_name'` フルテキストインデックス情報を要求する1つまたは2つの要素で構成されるテーブル名を指定します。 *table_name* は **nvarchar (517)** で、既定値は NULL です。 *Table_name*を省略した場合、フルテキストインデックスが作成されたテーブルごとにフルテキストインデックス列の情報が取得されます。  
  
`[ @column_name = ] 'column_name'` フルテキストインデックスメタデータを必要とする列の名前を指定します。 *column_name* は **sysname** で、既定値は NULL です。 *Column_name*を省略した場合、または NULL の場合、 *table_name*のフルテキストインデックス列ごとにフルテキスト列情報が返されます。 *Table_name*も省略した場合、または NULL の場合は、データベース内のすべてのテーブルのフルテキストインデックスが作成されたすべての列に対してフルテキストインデックス列の情報が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または (1) エラー  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|テーブル所有者 これは、テーブルを作成したデータベースユーザーの名前です。|  
|**TABLE_ID**|**int**|テーブルの ID。|  
|**TABLE_NAME**|**sysname**|テーブル名。|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|インデックス作成用に指定されているフルテキストインデックス付きテーブルの列。|  
|**FULLTEXT_COLID**|**int**|フルテキスト インデックスが作成された列の列 ID。|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|フルテキスト インデックスが作成されたテーブル内の列で、フルテキスト インデックス列のドキュメントの種類を指定する列。 この値は、フルテキストインデックスが作成された列が **varbinary (max)** 列または **image** 列の場合にのみ適用されます。|  
|**FULLTEXT_BLOBTP_COLID**|**int**|ドキュメント型列の列 ID。 この値は、フルテキストインデックスが作成された列が **varbinary (max)** 列または **image** 列の場合にのみ適用されます。|  
|**FULLTEXT_LANGUAGE**|**sysname**|列のフルテキスト検索に使用される言語です。|  
  
## <a name="permissions"></a>アクセス許可  
 実行権限は、既定では **public** ロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 次の例では、データベース内のすべてのテーブルでフルテキストインデックスが指定されている列に関する情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_columns_cursor @mycursor OUTPUT  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END;  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>関連項目  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
