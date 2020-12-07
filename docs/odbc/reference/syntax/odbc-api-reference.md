---
description: ODBC API リファレンス
title: ODBC API リファレンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apitype: dllExport
ms.assetid: b7a49774-f458-44ce-9a04-a0457501405b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1627838d3f34f8092dce2806a1b1d8f885b9bf6a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476183"
---
# <a name="odbc-api-reference"></a>ODBC API リファレンス
このセクションのトピックでは、各 ODBC 関数についてアルファベット順に説明します。 各関数は、C プログラミング言語の関数として定義されています。 説明には次のものがあります。  
  
-   目的  
  
-   ODBC のバージョン  
  
-   標準 CLI 準拠レベル  
  
-   構文  
  
-   引数  
  
-   戻り値  
  
-   診断  
  
-   使用法と実装に関するコメント  
  
-   コードの例  
  
-   関連する関数への参照  
  
 標準 CLI 準拠レベルは、次のいずれかになります。 ISO 92、Open Group、ODBC、または非推奨です。 Open Group は ISO 92 の純粋なスーパーセットであるため、ISO 92-準拠としてタグ付けされた関数は、オープングループバージョン1でも表示されます。 Open Group 準拠としてタグ付けされた関数は、ODBC 3 にも表示されます。*x*(ODBC 3)。*x* は、オープングループバージョン1の純粋スーパーセットです。 ODBC 準拠としてタグ付けされた関数は、標準ではありません。 非推奨としてタグ付けされた関数は、ODBC 3 では非推奨となりました。*x*。  
  
 診断情報の処理については、 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) 関数の説明を参照してください。 SQLSTATE 値に関連付けられたテキストは、条件の説明を提供するために含まれていますが、特定のテキストを指定するためのものではありません。  
  
> [!NOTE]  
>  ODBC 関数に関するドライバー固有の情報については、ドライバーの「」セクションを参照してください。  
  
 このセクションには、次の関数に関するトピックが含まれています。  
  
-   [SQLAllocConnect 関数](../../../odbc/reference/syntax/sqlallocconnect-function.md)  
  
-   [SQLAllocEnv 関数](../../../odbc/reference/syntax/sqlallocenv-function.md)  
  
-   [SQLAllocHandle 関数](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLAllocStmt 関数](../../../odbc/reference/syntax/sqlallocstmt-function.md)  
  
-   [SQLBindCol 関数](../../../odbc/reference/syntax/sqlbindcol-function.md)  
  
-   [SQLBindParameter 関数](../../../odbc/reference/syntax/sqlbindparameter-function.md)  
  
-   [SQLBrowseConnect 関数](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
  
-   [SQLBulkOperations 関数](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
  
-   [SQLCancel 関数](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle 関数](../../../odbc/reference/syntax/sqlcancelhandle-function.md)  
  
-   [SQLCloseCursor 関数](../../../odbc/reference/syntax/sqlclosecursor-function.md)  
  
-   [SQLColAttribute 関数](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
  
-   [SQLColAttributes 関数](../../../odbc/reference/syntax/sqlcolattributes-function.md)  
  
-   [SQLColumnPrivileges 関数](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
  
-   [SQLColumns 関数](../../../odbc/reference/syntax/sqlcolumns-function.md)  
  
-   [SQLCompleteAsync 関数](../../../odbc/reference/syntax/sqlcompleteasync-function.md)  
  
-   [SQLConnect 関数](../../../odbc/reference/syntax/sqlconnect-function.md)  
  
-   [SQLCopyDesc 関数](../../../odbc/reference/syntax/sqlcopydesc-function.md)  
  
-   [SQLDataSources 関数](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDescribeCol 関数](../../../odbc/reference/syntax/sqldescribecol-function.md)  
  
-   [SQLDescribeParam 関数](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
  
-   [SQLDisconnect 関数](../../../odbc/reference/syntax/sqldisconnect-function.md)  
  
-   [SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
-   [SQLDrivers 関数](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLEndTran 関数](../../../odbc/reference/syntax/sqlendtran-function.md)  
  
-   [SQLError 関数](../../../odbc/reference/syntax/sqlerror-function.md)  
  
-   [SQLExecDirect 関数](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
  
-   [SQLExecute 関数](../../../odbc/reference/syntax/sqlexecute-function.md)  
  
-   [SQLExtendedFetch 関数](../../../odbc/reference/syntax/sqlextendedfetch-function.md)  
  
-   [SQLFetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)  
  
-   [SQLFetchScroll 関数](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
-   [SQLForeignKeys 関数](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
  
-   [SQLFreeConnect 関数](../../../odbc/reference/syntax/sqlfreeconnect-function.md)  
  
-   [SQLFreeEnv 関数](../../../odbc/reference/syntax/sqlfreeenv-function.md)  
  
-   [SQLFreeHandle 関数](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
-   [SQLFreeStmt 関数](../../../odbc/reference/syntax/sqlfreestmt-function.md)  
  
-   [SQLGetConnectAttr 関数](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLGetConnectOption 関数](../../../odbc/reference/syntax/sqlgetconnectoption-function.md)  
  
-   [SQLGetCursorName 関数](../../../odbc/reference/syntax/sqlgetcursorname-function.md)  
  
-   [SQLGetData 関数](../../../odbc/reference/syntax/sqlgetdata-function.md)  
  
-   [SQLGetDescField 関数](../../../odbc/reference/syntax/sqlgetdescfield-function.md)  
  
-   [SQLGetDescRec 関数](../../../odbc/reference/syntax/sqlgetdescrec-function.md)  
  
-   [SQLGetDiagField 関数](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec 関数](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLGetEnvAttr 関数](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetFunctions 関数](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLGetInfo 関数](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetStmtAttr 関数](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
-   [SQLGetStmtOption 関数](../../../odbc/reference/syntax/sqlgetstmtoption-function.md)  
  
-   [SQLGetTypeInfo 関数](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
-   [SQLMoreResults 関数](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
  
-   [SQLNativeSql 関数](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
-   [SQLNumParams 関数](../../../odbc/reference/syntax/sqlnumparams-function.md)  
  
-   [SQLNumResultCols 関数](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
  
-   [SQLParamData 関数](../../../odbc/reference/syntax/sqlparamdata-function.md)  
  
-   [SQLParamOptions 関数](../../../odbc/reference/syntax/sqlparamoptions-function.md)  
  
-   [SQLPrepare 関数](../../../odbc/reference/syntax/sqlprepare-function.md)  
  
-   [SQLPrimaryKeys 関数](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
  
-   [SQLProcedureColumns 関数](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
  
-   [SQLProcedures 関数](../../../odbc/reference/syntax/sqlprocedures-function.md)  
  
-   [SQLPutData 関数](../../../odbc/reference/syntax/sqlputdata-function.md)  
  
-   [SQLRowCount 関数](../../../odbc/reference/syntax/sqlrowcount-function.md)  
  
-   [SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
  
-   [SQLSetConnectOption 関数](../../../odbc/reference/syntax/sqlsetconnectoption-function.md)  
  
-   [SQLSetCursorName 関数](../../../odbc/reference/syntax/sqlsetcursorname-function.md)  
  
-   [SQLSetDescField 関数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
-   [SQLSetDescRec 関数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)  
  
-   [SQLSetEnvAttr 関数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)  
  
-   [SQLSetParam 関数](../../../odbc/reference/syntax/sqlsetparam-function.md)  
  
-   [SQLSetPos 関数](../../../odbc/reference/syntax/sqlsetpos-function.md)  
  
-   [SQLSetScrollOptions 関数](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)  
  
-   [SQLSetStmtAttr 関数](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)  
  
-   [SQLSetStmtOption 関数](../../../odbc/reference/syntax/sqlsetstmtoption-function.md)  
  
-   [SQLSpecialColumns 関数](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
  
-   [SQLStatistics 関数](../../../odbc/reference/syntax/sqlstatistics-function.md)  
  
-   [SQLTablePrivileges 関数](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
  
-   [SQLTables 関数](../../../odbc/reference/syntax/sqltables-function.md)  
  
-   [SQLTransact 関数](../../../odbc/reference/syntax/sqltransact-function.md)
