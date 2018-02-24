---
title: "IDENT_CURRENT (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IDENT_CURRENT
- IDENT_CURRENT_TSQL
dev_langs: TSQL
helpviewer_keywords:
- last identity value generated for table
- identity values [SQL Server], last generated
- identity columns, current value
- IDENT_CURRENT function
ms.assetid: 21517ced-39f5-4cd8-8d9c-0a0b8aff554a
caps.latest.revision: "49"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9e303b59af41301be2b171c9b6a917dfad6139dc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="identcurrent-transact-sql"></a>IDENT_CURRENT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定されたテーブルまたはビューに対して生成された最新の ID 値を返します。 最新の ID 値は、任意のセッションおよびスコープに対して生成されることがあります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
IDENT_CURRENT( 'table_name' )  
```  
  
## <a name="arguments"></a>引数  
 *table_name*  
 ID 値が返されるテーブルの名前を指定します。 *table_name*は**varchar**、既定値はありません。  
  
## <a name="return-types"></a>戻り値の型  
 **numeric(38,0)**  
  
## <a name="exceptions"></a>例外  
 エラーが発生した場合、または呼び出し元にオブジェクトの表示権限がない場合は、NULL が返されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ユーザーは、ユーザーが所有するまたはをユーザーが許可されているアクセス許可のセキュリティ保護可能なメタデータのみを表示できます。 つまり、オブジェクトに対する権限がユーザーに与えられていない場合、メタデータを生成する組み込み関数 (IDENT_CURRENT など) が NULL を返す可能性があります。 詳細については、「 [メタデータ表示の構成](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="remarks"></a>解説  
 IDENT_CURRENT は、[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] の ID 関数 SCOPE_IDENTITY および @@IDENTITY に似ています。3 つの関数とも、最後に生成された ID 値を返します。ただし、各関数の中で、*最後*が定義されるスコープとセッションがそれぞれ異なります。  
  
-   IDENT_CURRENT は、任意のセッションおよび任意のスコープ内の特定のテーブルに対して生成された最後の ID 値を返します。  
  
-   @@IDENTITYすべてのスコープ全体で任意のテーブルの現在のセッションで生成された最後の ID 値を返します。  
  
-   SCOPE_IDENTITY は、現在のセッションと現在のスコープ内の任意のテーブルに対して生成された最後の ID 値を返します。  
  
 IDENT_CURRENT 値が NULL の場合 (テーブルに行が格納されたことがないか、テーブルで切り捨てが行われたため)、IDENT_CURRENT 関数はシード値を返します。  
  
 失敗したステートメントとトランザクションによって、テーブルに対する現在の ID が変更され、ID 列値に差異が生じる可能性があります。 ID 値がロールバックされることはありません。これは、テーブルに値を挿入するトランザクションがコミットされない場合でも同じです。 たとえば、INSERT ステートメントが IGNORE_DUP_KEY 違反のために失敗しても、テーブルの現在の ID 値は増分されます。  
  
 次に生成される ID 値の予測に IDENT_CURRENT を使用する場合は注意してください。 実際に生成される値は、他のセッションで実行される挿入操作が原因で、IDENT_CURRENT と IDENT_INCR の合計値とは異なる場合があります。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-the-last-identity-value-generated-for-a-specified-table"></a>A. 指定したテーブルに対して生成された最新の ID 値を返す  
 次の例では、`AdventureWorks2012` データベースの `Person.Address` テーブルに対して生成された最新の ID 値を返します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENT_CURRENT ('Person.Address') AS Current_Identity;  
GO  
```  
  
### <a name="b-comparing-identity-values-returned-by-identcurrent-identity-and-scopeidentity"></a>B. IDENT_CURRENT、によって返された id 値を比較する@IDENTITYおよび SCOPE_IDENTITY  
 次の例では、`IDENT_CURRENT`、`@@IDENTITY`、および `SCOPE_IDENTITY` によって返される異なる ID 値を示しています。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N't6', N'U') IS NOT NULL   
    DROP TABLE t6;  
GO  
IF OBJECT_ID(N't7', N'U') IS NOT NULL   
    DROP TABLE t7;  
GO  
CREATE TABLE t6(id int IDENTITY);  
CREATE TABLE t7(id int IDENTITY(100,1));  
GO  
CREATE TRIGGER t6ins ON t6 FOR INSERT   
AS  
BEGIN  
   INSERT t7 DEFAULT VALUES  
END;  
GO  
--End of trigger definition  
  
SELECT id FROM t6;  
--IDs empty.  
  
SELECT id FROM t7;  
--ID is empty.  
  
--Do the following in Session 1  
INSERT t6 DEFAULT VALUES;  
SELECT @@IDENTITY;  
/*Returns the value 100. This was inserted by the trigger.*/  
  
SELECT SCOPE_IDENTITY();  
/* Returns the value 1. This was inserted by the   
INSERT statement two statements before this query.*/  
  
SELECT IDENT_CURRENT('t7');  
/* Returns value inserted into t7, that is in the trigger.*/  
  
SELECT IDENT_CURRENT('t6');  
/* Returns value inserted into t6. This was the INSERT statement four statements before this query.*/  
  
-- Do the following in Session 2.  
SELECT @@IDENTITY;  
/* Returns NULL because there has been no INSERT action   
up to this point in this session.*/  
  
SELECT SCOPE_IDENTITY();  
/* Returns NULL because there has been no INSERT action   
up to this point in this scope in this session.*/  
  
SELECT IDENT_CURRENT('t7');  
/* Returns the last value inserted into t7.*/  
```  
  
## <a name="see-also"></a>参照  
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [IDENT_INCR &#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [IDENT_SEED &#40;Transact-SQL&#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [システム関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
