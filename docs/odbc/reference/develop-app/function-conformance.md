---
description: 関数の適合性
title: 関数の準拠 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ff61c62b18f531eaad7cc822f99c7065fcba129
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465794"
---
# <a name="function-conformance"></a>関数の適合性
次の表は、各 ODBC 関数が適切に定義されている場合の準拠レベルを示しています。  
  
|機能|一致レベル|  
|--------------|-----------------------|  
|**SQLAllocHandle**|コア|  
|**SQLBindCol**|コア|  
|**SQLBindParameter**|コア [1]|  
|**SQLBrowseConnect**|[レベル 1]|  
|**SQLBulkOperations**|[レベル 1]|  
|**SQLCancel**|コア [1]|  
|**SQLCloseCursor**|コア|  
|**SQLColAttribute**|コア [1]|  
|**SQLColumnPrivileges**|[レベル 2]|  
|**SQLColumns**|コア|  
|**SQLConnect**|コア|  
|**SQLCopyDesc**|コア|  
|**SQLDataSources**|コア|  
|**SQLDescribeCol**|コア [1]|  
|**SQLDescribeParam**|[レベル 2]|  
|**SQLDisconnect**|コア|  
|**SQLDriverConnect**|コア|  
|**SQLDrivers**|コア|  
|**SQLEndTran**|コア [1]|  
|**SQLExecDirect**|コア|  
|**SQLExecute**|コア|  
|**SQLFetch**|コア|  
|**SQLFetchScroll**|コア [1]|  
|**SQLForeignKeys**|[レベル 2]|  
|**SQLFreeHandle**|コア|  
|**SQLFreeStmt**|コア|  
|**SQLGetConnectAttr**|コア|  
|**SQLGetCursorName**|コア|  
|**SQLGetData**|コア|  
|**SQLGetDescField**|コア|  
|**SQLGetDescRec**|コア|  
|**SQLGetDiagField**|コア|  
|**SQLGetDiagRec**|コア|  
|**SQLGetEnvAttr**|コア|  
|**SQLGetFunctions**|コア|  
|**SQLGetInfo**|コア|  
|**SQLGetStmtAttr**|コア|  
|**SQLGetTypeInfo**|コア|  
|**SQLMoreResults**|[レベル 1]|  
|**SQLNativeSql**|コア|  
|**SQLNumParams**|コア|  
|**SQLNumResultCols**|コア|  
|**SQLParamData**|コア|  
|**SQLPrepare**|コア|  
|**SQLPrimaryKeys**|[レベル 1]|  
|**SQLProcedureColumns**|[レベル 1]|  
|**SQLProcedures**|[レベル 1]|  
|**SQLPutData**|コア|  
|**SQLRowCount**|コア|  
|**SQLSetConnectAttr**|コア [2]|  
|**SQLSetCursorName**|コア|  
|**SQLSetDescField**|コア [1]|  
|**SQLSetDescRec**|コア|  
|**SQLSetEnvAttr**|コア [2]|  
|**SQLSetPos**|レベル 1 [1]|  
|**SQLSetStmtAttr**|コア [2]|  
|**SQLSpecialColumns**|コア [1]|  
|**SQLStatistics**|コア|  
|**SQLTablePrivileges**|[レベル 2]|  
|**SQLTables**|コア|  
  
 [1] この関数の重要な機能は、より高い準拠レベルでのみ使用できます。  
  
 [2] 特定の属性を既定値以外の値に設定することは、準拠レベルによって異なります。 詳細については、次のセクション「 [属性の準拠](../../../odbc/reference/develop-app/attribute-conformance.md)」を参照してください。
