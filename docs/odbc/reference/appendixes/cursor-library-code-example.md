---
description: カーソル ライブラリのコード例
title: カーソルライブラリのコード例 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], examples
- cursor library [ODBC], examples
ms.assetid: 958a179c-97d9-4717-8d06-d33b715a9773
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8301cf0b608874075c7bc8c66bba25d00f07668d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429684"
---
# <a name="cursor-library-code-example"></a>カーソル ライブラリのコード例
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 次の例では、カーソルライブラリを使用して、ORDERS テーブルから各注文の ID、open date、status を取得します。 その後、20行のデータが表示されます。 ユーザーがこのデータを更新した場合、コードは行セットバッファーを更新し、配置された update ステートメントを実行します。 最後に、スクロールする方向をユーザーに求め、プロセスを繰り返します。  
  
```  
#define ROWS 20  
#define STATUS_LEN 6  
#define OPENDATE_LEN 11  
#define DONE -1  
  
SQLHENV        henv;  
SQLHDBC        hdbc;  
SQLHSTMT       hstmt1, hstmt2;  
SQLRETURN      retcode;  
SQLCHAR        szStatus[ROWS][STATUS_LEN],   
               szOpenDate[ROWS][OPENDATE_LEN];  
SQLCHAR        szNewStatus[STATUS_LEN], szNewOpenDate[OPENDATE_LEN];  
SQLSMALLINT    sOrderID[ROWS], sNewOrderID[ROWS];  
SQLINTEGER     cbStatus[ROWS], cbOrderID[ROWS], cbOpenDate[ROWS];  
SQLUINTEGER    FetchOrientation, crow, FetchOffset, irowUpdt;  
SQLUSMALLINT   RowStatusArray[ROWS];  
  
SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, SQL_OV_ODBC3,0);  
SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
// Specify that the ODBC Cursor Library is always used, then connect.  
  
SQLSetConnectAttr(hdbc, SQL_ATTR_ODBC_CURSORS, SQL_CUR_USE_ODBC);  
SQLConnect(hdbc, "SalesOrder", SQL_NTS,  
            "JohnS", SQL_NTS,  
            "Sesame", SQL_NTS);  
  
if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
   /* Allocate a statement handle for the result set and a statement */  
   /* handle for positioned update statements. */  
  
   SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt1);  
   SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt2);  
  
   /* Specify an updatable static cursor with 20 rows of data. Set */  
   /* the cursor name, execute the SELECT statement, and bind the */  
   /* rowset buffers to result set columns in column-wise fashion. */  
   SQLSetStmtAttr(hstmt1, SQL_ATTR_CONCURRENCY, SQL_CONCUR_VALUES, 0);  
   SQLSetStmtAttr(hstmt1, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_STATIC, 0);  
   SQLSetStmtAttr(hstmt1, SQL_ATTR_ROW_ARRAY_SIZE, ROWS, 0);  
   SQLSetStmtAttr(hstmt1, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   SQLSetStmtAttr(hstmt1, SQL_ATTR_ROWS_FETCHED_PTR, &crow, 0);  
   SQLSetCursorName(hstmt1, "ORDERCURSOR", SQL_NTS);  
   SQLExecDirect(hstmt1,  
                  "SELECT ORDERID, OPENDATE, STATUS FROM ORDERS ",  
                  SQL_NTS);  
   SQLBindCol(hstmt1, 1, SQL_C_SSHORT, sOrderID, 0, cbName);  
   SQLBindCol(hstmt1, 2, SQL_C_CHAR, szOpenDate, OPENDATE_LEN, cbOpenDate);  
   SQLBindCol(hstmt1, 3, SQL_C_CHAR, szStatus, STATUS_LEN, cbStatus);  
  
   /* Fetch the first block of data and display it. Prompt the user */  
   /* for new data values. If the user supplies new values, update */  
   /* the rowset buffers, bind them to the parameters in the update */  
   /* statement, and execute a positioned update on another hstmt. */  
   /* Prompt the user for how to scroll. Fetch and redisplay data as */  
   /* needed. */  
  
   FetchOrientation = SQL_FETCH_FIRST;  
   FetchOffset = 0;  
   do {  
  
      SQLFetchScroll(hstmt1, FetchOrientation, FetchOffset);  
      DisplayRows(sOrderID, szOpenDate, szStatus, RowStatusArray);  
  
      if (PromptUpdate(&irowUpdt,&sNewOrderID,szNewOpenDate,szNewStatus)==TRUE){  
         sOrderID[irowUpdt] = sNewOrderID;  
         cbOrderID[irowUpdt] = 0;  
         strcpy_s((char*)szOpenDate[irowUpdt], _countof(szOpenDate[irowUpdt]), szNewOpenData);  
         cbOpenDate[irowUpdt] = SQL_NTS;  
         strcpy_s((char*)szStatus[irowUpdt], _countof(szStatus[irowUpdt]), szNewStatus);  
         cbStatus[irowUpdt] = SQL_NTS;  
         SQLBindParameter(hstmt2, 1, SQL_PARAM_INPUT,  
                           SQL_C_SSHORT, SQL_INTEGER, 0, 0,  
                           &sOrderID[irowUpdt], 0, &cbOrderID[irowUpdt]);  
         SQLBindParameter(hstmt2, 2, SQL_PARAM_INPUT,  
                           SQL_C_CHAR, SQL_TYPE_DATE, OPENDATE_LEN, 0,  
                           szOpenDate[irowUpdt], OPENDATE_LEN, &cbOpenDate[irowUpdt]);  
         SQLBindParameter(hstmt2, 3, SQL_PARAM_INPUT,  
                           SQL_C_CHAR, SQL_CHAR, STATUS_LEN, 0,  
                           szStatus[irowUpdt], STATUS_LEN, &cbStatus[irowUpdt]);  
         SQLExecDirect(hstmt2,  
                        "UPDATE EMPLOYEE SET ORDERID = ?, OPENDATE = ?, STATUS = ?"  
                        "WHERE CURRENT OF EMPCURSOR",  
                        SQL_NTS);  
      }  
  
   while (PromptScroll(&FetchOrientation, &FetchOffset) != DONE)  
}  
```
