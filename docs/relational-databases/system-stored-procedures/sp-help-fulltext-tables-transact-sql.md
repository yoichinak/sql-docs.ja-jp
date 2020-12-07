---
description: sp_help_fulltext_tables (Transact-SQL)
title: sp_help_fulltext_tables (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables
- sp_help_fulltext_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables
ms.assetid: 86e24a5f-a869-43f6-b83e-c52b7b01b5ff
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bcb8ba1c0e4dcd20557ad2291dd9a84912985086
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538866"
---
# <a name="sp_help_fulltext_tables-transact-sql"></a>sp_help_fulltext_tables (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  フルテキストインデックス作成用に登録されているテーブルの一覧を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、 **fulltext_indexes** カタログビューを使用してください。 詳細については、「 [sys. fulltext_indexes &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_fulltext_tables [ [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'` フルテキストカタログの名前を指定します。 *fulltext_catalog_name* は **sysname**,、既定値は NULL です。 *Fulltext_catalog_name*を省略した場合、または NULL の場合は、データベースに関連付けられているすべてのフルテキストインデックス付きテーブルが返されます。 *Fulltext_catalog_name*が指定されていても、 *table_name*が省略されているか、が NULL の場合は、このカタログに関連付けられているフルテキストインデックスが作成されたすべてのテーブルについて、フルテキストインデックス情報が取得されます。 *Fulltext_catalog_name*と*table_name*の両方が指定されている場合*table_name*が*fulltext_catalog_name*に関連付けられていると、行が返されます。それ以外の場合は、エラーが発生します。  
  
`[ @table_name = ] 'table_name'` フルテキストメタデータを要求する1つまたは2つの要素で構成されるテーブル名を指定します。 *table_name* は **nvarchar (517)** で、既定値は NULL です。 *Table_name*だけを指定した場合は、 *table_name*に関連する行だけが返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または (1) エラー  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|テーブル所有者 これは、テーブルを作成したデータベースユーザーの名前です。|  
|**TABLE_NAME**|**sysname**|テーブル名。|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|インデックスは、一意のキー列として指定された列に UNIQUE 制約を強制します。|  
|**FULLTEXT_KEY_COLID**|**int**|FULLTEXT_KEY_NAME によって識別される一意のインデックスの列 ID。|  
|**FULLTEXT_INDEX_ACTIVE**|**int**|このテーブルでフルテキスト インデックス作成のマークが付いている列がクエリに適しているかどうか。<br /><br /> 0 = 非アクティブ<br /><br /> 1 = アクティブ|  
|**FULLTEXT_CATALOG_NAME**|**sysname**|フルテキストインデックスデータが存在するフルテキストカタログ。|  
  
## <a name="permissions"></a>アクセス許可  
 実行権限は、既定では **public** ロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 次の例では、フルテキスト カタログ `Cat_Desc` に関連付けられた、フルテキスト インデックスが作成されているテーブルの名前を返します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_tables 'Cat_Desc';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_fulltext_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
