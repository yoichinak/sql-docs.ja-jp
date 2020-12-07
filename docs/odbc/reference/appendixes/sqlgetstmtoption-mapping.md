---
description: SQLGetStmtOption のマッピング
title: SQLGetStmtOption Mapping |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01d099c4802c05f8e5bd1e093987f2c3993ac9c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448982"
---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption のマッピング
アプリケーションが **SQLGetStmtOption** をサポートしてい *ない ODBC 3.x* ドライバーへの呼び出しを行う場合、  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 次のようになります。  
  
-   *Foption*が文字列を返す ODBC 定義のステートメントオプションを示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   *Foption*が32ビットの整数値を返す ODBC 定義のステートメントオプションを示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   *Foption*がドライバーで定義されたステートメントオプションを示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 上記の3つのケースでは、 *StatementHandle* 引数が *hstmt*の値に設定され、 *属性* 引数が *foption*の値に設定され、 *valueptr* 引数が *pvparam*と同じ値に設定されています。  
  
 ODBC で定義された文字列接続オプションの場合、ドライバーマネージャーは、 **Sqlgetconnectattr**への呼び出しで*bufferlength*引数を事前に定義された最大長 (SQL_MAX_OPTION_STRING_LENGTH) に設定します。文字列以外の接続オプションでは、 *Bufferlength*は0に設定されます。  
  
 SQL_GET_BOOKMARK statement オプションは *、ODBC 3.x*では非推奨とされました。 ODBC 3.x ドライバーが SQL_GET_BOOKMARK を使用 *する odbc 2.x* アプリケーション *を* 操作するには、SQL_GET_BOOKMARK をサポートしている必要があります。 *Odbc 2.x ドライバーが*odbc 2.x アプリケーションを操作するには、SQL_USE_BOOKMARKS を SQL_UB_ON に設定し、固定長のブックマークを公開する必要が*あります。* ODBC 2.x ドライバーが、固定長のブックマークではなく可変長のブックマークのみをサポートしている場合は、ODBC *2.x アプリケーションが*SQL_USE_BOOKMARKS を SQL_UB_ON に設定しようとすると、SQLSTATE HYC00 (省略可能な機能は実装されていません) を返す必要が*あります。*  
  
 ODBC 3.x ドライバーの場合、ドライバーマネージャーは、*オプション*が SQL_STMT_OPT_MIN と SQL_STMT_OPT_MAX の間にあるかどうか、または SQL_CONNECT_OPT_DRVR_START より大きいかどうかを確認しなく*なります。* ドライバーはこれを確認する必要があります。
