---
description: sp_unbindrule (Transact-sql)
title: sp_unbindrule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unbindrule_TSQL
- sp_unbindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unbindrule
ms.assetid: f54ee155-c3c9-4f1a-952e-632a8339f0cc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7ddf241acfb6e82e0cdd67315727017fb9965f77
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547348"
---
# <a name="sp_unbindrule-transact-sql"></a>sp_unbindrule (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベース内の列または別名データ型のルールをバインド解除します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 代わりに、 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ステートメントまたは [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) ステートメントで default キーワードを使用して、既定の定義を作成することをお勧めします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_unbindrule [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @objname = ] 'object_name'` ルールのバインドを解除するテーブルと列、または別名データ型の名前を指定します。 *object_name* は **nvarchar (776)**,、既定値はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、最初に列名に対して、次に別名データ型に対して、2 つの要素で構成される識別子の解決が試行されます。 別名データ型からルールをバインド解除すると、同じルールを持つデータ型のすべての列もバインド解除されます。 ただし、同じデータ型でも、ルールが直接バインドされている列には影響はありません。  
  
> [!NOTE]  
>  *object_name* には、区切られた識別子の文字として角かっこ **[]** を含めることができます。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
`[ @futureonly = ] 'futureonly_flag'` 別名データ型からルールをバインド解除する場合にのみ使用します。 *futureonly_flag* は **varchar (15)**,、既定値は NULL です。 *Futureonly_flag*が**futureonly**の場合、そのデータ型の既存の列には、指定された規則が失われません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 ルールのテキストを表示するには、ルール名をパラメーターに使用して **sp_helptext** を実行します。  
  
 ルールがバインド解除されると、ルールが列にバインドされている場合は、そのバインドに関する情報が **sys** テーブルから削除されます。また、ルールが別名データ型にバインドされている場合は、 **.sys** テーブルからも削除されます。  
  
 別名データ型からルールをバインド解除すると、その別名データ型のすべての列からも該当するルールがバインド解除されます。 また、ALTER TABLE ステートメントの ALTER COLUMN 句によって後で変更されたデータ型の列にもバインドされている可能性があります。 **sp_unbindrule** を使用し、列名を指定して、これらの列からルールを明示的にバインド解除する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 テーブル列からルールをバインド解除するには、そのテーブルに対する ALTER 権限が必要です。 別名データ型からルールをバインド解除するには、その型に対する CONTROL 権限、または型が属するスキーマに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-unbinding-a-rule-from-a-column"></a>A. 列からのルールのバインド解除  
 次の例では、テーブルの列からルールをバインド解除し `startdate` `employees` ます。  
  
```  
EXEC sp_unbindrule 'employees.startdate';  
```  
  
### <a name="b-unbinding-a-rule-from-an-alias-data-type"></a>B. 別名データ型からルールをバインド解除する  
 次の例では、別名データ型 `ssn` からルールをバインド解除します。 その型の既存および将来の列からルールをバインド解除します。  
  
```  
EXEC sp_unbindrule ssn;  
```  
  
### <a name="c-using-futureonly_flag"></a>C. Futureonly_flag の使用  
 次の例では、既存の `ssn` 列に影響を与えずに、別名データ型 `ssn` からルールをバインド解除します。  
  
```  
EXEC sp_unbindrule 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 区切られた識別子の使用  
 次の例では、 *object_name* パラメーターで区切られた識別子を使用しています。  
  
```  
CREATE TABLE [t.4] (c1 int); -- Notice the period as part of the table   
-- name.  
GO  
CREATE RULE rule2 AS @value > 100;  
GO  
EXEC sp_bindrule rule2, '[t.4].c1' -- The object contains two   
-- periods; the first is part of the table name and the second   
-- distinguishes the table name from the column name.  
GO  
EXEC sp_unbindrule '[t.4].c1';  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_bindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
