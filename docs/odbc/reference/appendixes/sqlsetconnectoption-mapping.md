---
description: SQLSetConnectOption のマッピング
title: SQLSetConnectOption Mapping |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c1f1379bfd2bbc2faccf719d68009ed63b350fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476964"
---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption のマッピング
ODBC 2 の場合。*x*アプリケーションは、ODBC 3 *. x*ドライバーを介して**SQLSetConnectOption**を呼び出します。  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 次のようになります。  
  
-   *Foption*が文字列を必要とする ODBC 定義の接続属性を示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   *Foption*が32ビットの整数値を返す ODBC 定義の接続属性を示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   *Foption*がドライバーによって定義された接続属性を示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 上記の3つのケースでは、 *Connectionhandle* 引数は *hdbc*の値に設定され、 *属性* 引数は *foption*の値に設定され、 *valueptr* 引数は *vparam*と同じ値に設定されます。  
  
 ドライバーマネージャーは、ドライバー定義の接続属性に文字列または32ビットの整数値が必要かどうかを認識しないため、 **SQLSetConnectAttr**の*bufferlength*引数に有効な値を渡す必要があります。 ドライバーがドライバーによって定義された接続属性に対して特殊なセマンティクスを定義しており、 **SQLSetConnectOption**を使用して呼び出す必要がある場合は、 **SQLSetConnectOption**をサポートする必要があります。  
  
 ODBC 2 の場合。*x*アプリケーションは、odbc 3 *. x*ドライバーでドライバー固有のステートメントオプションを設定するために**SQLSetConnectOption**を呼び出し、オプションは odbc 2 で定義されています。*x*バージョンのドライバーでは、ODBC 3 *. x*ドライバーのオプションに新しいマニフェスト定数を定義する必要があります。 **SQLSetConnectOption**の呼び出しで古いマニフェスト定数が使用されている場合、ドライバーマネージャーは**stringlength**引数を0に設定して**SQLSetConnectAttr**を呼び出します。  
  
 ODBC 3.x ドライバーの場合、ドライバーマネージャーは、 *Foption*が SQL_CONN_OPT_MIN と SQL_CONN_OPT_MAX の間にあるかどうか、または SQL_CONNECT_OPT_DRVR_START より大きいかどうかを確認しなく*なります。*  
  
## <a name="setting-statement-options-on-the-connection-level"></a>接続レベルでのステートメントオプションの設定  
 ODBC 2 の場合。*x*アプリケーションは、 **SQLSetConnectOption** を呼び出してステートメントオプションを設定することができます。 この処理が完了すると、ドライバーは、後でその接続に割り当てられたすべてのステートメントの既定値としてステートメントオプションを設定します。 ドライバーは、指定された接続に関連付けられている既存のステートメントに対してステートメントオプションを設定するかどうかをドライバーで定義します。  
  
 ODBC 3.x では、この機能は非推奨*となりました。* ODBC 3.x*ドライバーでは、odbc* 2 の設定のみをサポートする必要があります。ODBC 2 を使用する場合は、接続レベルで*x* ステートメント属性を使用します。これを実行する*x* アプリケーション。 ODBC 3 *. x* アプリケーションでは、接続レベルでステートメント属性を設定しないでください。 ODBC 3 *. x* ステートメントの属性は、接続レベルでは設定できません。ただし、接続属性とステートメント属性の両方である SQL_ATTR_METADATA_ID および SQL_ATTR_ASYNC_ENABLE 属性は、接続レベルまたはステートメントレベルのどちらかで設定できます。
