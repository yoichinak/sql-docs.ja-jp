---
description: ODBC 3.x ドライバーの作成
title: ODBC 3.x ドライバーの記述 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c5fec9b94dbcf60868c44e49d92bddb4bb73e9cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421346"
---
# <a name="writing-odbc-3x-drivers"></a>ODBC 3.x ドライバーの作成
次の表は、ODBC 3 での関数のサポートを示しています。*x* ドライバーと odbc アプリケーション、および odbc 3 に対して関数が呼び出されたときにドライバーマネージャーによって実行されるマッピング。*x* ドライバー。  
  
|機能|サポートされています<br /><br /> による<br /><br /> ODBC 3.*x*<br /><br /> driver?|サポートされています<br /><br /> による<br /><br /> ODBC 3.*x*<br /><br /> 適用?|マップ/サポート<br /><br /> ODBC 3.*x*<br /><br /> ドライバーマネージャーから<br /><br /> ODBC 3.*x* ドライバーですか?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|いいえ|いいえ [1]|はい|  
|**SQLAllocEnv**|いいえ|いいえ [1]|はい|  
|**SQLAllocHandle**|はい|はい|いいえ|  
|**SQLAllocStmt**|いいえ|いいえ [1]|はい|  
|**SQLBindCol**|はい|はい|いいえ|  
|**SQLBindParam**|いいえ|はい [2]|はい|  
|**SQLBindParameter**|はい|はい|いいえ|  
|**SQLBrowseConnect**|はい|はい|いいえ|  
|**SQLBulkOperations**|はい|はい|いいえ|  
|**SQLCancel**|はい|はい|いいえ|  
|**SQLCloseCursor**|はい|はい|いいえ|  
|**SQLColAttribute**|はい|はい|いいえ|  
|**SQLColAttributes**|いいえ [3]|いいえ|はい|  
|**SQLColumnPrivileges**|はい|はい|いいえ|  
|**SQLColumns**|はい|はい|いいえ|  
|**SQLConnect**|はい|はい|いいえ|  
|**SQLCopyDesc**|はい|はい|はい [4]|  
|**SQLDataSources**|いいえ|はい|はい|  
|**SQLDescribeCol**|はい|はい|いいえ|  
|**SQLDescribeParam**|はい|はい|いいえ|  
|**SQLDisconnect**|はい|はい|いいえ|  
|**SQLDriverConnect**|はい|はい|いいえ|  
|**SQLDrivers**|いいえ|はい|はい|  
|**SQLEndTran**|はい|はい|いいえ|  
|**SQLError**|いいえ|いいえ [1]|はい|  
|**SQLExecDirect**|はい|はい|いいえ|  
|**SQLExecute**|はい|はい|いいえ|  
|**SQLExtendedFetch**|はい|いいえ|いいえ|  
|**SQLFetch**|はい|はい|いいえ|  
|**SQLFetchScroll**|はい|はい|いいえ|  
|**SQLForeignKeys**|はい|はい|いいえ|  
|**SQLFreeConnect**|いいえ|はい [1]|はい|  
|**SQLFreeEnv**|いいえ|はい [1]|はい|  
|**SQLFreeHandle**|はい|はい|いいえ|  
|**SQLFreeStmt**|はい|はい|いいえ|  
|**SQLGetConnectAttr**|はい|はい|いいえ|  
|**SQLGetConnectOption**|[5]|いいえ [1]|はい|  
|**SQLGetCursorName**|はい|はい|いいえ|  
|**SQLGetData**|はい|はい|いいえ|  
|**SQLGetDescField**|はい|はい|いいえ|  
|**SQLGetDescRec**|はい|はい|いいえ|  
|**SQLGetDiagField**|はい|はい|いいえ|  
|**SQLGetDiagRec**|はい|はい|いいえ|  
|**SQLGetEnvAttr**|はい|はい|いいえ|  
|**SQLGetFunctions**|いいえ [6]|はい|はい|  
|**SQLGetInfo**|はい|はい|いいえ|  
|**SQLGetStmtAttr**|はい|はい|いいえ|  
|**SQLGetStmtOption**|[5]|いいえ [1]|はい|  
|**SQLGetTypeInfo**|はい|はい|いいえ|  
|**SQLMoreResults**|はい|はい|いいえ|  
|**SQLNativeSql**|はい|はい|いいえ|  
|**SQLNumParams**|はい|はい|いいえ|  
|**SQLNumResultCols**|はい|はい|いいえ|  
|**SQLParamData**|はい|はい|いいえ|  
|**SQLParamOptions**|いいえ|いいえ|はい|  
|**SQLPrepare**|はい|はい|いいえ|  
|**SQLPrimaryKeys**|はい|はい|いいえ|  
|**SQLProcedureColumns**|はい|はい|いいえ|  
|**SQLProcedures**|はい|はい|いいえ|  
|**SQLPutData**|はい|はい|いいえ|  
|**SQLRowCount**|はい|はい|いいえ|  
|**SQLSetConnectAttr**|はい|はい|いいえ|  
|**SQLSetConnectOption**|[5]|いいえ [1]|はい|  
|**SQLSetCursorName**|はい|はい|いいえ|  
|**SQLSetDescField**|はい|はい|いいえ|  
|**SQLSetDescRec**|はい|はい|いいえ|  
|**SQLSetEnvAttr**|はい|はい|いいえ|  
|**SQLSetPos**|はい|はい|いいえ|  
|**SQLSetParam**|いいえ|いいえ|はい|  
|**SQLSetScrollOption**|はい|はい|いいえ|  
|**SQLSetStmtAttr**|はい|はい|いいえ|  
|**SQLSetStmtOption**|[5]|いいえ [1]|はい|  
|**SQLSpecialColumns**|はい|はい|いいえ|  
|**SQLStatistics**|はい|はい|いいえ|  
|**SQLTablePrivileges**|はい|はい|いいえ|  
|**SQLTables**|はい|はい|いいえ|  
|**SQLTransact**|いいえ|いいえ [1]|はい|  
  
 [1] ODBC 3 では、この関数は非推奨とされます。*x*。 ODBC 3.*x* アプリケーションでは、この関数を使用しないでください。 ただし、Open Group または ISO CLI 準拠アプリケーションでは、この関数を呼び出すことができます。  
  
 [2] ODBC 3.*x*アプリケーションでは、 **SQLBindParam**ではなく**SQLBindParameter**を使用する必要があります。 ただし、Open Group または ISO CLI 準拠アプリケーションでは、この関数を呼び出すことができます。  
  
 [3] ドライバーライターは ODBC 2 に注意する必要があります。*x* 列属性 SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE、および SQL_COLUMN_LENGTH は、 **sqlcolattribute**でサポートされている必要があります。  
  
 [4] 異なるドライバーに属する接続間で記述子をコピーするときに、ドライバーマネージャーによって   **Sqlcopydesc** が部分的に実装されます。 ドライバーは、2つの接続の間で **Sqlcopydesc** をサポートするために必要です。 ドライバーマネージャーによってのみ実装されている **Sqldrivers**などの関数は、この一覧には表示されません。  
  
 [5] 特定の状況下で、ドライバーがこの機能をサポートする必要がある場合があります。 詳細については、この関数のリファレンスページを参照してください。  
  
 [6] ドライバーがサポートする関数のセットが接続への接続によって異なる場合、ドライバーは **Sqlgetfunctions** のサポートを選択できます。
