---
description: SQLGetConnectOption のマッピング
title: SQLGetConnectOption Mapping |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cdc5f2e9249e262d0d3da9a69607861bfe64bc25
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202793"
---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption のマッピング
アプリケーションが ODBC *3. x* ドライバーを介して **SQLGetConnectOption** を呼び出すとき、  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 は次のようにマップされます。  
  
-   *Foption* が文字列を返す ODBC 定義の接続オプションを示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   *Foption* が32ビットの整数値を返す ODBC 定義の接続オプションを示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   *Foption* がドライバーで定義されたステートメントオプションを示す場合、ドライバーマネージャーはを呼び出します。  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 上記の3つのケースでは、 *Connectionhandle* 引数は *hdbc* の値に設定され、 *属性* 引数は *foption* の値に設定され、 *valueptr* 引数は *pvparam* と同じ値に設定されます。  
  
 ODBC で定義された文字列接続オプションの場合、ドライバーマネージャーは、 **Sqlgetconnectattr** への呼び出しで *bufferlength* 引数を事前に定義された最大長 (SQL_MAX_OPTION_STRING_LENGTH) に設定します。文字列以外の接続オプションでは、 *Bufferlength* は0に設定されます。  
  
 ODBC 3.x ドライバーの場合、ドライバーマネージャーは、*オプション* が SQL_CONN_OPT_MIN と SQL_CONN_OPT_MAX の間にあるかどうか、または SQL_CONNECT_OPT_DRVR_START より大きいかどうかを確認しなく *なります。* ドライバーは、オプション値の有効性を確認する必要があります。
