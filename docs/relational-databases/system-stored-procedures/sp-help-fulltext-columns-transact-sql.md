---
description: sp_help_fulltext_columns (Transact-sql)
title: sp_help_fulltext_columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns
- sp_help_fulltext_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns
ms.assetid: 92c8656b-f7fd-4904-9796-acc9ffed4106
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 029cd09cca1945a521d7a8a11c47ea8b7700b57e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535819"
---
# <a name="sp_help_fulltext_columns-transact-sql"></a>sp_help_fulltext_columns (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  フルテキスト インデックス作成用として指定された列を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、 [fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) カタログビューを使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_fulltext_columns [ [ @table_name = ] 'table_name' ] ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table_name = ] 'table\_name'` フルテキストインデックス情報を要求する1つまたは2つの要素で構成されるテーブル名を指定します。 *table_name* は **nvarchar (517)** で、既定値は NULL です。 *Table_name*を省略した場合、フルテキストインデックスが作成されたテーブルごとにフルテキストインデックス列の情報が取得されます。  
  
`[ @column_name = ] 'column\_name'` フルテキストインデックスメタデータが要求される列の名前を指定します。 *column_name* は **sysname**で、既定値は NULL です。 *Column_name*を省略した場合、または NULL の場合、 *table_name*のフルテキストインデックス列ごとにフルテキスト列情報が返されます。 *Table_name*も省略した場合、または NULL の場合は、データベース内のすべてのテーブルのフルテキストインデックスが作成されたすべての列に対してフルテキストインデックス列の情報が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または (1) エラー  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|テーブル所有者 これは、テーブルを作成したデータベースユーザーの名前です。|  
|**TABLE_ID**|**int**|テーブルの ID。|  
|**TABLE_NAME**|**sysname**|テーブルの名前。|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|インデックス作成用に指定されているフルテキストインデックス付きテーブルの列。|  
|**FULLTEXT_COLID**|**int**|フルテキスト インデックスが作成された列の列 ID。|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|フルテキスト インデックスが作成されたテーブル内の列で、フルテキスト インデックス列のドキュメントの種類を指定する列。 この値は、フルテキストインデックスが作成された列が **varbinary (max)** 列または **image** 列の場合にのみ適用されます。|  
|**FULLTEXT_BLOBTP_COLID**|**int**|ドキュメント型列の列 ID。 この値は、フルテキストインデックスが作成された列が **varbinary (max)** 列または **image** 列の場合にのみ適用されます。|  
|**FULLTEXT_LANGUAGE**|**sysname**|列のフルテキスト検索に使用される言語です。|  
  
## <a name="permissions"></a>アクセス許可  
 実行権限は、既定では **public** ロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 次の例では、`Document` テーブルでフルテキスト インデックス作成用に指定された列に関する情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_columns 'Production.Document';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
