---
description: sp_bindefault (Transact-sql)
title: sp_bindefault (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/25/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindefault
- sp_bindefault_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindefault
ms.assetid: 3da70c10-68d0-4c16-94a5-9e84c4a520f6
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 21f743aa4c28095a3167ebb16cf873f46afece38
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541962"
---
# <a name="sp_bindefault-transact-sql"></a>sp_bindefault (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  デフォルトを列または別名データ型にバインドします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに、 [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) または [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) ステートメントの default キーワードを使用して、既定の定義を作成することをお勧めします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_bindefault [ @defname = ] 'default' ,   
    [ @objname = ] 'object_name'   
    [ , [ @futureonly = ] 'futureonly_flag' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @defname = ] 'default'` CREATE DEFAULT によって作成される既定の名前を指定します。 *既定値* は **nvarchar (776)**,、既定値はありません。  
  
`[ @objname = ] 'object_name'` 既定値をバインドするテーブルと列、または別名データ型の名前を指定します。 *object_name* は **nvarchar (776)** で、既定値はありません。 *object_name* は、 **varchar (max)**、 **nvarchar (max)**、 **varbinary (MAX)**、 **xml**、または CLR ユーザー定義型では定義できません。  
  
 *Object_name*が1つの部分で構成される名前である場合、別名データ型として解決されます。 2部構成または3部構成の名前の場合は、最初にテーブルと列として解決されます。この解決が失敗した場合、別名データ型として解決されます。 既定では、default が列に直接バインドされていない限り、別名データ型の既存の列は *default*を継承します。 既定値をバインドすることはできません、 **text**,、 **ntext**,、 **イメージ**,、 **varchar (max**),、 **nvarchar (max)**,、 **varbinary (max)**,、 **xml**,、 **タイムスタンプ**,、または CLR ユーザー定義型の列、IDENTITY プロパティを持つ列、計算列、または既に既定の制約が設定されている列です。  
  
> [!NOTE]  
>  *object_name* には、区切られた識別子として角かっこ **[]** を含めることができます。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
`[ @futureonly = ] 'futureonly_flag'` は、別名データ型に既定値をバインドする場合にのみ使用されます。 *futureonly_flag* は **varchar (15)** で、既定値は NULL です。 このパラメーターが **futureonly**に設定されている場合、そのデータ型の既存の列は新しい既定値を継承できません。 このパラメーターは、既定値を列にバインドするときには使用されません。 *Futureonly_flag*が NULL の場合、新しい既定値は、現在既定値を持たない別名データ型の列、または別名データ型の既存の既定値を使用している列にバインドされます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **Sp_bindefault**を使用すると、新しい既定値を列にバインドできます。ただし、既定の制約を使用することをお勧めします。または、既存の既定値をアンバインドせずに別名データ型に対して使用することもできます。 古い既定値はオーバーライドされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]システムデータ型または CLR ユーザー定義型に既定値をバインドすることはできません。 既定値がバインド先の列と互換性がない場合、バインド時ではなく、既定値を挿入しようとする [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] とエラーメッセージが返されます。  
  
 別名データ型の既存の列は、既定値が直接バインドされているか、 *futureonly_flag* または **futureonly**として指定されていない限り、新しい既定値を継承します。 別名データ型の新しい列は、常に既定値を継承します。  
  
 既定値を列にバインドすると、関連する情報が、列 **カタログビュー** に追加されます。 別名データ型に既定値をバインドすると、関連する情報が、の **種類** のカタログビューに追加されます。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは、テーブルを所有しているか、 **sysadmin** 固定サーバーロールのメンバーであるか、固定データベースロールの **db_owner** および **db_ddladmin** である必要があります。  
  
## <a name="examples"></a>例  
  
### <a name="a-binding-a-default-to-a-column"></a>A. 列への既定値のバインド  
 既定値の CREATE DEFAULT を使用して、現在のデータベースでという名前の既定値 `today` が定義されています。次の例では、テーブルの列に既定値をバインドしてい `HireDate` `Employee` ます。 `Employee` テーブルに行を追加するときに、`HireDate` 列の入力がなければ、この列にデフォルト `today` が入力されます。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'today', 'HumanResources.Employee.HireDate';  
```  
  
### <a name="b-binding-a-default-to-an-alias-data-type"></a>B. 別名データ型に既定値をバインドする  
 `def_ssn` という名前のデフォルトと、`ssn` という別名データ型が既に存在しています。 次の例では、既定の `def_ssn` をにバインド `ssn` しています。 テーブルが作成されると、別名データ型が割り当てられているすべての列によって、既定値が継承され `ssn` ます。 **Ssn**型の既存の列も既定の**def_ssn**を継承します。ただし、 *futureonly_flag*値に**futureonly**が指定されていない場合、または列に既定のが直接バインドされている場合を除きます。 列にバインドされているデフォルトは、データ型にバインドされているデフォルトより常に優先します。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn';  
```  
  
### <a name="c-using-the-futureonly_flag"></a>C. Futureonly_flag の使用  
 次の例では、 `def_ssn` 別名データ型に既定値をバインドし `ssn` ます。 **Futureonly**が指定されているため、型の既存の列 `ssn` は影響を受けません。  
  
```  
USE master;  
GO  
EXEC sp_bindefault 'def_ssn', 'ssn', 'futureonly';  
```  
  
### <a name="d-using-delimited-identifiers"></a>D. 区切られた識別子の使用  
 次の例では、object_name で区切られた識別子を使用して `[t.1]` います。 *object_name*  
  
```  
USE master;  
GO  
CREATE TABLE [t.1] (c1 int);   
-- Notice the period as part of the table name.  
EXEC sp_bindefault 'default1', '[t.1].c1' ;  
-- The object contains two periods;   
-- the first is part of the table name,   
-- and the second distinguishes the table name from the column name.  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [DROP DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-default-transact-sql.md)   
 [sp_unbindefault &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
