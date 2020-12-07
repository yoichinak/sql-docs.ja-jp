---
description: ユーザーが入力した SQL ステートメント
title: ユーザーによって入力された SQL ステートメント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- user-entered SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], entered by user
ms.assetid: 109af162-93ba-425a-8fe5-49c7dc7cc784
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d7d7ee7ffc2a4c949173c3eee888e4c41b9e741
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424544"
---
# <a name="sql-statements-entered-by-the-user"></a>ユーザーが入力した SQL ステートメント
アドホック分析を実行するアプリケーションでは、通常、ユーザーが直接 SQL ステートメントを入力できるようにすることもできます。 次に例を示します。  
  
```  
SQLCHAR *     Statement, SqlState[6], Msg[SQL_MAX_MESSAGE_LENGTH];  
SQLSMALLINT   i, MsgLen;  
SQLINTEGER    NativeError;  
SQLRETURN     rc1, rc2;  
  
// Prompt user for SQL statement.  
GetSQLStatement(Statement);  
  
// Execute the statement directly. Because it will be executed only once,  
// do not prepare it.  
rc1 = SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Process any errors or returned information.  
if ((rc1 == SQL_ERROR) || rc1 == SQL_SUCCESS_WITH_INFO) {  
   i = 1;  
   while ((rc2 = SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, SqlState, &NativeError,  
         Msg, sizeof(Msg), &MsgLen)) != SQL_NO_DATA) {  
      DisplayError(SqlState, NativeError, Msg, MsgLen);  
      i++;  
   }  
}  
```  
  
 この方法では、アプリケーションのコーディングが簡単になります。アプリケーションでは、ステートメントの有効性を確認するために、ユーザーが SQL ステートメントとデータソースを作成することに依存しています。 複雑な SQL を適切に公開するグラフィカルユーザーインターフェイスを作成するのは困難なので、SQL ステートメントのテキストを入力するようユーザーに求めるだけで、代替手段として使用することもできます。 ただし、これには、SQL だけでなく、クエリ対象のデータソースのスキーマも把握しておく必要があります。 アプリケーションによっては、グラフィカルユーザーインターフェイスが用意されており、ユーザーは基本的な SQL ステートメントを作成できます。また、ユーザーがこのステートメントを変更できるテキストインターフェイスも用意されています。
