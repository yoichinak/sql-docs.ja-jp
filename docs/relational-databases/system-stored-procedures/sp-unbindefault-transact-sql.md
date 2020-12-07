---
description: sp_unbindefault (Transact-sql)
title: sp_unbindefault (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unbindefault_TSQL
- sp_unbindefault
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindefault
ms.assetid: c96a6c5e-f3ca-4c1e-b64b-0d8ef6986af8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b8a0ee77c73c6edcee17d6baad363c6c02eb52c3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543004"
---
# <a name="sp_unbindefault-transact-sql"></a>sp_unbindefault (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースの列または別名データ型から、デフォルトをバインド解除 (削除) します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 代わりに、 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ステートメントまたは [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) ステートメントで default キーワードを使用して、既定の定義を作成することをお勧めします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_unbindefault [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @objname = ] 'object_name'` 既定値のバインドを解除するテーブルと列、または別名データ型の名前を指定します。 *object_name* は **nvarchar (776)**,、既定値はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、最初に列名に対して、次に別名データ型に対して、2 つの要素で構成される識別子の解決が試行されます。  
  
 別名データ型から既定値をバインド解除すると、同じ既定値を持つそのデータ型の列もバインド解除されます。 ただし、同じデータ型でも、デフォルトが直接バインドされている列は影響を受けません。  
  
> [!NOTE]  
>  *object_name* には、区切られた識別子の文字として角かっこ **[]** を含めることができます。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
`[ @futureonly = ] 'futureonly_flag'` 別名データ型から既定値をバインド解除する場合にのみ使用します。 *futureonly_flag* は **varchar (15)**,、既定値は NULL です。 *Futureonly_flag*が**futureonly**の場合、データ型の既存の列には指定された既定値が失われません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 既定のテキストを表示するには、パラメーターとして既定の名前を使用して **sp_helptext** を実行します。  
  
## <a name="permissions"></a>アクセス許可  
 テーブル列から既定値のバインドを解除するには、テーブルに対する ALTER 権限が必要です。 別名データ型から既定値をアンバインドするには、その型に対する CONTROL 権限、または型が属するスキーマに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-unbinding-a-default-from-a-column"></a>A. 列からの既定値のバインド解除  
 次の例では、`hiredate` テーブルの `employees` 列からデフォルトをバインド解除します。  
  
```  
EXEC sp_unbindefault 'employees.hiredate';  
```  
  
### <a name="b-unbinding-a-default-from-an-alias-data-type"></a>B. 別名データ型からデフォルトをバインド解除する  
 次の例では、別名データ型の `ssn` からデフォルトをバインド解除します。 この型の既存の列と将来の列をバインド解除します。  
  
```  
EXEC sp_unbindefault 'ssn';  
```  
  
### <a name="c-using-the-futureonly_flag"></a>C. Futureonly_flag の使用  
 次の例では、既存の列に影響を与えずに別名データ型の将来の使用をバインド解除し `ssn` `ssn` ます。  
  
```  
EXEC sp_unbindefault 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 区切られた識別子の使用  
 次の例では、 *object_name* パラメーターで区切られた識別子を使用しています。  
  
```  
CREATE TABLE [t.3] (c1 int); -- Notice the period as part of the table   
-- name.  
CREATE DEFAULT default2 AS 0;  
GO  
EXEC sp_bindefault 'default2', '[t.3].c1' ;  
-- The object contains two periods;  
-- the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
EXEC sp_unbindefault '[t.3].c1';  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_bindefault &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
