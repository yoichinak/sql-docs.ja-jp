---
description: sp_bindrule (Transact-SQL)
title: sp_bindrule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindrule_TSQL
- sp_bindrule
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindrule
ms.assetid: 2606073e-c52f-498d-a923-5026b9d97e67
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c7355f421701c5eb24da58dec5037b5fb1b8317c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548319"
---
# <a name="sp_bindrule-transact-sql"></a>sp_bindrule (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  ルールを列または別名データ型にバインドします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに[、Unique 制約と Check 制約](../../relational-databases/tables/unique-constraints-and-check-constraints.md) を使用してください。 CHECK 制約は、 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) または [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ステートメントの check キーワードを使用して作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_bindrule [ @rulename = ] 'rule' ,   
     [ @objname = ] 'object_name'   
     [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @rulename = ] 'rule'` CREATE RULE ステートメントによって作成されたルールの名前を指定します。 *rule* は **nvarchar (776)**,、既定値はありません。  
  
`[ @objname = ] 'object_name'` テーブルと列、またはルールをバインドする別名データ型を指定します。 **text**、**ntext**、**image**、**varchar(max)**、**nvarchar(max)**、**varbinary(max)**、**xml**、CLR ユーザー定義型、**timestamp** の列には、ルールをバインドできません。 ルールは計算列にバインドできません。  
  
 *object_name* は **nvarchar (776)** で、既定値はありません。 *Object_name*が1つの部分で構成される名前である場合、別名データ型として解決されます。 2部構成または3部構成の名前の場合は、最初にテーブルと列として解決されます。この解決が失敗した場合、別名データ型として解決されます。 既定では、列に規則が直接バインドされていない限り、別名データ型の既存の列は *rule* を継承します。  
  
> [!NOTE]  
>  *object_name* には、かっこ **[** および **]** 文字を区切られた識別子文字として含めることができます。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
> [!NOTE]  
>  別名データ型を使用する式に対して作成されたルールは、列または別名データ型にバインドできますが、参照されてもコンパイルできません。 別名データ型に対して作成されたルールは使用しないでください。  
  
`[ @futureonly = ] 'futureonly_flag'` は、規則を別名データ型にバインドする場合にのみ使用されます。 *future_only_flag* は **varchar (15)** で、既定値は NULL です。 このパラメーターを **futureonly** に設定すると、別名データ型の既存の列によって新しいルールが継承されるのを防ぐことができます。 *Futureonly_flag*が NULL の場合、新しいルールは、現在ルールが設定されていないか、別名データ型の既存のルールを使用している別名データ型の列にバインドされます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 新しいルールを列にバインドすることができます (CHECK 制約を使用することをお勧めします)。または、既存のルールをバインド解除せずに **sp_bindrule** の別名データ型にバインドすることもできます。 元のルールはオーバーライドされます。 既に CHECK 制約のある列にルールをバインドすると、すべての制限が評価されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型にはルールをバインドできません。  
  
 このルールは、バインドではなく、INSERT ステートメントが試行されたときに適用されます。 文字ルールを **数値** データ型の列にバインドすることはできますが、このような挿入操作は無効です。  
  
 別名データ型の既存の列は、 *futureonly_flag* が **futureonly**として指定されていない限り、新しいルールを継承します。 別名データ型で定義された新しい列は、常にルールを継承します。 しかし、ALTER TABLE ステートメントの ALTER COLUMN 句によって、列のデータ型をルールがバインドされた別名データ型に変更すると、データ型にバインドしているルールはその列に継承されません。 このルールは、 **sp_bindrule**を使用して列に明示的にバインドされている必要があります。  
  
 ルールを列にバインドすると、関連する情報が **sys** テーブルに追加されます。 別名データ型にルールをバインドすると、関連する情報が、 **sys. types** テーブルに追加されます。  
  
## <a name="permissions"></a>アクセス許可  
 テーブル列にルールをバインドするには、そのテーブルに対する ALTER 権限が必要です。 別名データ型に対する CONTROL 権限、または型が属するスキーマに対する ALTER 権限は、ルールを別名データ型にバインドするために必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-binding-a-rule-to-a-column"></a>A. ルールを列にバインドする  
 CREATE RULE ステートメントを使用して、という名前のルールが現在のデータベースに作成されていると仮定すると、 `today` 次の例では、ルールをテーブルの列にバインドしてい `HireDate` `Employee` ます。 行が `Employee` テーブルに追加されると、`HireDate` 列のデータは `today` ルールと照らし合わせてチェックされます。  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-rule-to-an-alias-data-type"></a>B. 別名データ型にルールをバインドする  
 `rule_ssn` という名前のルールがあり、`ssn` という名前の別名データ型があるものとします。次の例では、`rule_ssn` を `ssn` にバインドします。 CREATE TABLE ステートメントでは、型の列が `ssn` ルールを継承し `rule_ssn` ます。 `ssn` `rule_ssn` *Futureonly_flag*に対して**futureonly**が指定されていない場合、または `ssn` ルールが直接バインドされている場合を除き、型の既存の列もルールを継承します。 列にバインドされたルールは、データ型にバインドされたルールよりも常に優先されます。  
  
```  
USE master;  
GO  
EXEC sp_bindrule 'rule_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonly_flag"></a>C. Futureonly_flag の使用  
 次の例では、`rule_ssn` ルールを別名データ型 `ssn` にバインドします。 `futureonly` が指定されているため、`ssn` 型の既存の列は影響を受けません。  
  
```  
USE master;  
GO  
EXEC sp_bindrule rule_ssn, 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 区切られた識別子の使用  
 *Object_name*パラメーターで区切られた識別子の使用例を次に示します。  
  
```  
USE master;  
GO  
CREATE TABLE [t.2] (c1 int) ;  
-- Notice the period as part of the table name.  
EXEC sp_bindrule rule1, '[t.2].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [DROP RULE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-rule-transact-sql.md)   
 [sp_unbindrule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
