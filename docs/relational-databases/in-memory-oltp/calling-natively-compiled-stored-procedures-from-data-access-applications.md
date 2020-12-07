---
title: ネイティブ コンパイル ストアド プロシージャ - データ アクセス アプリケーション
description: SQL Server Native Client の ODBC ドライバーを使用する例を使用して、データ アクセス アプリケーションからネイティブ コンパイル ストアド プロシージャを呼び出す方法について説明します。
ms.custom: seo-dt-2019
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 9cf6c5ff-4548-401a-b3ec-084f47ff0eb8
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b63ebe7f73561408e464d73b29101c42ac111480
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867301"
---
# <a name="calling-natively-compiled-stored-procedures-from-data-access-applications"></a>データ アクセス アプリケーションからのネイティブ コンパイル ストアド プロシージャの呼び出し

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

このトピックでは、データ アクセス アプリケーションからのネイティブ コンパイル ストアド プロシージャの呼び出しに関するガイダンスを示します。

## <a name="guidance-points"></a>ガイダンスのポイント

- カーソルは、ネイティブ コンパイル ストアド プロシージャに対して繰り返し処理できません。

- コンテキスト接続を使用して CLR モジュールからネイティブ コンパイル ストアド プロシージャを呼び出すことはできません。

### <a name="sqlclient"></a>SqlClient

- SqlClient の場合、*準備*実行と*直接*実行の区別はありません。 `CommandType = CommandType.StoredProcedure` で SqlCommand を使用してストアド プロシージャを実行します。

- SqlClient では、準備された RPC プロシージャ呼び出しはサポートされません。

- SqlClient では、ネイティブ コンパイル ストアド プロシージャ (`CommandType.SchemaOnly`) から返された結果セットに関するスキーマのみの情報 (メタデータ検出) の取得はサポートされません。
  - 代わりに、[sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) を使用します。

### <a name="sql-server-native-client"></a>SQL Server Native Client

- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] より前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client では、ネイティブ コンパイル ストアド プロシージャから返された結果セットに関するスキーマのみの情報 (メタデータ検出) の取得はサポートされません。
- 代わりに、[sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) を使用します。

### <a name="odbc"></a>ODBC

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client で ODBC ドライバーを使用したネイティブ コンパイル ストアド プロシージャの呼び出しに関して、次の推奨事項が適用されます。

"*呼び出しが 1 回のみ:* "1 回だけストアド プロシージャを呼び出すのに最も効率的な方法は、 **SQLExecDirect** と ODBC CALL 句を使用して直接 RPC を呼び出す方法です。 [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXECUTE** ステートメントを使用しないでください。 ストアド プロシージャを複数回呼び出す場合は、準備実行が効率的です。

"*呼び出しが複数回:* "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャを複数回呼び出すのに最も効率的な方法は、準備された RPC プロシージャ呼び出しを使用する方法です。 準備された RPC 呼び出しは、次のように、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の ODBC ドライバーを使用して実行されます。

1. データベースへの接続を開きます。
2. **SQLBindParameter** を使用してパラメーターをバインドします。
3. **SQLPrepare** を使用してプロシージャ呼び出しを準備します。
4. **SQLExecute** を使用してストアド プロシージャを複数回実行します。

#### <a name="c-code-for-odbc"></a>ODBC 用の C コード

次の C コード フラグメントは、注文に行アイテムを追加するためのストアド プロシージャの準備実行を示しています。 **SQLPrepare** は、1 回のみ呼び出されます。 **SQLExecute** は、複数回呼び出されます (プロシージャを実行するたびに 1 回呼び出されます)。

```cpp
// Bind parameters
// 1 - OrdNo
SQLRETURN returnCode = SQLBindParameter(
                     hstmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 10, 0,
                     &order.OrdNo, sizeof(SQLINTEGER), NULL);
if (returnCode != SQL_SUCCESS && returnCode != SQL_SUCCESS_WITH_INFO) {
   ODBCError(henv, hdbc, hstmt, NULL, true);
   exit(-1);
}

// 2, 3, 4 - ItemNo, ProdCode, Qty
...

// Prepare stored procedure
returnCode = SQLPrepare(hstmt, (SQLTCHAR *) _T("{call ItemInsert(?, ?, ?, ?)}"),
                        SQL_NTS);

for (unsigned int i = 0; i < order.ItemCount; i++) {
   ItemNo = order.ItemNo[i];
   ProdCode = order.ProdCode[i];
   Qty = order.Qty[i];

   // Execute stored procedure
   returnCode = SQLExecute(hstmt);
   if (returnCode != SQL_SUCCESS && returnCode != SQL_SUCCESS_WITH_INFO) {
      ODBCError(henv, hdbc, hstmt, NULL, true);
      exit(-1);
   }
}
```

## <a name="using-odbc-to-execute-a-natively-compiled-stored-procedure"></a>ODBC を使用したネイティブ コンパイル ストアド プロシージャの実行

このサンプルでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを使用してパラメーターをバインドし、ストアド プロシージャを実行する方法について説明します。 このサンプルは、直接実行を使用して単一の注文を挿入し、準備実行を使用して注文の明細を挿入するコンソール アプリケーションにコンパイルされます。

このサンプルを実行するには:

1. メモリ最適化データ ファイル グループが含まれるサンプル データベースを作成します。 メモリ最適化データ ファイルグループが含まれるデータベースを作成する方法については、「 [メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャの作成](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)」を参照してください。

2. データベースを参照する PrepExecSample という ODBC データ ソースを作成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ドライバーを使用します。 また、サンプルを変更して [Microsoft ODBC Driver for SQL Server](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)を使用できます。

3. サンプル データベースに [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト (下記) を実行します。

4. サンプルをコンパイルして実行します。

5. テーブルの内容を照会することで、プログラムが正常に実行されたことを確認します。

    ```sql
    SELECT * FROM dbo.Ord;
    ```

    ```sql
    SELECT * FROM dbo.Item;
    ```

## <a name="preliminary-transact-sql"></a>準備の Transact-SQL

以下は、メモリ最適化データベース オブジェクトを作成する [!INCLUDE[tsql](../../includes/tsql-md.md)] コード リストです。

```sql
IF EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID=OBJECT_ID('dbo.OrderInsert'))
DROP PROCEDURE dbo.OrderInsert;  
GO
IF EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID=OBJECT_ID('dbo.ItemInsert'))
DROP PROCEDURE dbo.ItemInsert;  
GO  
IF EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID=OBJECT_ID('dbo.Ord'))
DROP TABLE dbo.Ord;  
GO  
IF EXISTS (SELECT * FROM SYS.OBJECTS WHERE OBJECT_ID=OBJECT_ID('dbo.Item'))
DROP TABLE dbo.Item;  
GO

CREATE TABLE dbo.Ord  
(  
   OrdNo INTEGER NOT NULL PRIMARY KEY NONCLUSTERED,  
   OrdDate DATETIME NOT NULL,   
   CustCode VARCHAR(5) NOT NULL)   
 WITH (MEMORY_OPTIMIZED=ON);  
GO  
  
CREATE TABLE dbo.Item  
(  
   OrdNo INTEGER NOT NULL,   
   ItemNo INTEGER NOT NULL,   
   ProdCode INTEGER NOT NULL,   
   Qty INTEGER NOT NULL,  
   CONSTRAINT PK_Item PRIMARY KEY NONCLUSTERED (OrdNo,ItemNo))  
   WITH (MEMORY_OPTIMIZED=ON);  
GO  
  
CREATE PROCEDURE dbo.OrderInsert(
    @OrdNo INTEGER, @CustCode VARCHAR(5))  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
   (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = 'english')  
  
  DECLARE @OrdDate datetime = GETDATE();  
  INSERT INTO dbo.Ord (OrdNo, CustCode, OrdDate)
  VALUES (@OrdNo, @CustCode, @OrdDate);
END;  
GO  
  
CREATE PROCEDURE dbo.ItemInsert(
    @OrdNo INTEGER, @ItemNo INTEGER, @ProdCode INTEGER, @Qty INTEGER)
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
   (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  
  INSERT INTO dbo.Item (OrdNo, ItemNo, ProdCode, Qty)
  VALUES (@OrdNo, @ItemNo, @ProdCode, @Qty)
END  
GO  
```

## <a name="c-code"></a>C コード

以下は、C コード リストです。

```cpp
// compile with: user32.lib odbc32.lib
#pragma once  
#define WIN32_LEAN_AND_MEAN  // Exclude rarely-used stuff from Windows headers.
#include <stdio.h>  
#include <stdlib.h>  
#include <tchar.h>  
#include <windows.h>  
#include "sql.h"  
#include "sqlext.h"  
#include "sqlncli.h"  
  
// cardinality of order item related array variables
#define ITEM_ARRAY_SIZE 20  
  
// struct to pass order entry data  
typedef struct OrdEntry_struct {  
   SQLINTEGER OrdNo;  
   SQLTCHAR CustCode[6];  
   SQLUINTEGER ItemCount;  
   SQLINTEGER ItemNo[ITEM_ARRAY_SIZE];  
   SQLINTEGER ProdCode[ITEM_ARRAY_SIZE];  
   SQLINTEGER Qty[ITEM_ARRAY_SIZE];  
} OrdEntryData;  
  
SQLHANDLE henv, hdbc, hstmt;  
  
void ODBCError(
      SQLHANDLE henv, SQLHANDLE hdbc,
      SQLHANDLE hstmt, SQLHANDLE hdesc,
      bool ShowError)
{  
   SQLRETURN r = 0;  
   SQLTCHAR szSqlState[6] = {0};  
   SQLINTEGER fNativeError = 0;  
   SQLTCHAR szErrorMsg[256] = {0};  
   SQLSMALLINT cbErrorMsgMax = sizeof(szErrorMsg) - 1;
   SQLSMALLINT cbErrorMsg = 0;  
   TCHAR text[1024] = {0}, title[256] = {0};  
  
   if (hdesc != NULL)  
      r = SQLGetDiagRec(SQL_HANDLE_DESC, hdesc, 1, szSqlState,
              &fNativeError, szErrorMsg, cbErrorMsgMax, &cbErrorMsg);
   else {  
      if (hstmt != NULL)  
         r = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, 1, szSqlState,
                 &fNativeError, szErrorMsg, cbErrorMsgMax, &cbErrorMsg);
      else {  
         if (hdbc != NULL)  
            r = SQLGetDiagRec(SQL_HANDLE_DBC, hdbc, 1, szSqlState,
                    &fNativeError, szErrorMsg, cbErrorMsgMax, &cbErrorMsg);
         else  
            r = SQLGetDiagRec(SQL_HANDLE_ENV, henv, 1, szSqlState,
                    &fNativeError, szErrorMsg, cbErrorMsgMax, &cbErrorMsg);
      }  
   }  
  
   if (ShowError) {  
      _sntprintf_s(title, _countof(title), _TRUNCATE, _T("ODBC Error %i"),
                      fNativeError);  
      _sntprintf_s(text, _countof(text), _TRUNCATE, _T("[%s] - %s"),
                      szSqlState, szErrorMsg);  
  
      MessageBox(NULL, (LPCTSTR) text, (LPCTSTR) _T("ODBC Error"), MB_OK);
   }  
}  
  
void connect() {  
   SQLRETURN r;  
  
   r = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &henv);  
  
   // This is an ODBC v3 application  
   r = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, 0);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, NULL, NULL, NULL, true);  
      exit(-1);  
   }  
  
   r = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
   // Run in ANSI/implicit transaction mode  
   r = SQLSetConnectAttr(hdbc, SQL_ATTR_AUTOCOMMIT,
                          (SQLPOINTER) SQL_AUTOCOMMIT_OFF, SQL_IS_INTEGER);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, NULL, NULL, NULL, true);  
      exit(-1);  
   }  
  
   TCHAR szConnStrIn[256] = _T("DSN=PrepExecSample");  
  
   r = SQLDriverConnect(hdbc, NULL, (SQLTCHAR *) szConnStrIn, SQL_NTS,
                          NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, NULL, NULL, true);  
      exit(-1);  
   }  
}  
  
void setup_ODBC_basics() {  
   SQLRETURN r;  
  
   r = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);  
      exit(-1);  
   }  
}  
  
void OrdEntry(OrdEntryData& order) {  
   // Simple order entry  
   SQLRETURN r;  
  
   SQLINTEGER ItemNo, ProdCode, Qty;  
  
   // Bind parameters for the Order  
   // 1 - OrdNo input  
   r = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER,
                          0, 0, &order.OrdNo, sizeof(SQLINTEGER), NULL);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // 2 - Custcode input  
   r = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT,SQL_C_TCHAR, SQL_VARCHAR, 5, 0,
                          &order.CustCode, sizeof(order.CustCode), NULL);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // Insert the order  
   r = SQLExecDirect(hstmt, (SQLTCHAR *) _T("{call OrderInsert(?, ?)}"),SQL_NTS);
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // Flush results & reset hstmt  
   r = SQLMoreResults(hstmt);  
   if (r != SQL_NO_DATA) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   r = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // Bind parameters for the Items  
   // 1 - OrdNo   
   r = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 10, 0,
                          &order.OrdNo, sizeof(SQLINTEGER), NULL);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // 2 - ItemNo   
   r = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 10, 0,
                          &ItemNo, sizeof(SQLINTEGER), NULL);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // 3 - ProdCode  
   r = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 10, 0,
                          &ProdCode, sizeof(SQLINTEGER), NULL);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // 4 - Qty  
   r = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 10, 0,
                          &Qty, sizeof(SQLINTEGER), NULL);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // Prepare to insert items one at a time  
   r = SQLPrepare(hstmt, (SQLTCHAR *) _T("{call ItemInsert(?, ?, ?, ?)}"),SQL_NTS);
  
   for (unsigned int i = 0; i < order.ItemCount; i++) {  
  ItemNo = order.ItemNo[i];  
      ProdCode = order.ProdCode[i];  
      Qty = order.Qty[i];  
      r = SQLExecute(hstmt);  
      if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
         ODBCError(henv, hdbc, hstmt, NULL, true);   
         exit(-1);  
      }  
   }  
  
   // Flush results & reset hstmt  
   r = SQLMoreResults(hstmt);  
   if (r != SQL_NO_DATA) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   r = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
  
   // Commit the transaction  
   r = SQLEndTran(SQL_HANDLE_DBC, hdbc, SQL_COMMIT);  
   if (r != SQL_SUCCESS && r != SQL_SUCCESS_WITH_INFO) {  
      ODBCError(henv, hdbc, hstmt, NULL, true);   
      exit(-1);  
   }  
}  
  
void testOrderEntry() {  
  
   OrdEntryData order;  
  
   order.OrdNo = 1;  
   _tcscpy_s((TCHAR *) order.CustCode, _countof(order.CustCode), _T("CUST1"));
   order.ItemNo[0] = 1;  
   order.ProdCode[0] = 10;  
   order.Qty[0] = 1;  
   order.ItemNo[1] = 2;  
   order.ProdCode[1] = 20;  
   order.Qty[1] = 2;  
   order.ItemNo[2] = 3;  
   order.ProdCode[2] = 30;  
   order.Qty[2] = 3;  
   order.ItemNo[3] = 4;  
   order.ProdCode[3] = 40;  
   order.Qty[3] = 4;  
   order.ItemCount = 4;  
  
   OrdEntry(order);  
}  
int _tmain() {  
   connect();  
   setup_ODBC_basics();  
  
   testOrderEntry();  
}  
```

## <a name="see-also"></a>参照
[ネイティブ コンパイル ストアド プロシージャ](./a-guide-to-query-processing-for-memory-optimized-tables.md)