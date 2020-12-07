---
description: SQLSetConnectAttr (カーソル ライブラリ)
title: SQLSetConnectAttr (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b809ad81e9edaca7fbe7d40952673a1698f113e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424894"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **SQLSetConnectAttr** 関数の使用について説明します。 **SQLSetConnectAttr**の一般的な情報については、「 [SQLSetConnectAttr 関数](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)」を参照してください。  
  
 アプリケーションは、SQL_ATTR_ODBC_CURSORS 属性を使用して **SQLSetConnectAttr** を呼び出し、カーソルライブラリを常に使用するかどうかを指定します。これは、ドライバーがスクロール可能なカーソルをサポートしていない場合、または使用しない場合に使用します。 カーソルライブラリでは、 **SQLGetInfo**の SQL_STATIC_CURSOR_ATTRIBUTES1 情報型に対して SQL_CA1_RELATIVE が返された場合に、ドライバーがスクロール可能なカーソルをサポートしていると想定しています。  
  
 アプリケーションは**SQLSetConnectAttr**を呼び出して、接続を割り当て、データソースに接続する前に、SQL_HANDLE_DBC の*handletype*を使用して**SQLAllocHandle**を呼び出した後、カーソルライブラリの使用を指定する必要があります。 接続がまだアクティブであるときに、アプリケーションが SQL_ATTR_ODBC_CURSORS 属性を使用して **SQLSetConnectAttr** を呼び出すと、カーソルライブラリがエラーを返します。  
  
 接続に関連付けられているすべてのステートメントについて、カーソルライブラリでサポートされているステートメント属性を設定するには、データソースに接続してからカーソルを開く前に、そのステートメント属性に対して **SQLSetConnectAttr** を呼び出す必要があります。 アプリケーションがステートメント属性を使用して **SQLSetConnectAttr** を呼び出し、その接続に関連付けられているステートメントでカーソルが開いている場合、カーソルを閉じて再度開くまで、ステートメント属性はそのステートメントに適用されません。
