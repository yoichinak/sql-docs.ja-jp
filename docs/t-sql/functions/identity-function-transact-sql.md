---
title: "IDENTITY (関数) (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IDENTITY_TSQL
- IDENTITY
dev_langs: TSQL
helpviewer_keywords:
- IDENTITY function
- SELECT statement [SQL Server], IDENTITY function
- inserting identity columns
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY function
ms.assetid: ebec77eb-fc02-4feb-b6c5-f0098d43ccb6
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 70fbbbae7e04331130346702c8f974669d53942a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="identity-function-transact-sql"></a>IDENTITY (関数) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  INTO *table* 句と共に SELECT ステートメントでのみ使用し、新しいテーブルに ID 列を追加します。IDENTITY 関数は、CREATE TABLE と ALTER TABLE で使用される IDENTITY プロパティと似ていますが、同じものではありません。  
  
> [!NOTE]  
>  複数のテーブルで使用できる自動的に増分する番号、またはテーブルを参照せずにアプリケーションから呼び出すことができる自動的に増分する番号を作成するには、「[シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
IDENTITY (data_type [ , seed , increment ] ) AS column_name  
```  
  
## <a name="arguments"></a>引数  
 *data_type*  
 ID 列のデータ型を指定します。 有効なデータ型、id 列では、整数データ型カテゴリに、任意のデータ型を除く、**ビット**データ型、または**decimal**データ型。  
  
 *seed*  
 テーブル内の先頭行に割り当てる整数値を指定します。それ以降の各行には、前の IDENTITY 値に *increment* 値を加えた次の ID 値が割り当てられます。*seed* と *increment* のいずれも指定しなかった場合は、両方とも既定値 1 が使用されます。  
  
 *increment*  
 テーブル内の連続する行に対して、*seed* の値に加える整数値です。  
  
 *column_name*  
 新しいテーブルに挿入する列の名前を指定します。  
  
## <a name="return-types"></a>戻り値の型  
 *data_type* と同じデータ型が返されます。  
  
## <a name="remarks"></a>解説  
 この関数ではテーブルに列が作成されるので、次のいずれかの方法で選択リストから列名を指定する必要があります。  
  
```  
--(1)  
SELECT IDENTITY(int, 1,1) AS ID_Num  
INTO NewTable  
FROM OldTable;  
  
--(2)  
SELECT ID_Num = IDENTITY(int, 1, 1)  
INTO NewTable  
FROM OldTable;  
  
```  
  
## <a name="examples"></a>使用例  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの `Contact` テーブルにあるすべての行を、`NewContact` という新しいテーブルに追加します。 IDENTITY 関数を使用して、`NewContact` テーブルの識別番号を 1 ではなく 100 から開始するようにします。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.NewContact', N'U') IS NOT NULL  
    DROP TABLE Person.NewContact;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
SELECT  IDENTITY(smallint, 100, 1) AS ContactNum,  
        FirstName AS First,  
        LastName AS Last  
INTO Person.NewContact  
FROM Person.Person;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
SELECT ContactNum, First, Last FROM Person.NewContact;  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)  
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)  
 [IDENTITY &#40;プロパティ&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)  
 [SELECT @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/select-local-variable-transact-sql.md)  
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)  
 [sys.identity_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
  
