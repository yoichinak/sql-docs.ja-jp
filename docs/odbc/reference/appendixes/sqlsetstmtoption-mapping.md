---
description: SQLSetStmtOption のマッピング
title: SQLSetStmtOption Mapping |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLSetStmtOption
- SQLSetStmtOption function [ODBC], mapping
ms.assetid: 6a9921aa-8a53-4668-9b13-87164062f1e5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f2c4a65ade202003d454988372895ba40fb6eeef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424880"
---
# <a name="sqlsetstmtoption-mapping"></a>SQLSetStmtOption のマッピング
アプリケーションが ODBC *3. x*ドライバーを介して**SQLSetStmtOption**を呼び出すとき、  
  
```  
SQLSetStmtOption(StatementHandle, fOption, vParam)  
```  
  
 次のようになります。  
  
-   *Foption*が文字列である ODBC 定義のステートメント属性を示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, SQL_NTS)  
    ```  
  
-   *Foption*が32ビットの整数値を返す ODBC 定義のステートメント属性を示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, 0)  
    ```  
  
-   *Foption*がドライバー定義のステートメント属性を示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLSetStmtAttr(StatementHandle, fOption, ValuePtr, BufferLength)  
    ```  
  
 上記の3つのケースでは、 **StatementHandle** 引数は *hstmt*の値に設定され、 *属性* 引数は *foption*の値に設定され、 *valueptr* 引数は *vparam*として値に設定されます。  
  
 ドライバーマネージャーは、ドライバー定義のステートメント属性に文字列または32ビットの整数値が必要かどうかを認識しないため、 **SQLSetStmtAttr**の*stringlength*引数に有効な値を渡す必要があります。 ドライバーがドライバー定義のステートメント属性に対して特殊なセマンティクスを定義しており、 **SQLSetStmtOption**を使用して呼び出す必要がある場合は、 **SQLSetStmtOption**をサポートする必要があります。  
  
 アプリケーションが **SQLSetStmtOption** を呼び出して odbc *3. x* ドライバーでドライバー固有のステートメントオプションを設定し、オプションが odbc *2.x バージョンの* ドライバーで定義されている場合は、odbc *2.x ドライバーの* オプションに新しいマニフェスト定数を定義する必要があります。 **SQLSetStmtOption**の呼び出しで古いマニフェスト定数が使用されている場合、ドライバーマネージャーは*stringlength*引数を0に設定して**SQLSetStmtAttr**を呼び出します。  
  
 アプリケーションが **SQLSetStmtAttr** を呼び出して、ODBC *3. x* ドライバーで SQL_UB_ON に SQL_ATTR_USE_BOOKMARKS を設定すると、SQL_ATTR_USE_BOOKMARKS statement 属性が SQL_UB_FIXED に設定されます。 SQL_UB_ON は SQL_UB_FIXED と同じ定数です。 ドライバーマネージャーは SQL_UB_FIXED をドライバーに渡します。 SQL_UB_FIXED*は odbc 3.x*では非推奨とされましたが、odbc 3.x ドライバーは、固定長のブックマークを使用*する odbc 2.x*アプリケーションを操作するためにそれを実装する必要が*あります。*  
  
 ODBC 3.x ドライバーの場合、ドライバーマネージャーは、*オプション*が SQL_STMT_OPT_MIN と SQL_STMT_OPT_MAX の間にあるかどうか、または SQL_CONNECT_OPT_DRVR_START より大きいかどうかを確認しなく*なります。*
