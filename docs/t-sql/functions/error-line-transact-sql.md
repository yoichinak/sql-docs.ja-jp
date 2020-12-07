---
description: ERROR_LINE (Transact-SQL)
title: ERROR_LINE (Transact-SQL)
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ERROR_LINE
- ERROR_LINE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- errors [SQL Server], line number
- messages [SQL Server], line number
- TRY...CATCH [SQL Server]
- line number of error [SQL Server]
- ERROR_LINE function
- CATCH block
ms.assetid: 47335734-0baf-45a6-8b3b-6c4fd80d2cb8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c914c69646f99fdcb3ff4a214d37faa61feef3b6
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116732"
---
# <a name="error_line-transact-sql"></a>ERROR_LINE (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

この関数では、TRY...CATCH 構文の CATCH ブロックが実行される原因となったエラーが発生した行番号が返されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文

```syntaxsql
ERROR_LINE ( )
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-type"></a>戻り値の型
**int**

## <a name="return-value"></a>戻り値  
CATCH ブロック内で呼び出されると、`ERROR_LINE` は次の値を返します。  
  
-   エラーが発生した行番号    
-   ストアド プロシージャまたはトリガー内でエラーが発生した場合は、ルーチン内の行番号  
-   CATCH ブロックの範囲外で呼び出された場合は、NULL  
  
## <a name="remarks"></a>解説  
`ERROR_LINE` は、CATCH ブロックのスコープ内の任意の場所で呼び出すことができます。  
  
`ERROR_LINE` はエラーが発生した行番号を返します。 これは、CATCH ブロックのスコープ内で `ERROR_LINE` が呼び出された位置に関係なく、また `ERROR_LINE` の呼び出し回数に関係なく発生します。 これは @@ERROR などの関数とは対照的です。 @@ERROR は、エラーが発生したステートメントの直後のステートメントまたは CATCH ブロックの最初のステートメントでエラー番号を返します。  
  
入れ子になった CATCH ブロックでは、`ERROR_LINE` は、参照されている CATCH ブロックのスコープに固有のエラー行番号を返します。 たとえば、TRY...CATCH コンストラクトの CATCH ブロックに、入れ子になった TRY...CATCH コンストラクトが含まれる場合があります。 入れ子になった CATCH ブロック内では、`ERROR_LINE` は、入れ子になった CATCH ブロックを呼び出したエラーの行番号を返します。 `ERROR_LINE` が外部の CATCH ブロックで実行されると、その特定の CATCH ブロックを呼び出したエラーの行番号が返されます。  
  
## <a name="examples"></a>例  
  
### <a name="a-using-error_line-in-a-catch-block"></a>A. CATCH ブロックで ERROR_LINE を使用する  
このコード例は、0 除算エラーを生成する `SELECT` ステートメントを示しています。 `ERROR_LINE` は、エラーが発生した行番号を返します。  
  
```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
```  
  
### <a name="b-using-error_line-in-a-catch-block-with-a-stored-procedure"></a>B.  CATCH ブロックで ERROR_LINE をストアド プロシージャと一緒に使用する  
この例では、0 除算エラーを生成したストアド プロシージャを示します。 `ERROR_LINE` は、エラーが発生した行番号を返します。  
  
```sql  
-- Verify that the stored procedure does not already exist.  
IF OBJECT_ID ( 'usp_ExampleProc', 'P' ) IS NOT NULL   
    DROP PROCEDURE usp_ExampleProc;  
GO  
  
-- Create a stored procedure that  
-- generates a divide-by-zero error.  
CREATE PROCEDURE usp_ExampleProc  
AS  
    SELECT 1/0;  
GO  
  
BEGIN TRY  
    -- Execute the stored procedure inside the TRY block.  
    EXECUTE usp_ExampleProc;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_LINE() AS ErrorLine;  
END CATCH;  
GO  
``` 


### <a name="c-using-error_line-in-a-catch-block-with-other-error-handling-tools"></a>C. CATCH ブロックで ERROR_LINE を他のエラー処理ツールと一緒に使用する  
このコード例は、0 除算エラーを生成する `SELECT` ステートメントを示しています。 `ERROR_LINE` は、エラーが発生した行番号と、そのエラー自体に関する情報を返します。  
  
```sql  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_LINE() AS ErrorLine,  
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
``` 
  
## <a name="see-also"></a>参照  
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [ERROR_STATE &#40;Transact-SQL&#41;](../../t-sql/functions/error-state-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  
