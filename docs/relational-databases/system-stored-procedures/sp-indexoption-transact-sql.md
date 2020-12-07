---
description: sp_indexoption (Transact-sql)
title: sp_indexoption (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_indexoption
- sp_indexoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexoption
ms.assetid: 75f836be-d322-4a53-a45d-25bee6b42a52
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aaaf9863e6226de5aa30d553bfa4c7766588524b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547900"
---
# <a name="sp_indexoption-transact-sql"></a>sp_indexoption (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ユーザー定義のクラスター化インデックスと非クラスター化インデックス、またはクラスター化インデックスのないテーブルに対して、ロックのオプション値を設定します。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]は、ページレベル、行レベル、またはテーブルレベルのロックを自動的に選択します。 これらのオプションを手動で設定する必要はありません。 **sp_indexoption** は、特定の種類のロックが常に適切であることを理解している上級ユーザー向けに用意されています。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] 代わりに、 [ALTER INDEX &#40;transact-sql&#41;](../../t-sql/statements/alter-index-transact-sql.md)を使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_indexoption [ @IndexNamePattern = ] 'table_or_index_name'   
    , [ @OptionName = ] 'option_name'   
    , [ @OptionValue = ] 'value'  
```  
  
## <a name="arguments"></a>引数  
`[ @IndexNamePattern = ] 'table_or_index_name'` ユーザー定義テーブルまたはインデックスの修飾名または修飾され名を指定します。 *table_or_index_name* は **nvarchar (1035)**,、既定値はありません。 引用符は、修飾インデックスまたはテーブル名が指定されている場合にのみ必要です。 データベース名も含めてフル パスで指定した場合は、そのデータベース名は現在のデータベース名である必要があります。 インデックスなしでテーブル名を指定した場合、指定されたオプション値は、そのテーブルのすべてのインデックスと、クラスター化インデックスが存在しない場合はテーブル自体に設定されます。  
  
`[ @OptionName = ] 'option_name'` インデックスオプションの名前を指定します。 *option_name* は **varchar (35)**,、既定値はありません。 *option_name* には、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**AllowRowLocks**|TRUE の場合、インデックスにアクセスするときに行ロックが許可されます。 いつ行ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって決定されます。 FALSE の場合、行ロックは使用されません。 既定値は TRUE です。|  
|**AllowPageLocks**|TRUE の場合、インデックスにアクセスするときにページ ロックが許可されます。 いつページ ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] によって決定されます。 FALSE の場合、ページ ロックは使用されません。 既定値は TRUE です。|  
|**DisAllowRowLocks**|TRUE の場合、行ロックは使用されません。 FALSE の場合、インデックスにアクセスするときに行ロックが許可されます。 いつ行ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって決定されます。|  
|**DisAllowPageLocks**|TRUE の場合、ページ ロックは使用されません。 FALSE の場合、インデックスにアクセスするときにページロックが許可されます。 いつページ ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] によって決定されます。|  
  
`[ @OptionValue = ] 'value'`*Option_name*設定を有効にするかどうかを指定します (TRUE、ON、yes、または 1) または DISABLED (FALSE、OFF、no、または 0)。 *値* は **varchar (12)**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または0より大きい (失敗)  
  
## <a name="remarks"></a>解説  
 XML インデックスはサポートされていません。 XML インデックスが指定されている場合、またはテーブル名にインデックス名が指定されておらず、テーブルに XML インデックスが含まれている場合、ステートメントは失敗します。 これらのオプションを設定するには、代わりに [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) を使用します。  
  
 現在の行およびページロックのプロパティを表示するには、 [Indexproperty](../../t-sql/functions/indexproperty-transact-sql.md)またはのカタログビューを使用[します。](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
-   **Allowrowlocks** = true または**DisAllowRowLocks** = false の場合、および**Allowrowlocks** = true または**DisAllowPageLocks** = false の場合、インデックスにアクセスするときに、行レベル、ページレベル、およびテーブルレベルのロックが許可されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]は適切なロックを選択し、行ロックまたはページ ロックをテーブル ロックにエスカレートすることができます。  
  
 **Allowrowlocks** = false または**DisAllowRowLocks** = True と**Allowrowlocks** = false または**DisAllowPageLocks** = true の場合、インデックスにアクセスするときにはテーブルレベルのロックのみが許可されます。  
  
 テーブル名をインデックスなしで指定すると、設定はそのテーブルのすべてのインデックスに適用されます。 基になるテーブルにクラスター化インデックスがない (つまりヒープである) 場合、設定は次のように適用されます。  
  
-   **Allowrowlocks**または**DisAllowRowLocks**が TRUE または FALSE に設定されている場合、設定はヒープおよび関連する非クラスター化インデックスに適用されます。  
  
-   **Allowpagelocks**オプションが TRUE に設定されているか、 **DisAllowPageLocks**が FALSE に設定されている場合、設定はヒープおよび関連する非クラスター化インデックスに適用されます。  
  
-   **Allowpagelocks**オプションが FALSE に設定されているか、 **DisAllowPageLocks**が TRUE に設定されている場合、この設定は非クラスター化インデックスに完全に適用されます。 つまり、非クラスター化インデックスでは、すべてのページロックが許可されません。 ヒープで許可されないのは、ページに対する共有 (S)、更新 (U)、および排他 (X) ロックのみです。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]では内部目的用にインテント ページ ロック (IS、IU、または IX) を引き続き取得できます。  
  
## <a name="permissions"></a>アクセス許可  
 テーブルに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-setting-an-option-on-a-specific-index"></a>A. 特定のインデックスに対してオプションを設定する  
 次の例では、テーブルのインデックスでページロックを許可し `IX_Customer_TerritoryID` `Customer` ません。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_indexoption N'Sales.Customer.IX_Customer_TerritoryID',  
    N'disallowpagelocks', TRUE;  
```  
  
### <a name="b-setting-an-option-on-all-indexes-on-a-table"></a>B. テーブルのすべてのインデックスに対してオプションを設定する  
 次の例では、テーブルに関連付けられているすべてのインデックスに対して行ロックを許可 `Product` しません。 `sys.indexes` プロシージャの実行前と後に `sp_indexoption` カタログ ビューに対するクエリを実行して、ステートメントの結果を表示します。  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
-- Set the disallowrowlocks option on the Product table.   
EXEC sp_indexoption N'Production.Product',  
    N'disallowrowlocks', TRUE;  
GO  
--Verify the row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
```  
  
### <a name="c-setting-an-option-on-a-table-with-no-clustered-index"></a>C. クラスター化インデックスのないテーブルに対してオプションを設定する  
 次の例では、クラスター化インデックスを持たないテーブル (ヒープ) について、ページ ロックを許可していません。 `sys.indexes`ステートメントの結果を表示するには、プロシージャを実行する前と後にカタログビューを照会し `sp_indexoption` ます。  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options of the table.   
SELECT OBJECT_NAME (object_id) AS [Table], type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
-- Set the disallowpagelocks option on the table.   
EXEC sp_indexoption DatabaseLog,  
    N'disallowpagelocks', TRUE;  
GO  
--Verify the row and page lock settings of the table.  
SELECT OBJECT_NAME (object_id) AS [Table], allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
