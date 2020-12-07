---
description: 接続属性
title: 接続属性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection attributes
- ODBC drivers [ODBC], connection attributes
- connecting to data source [ODBC], connection attributes
- connection attributes [ODBC]
- connecting to driver [ODBC], connection attributes
ms.assetid: e6d03089-30a3-4627-a642-591ba0980894
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a7db2fb6361f114f4864436116f5b0f2f5651e79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424804"
---
# <a name="connection-attributes"></a>接続属性
接続属性は接続の特性です。 たとえば、トランザクションは接続レベルで行われるので、トランザクション分離レベルは 1 つの接続属性になります。 同様に、ログインタイムアウト、または接続を試行してからタイムアウトするまでの待機時間 (秒数) は接続属性です。  
  
 **SQLSetConnectAttr**を使用して接続属性を設定し、 **Sqlgetconnectattr**を使用してその現在の設定を取得します。 ドライバーが読み込まれる前に **SQLSetConnectAttr** が呼び出された場合、ドライバーマネージャーはその属性を接続構造に格納し、接続プロセスの一部としてドライバーに設定します。 アプリケーションで接続属性を設定する必要はありません。すべての接続属性には既定値があり、その一部はドライバー固有です。  
  
 接続属性は、接続の前または後に設定することも、属性とドライバーに応じて設定することもできます。 ログインタイムアウト (SQL_ATTR_LOGIN_TIMEOUT) は接続プロセスに適用され、接続前に設定されている場合にのみ有効です。 Odbc カーソルライブラリはドライバーマネージャーとドライバーの間に存在するため、odbc カーソルライブラリを使用するかどうかを指定する属性 (SQL_ATTR_ODBC_CURSORS) とネットワークパケットサイズ (SQL_ATTR_PACKET_SIZE) は、接続前に設定する必要があります。これは、ODBC カーソルライブラリがドライバーマネージャーとドライバーの間に存在するため、ドライバーの前に読み込む必要があるためです。  
  
 データソースが読み取り専用または読み取り/書き込み可能 (SQL_ATTR_ACCESS_MODE) かどうかを指定する属性と、接続の前または後に現在のカタログ (SQL_ATTR_CURRENT_CATALOG) を設定できるかどうかを指定する属性。ドライバーによって異なります。 ただし、接続後のドライバーによっては、接続後の変更がサポートされないため、相互運用可能なアプリケーションは接続前にこれらを設定します。  
  
 接続属性の中には、接続が確立される前に既定値が設定されているものもあれば、そうでないものもあります。 SQL_ATTR_ACCESS_MODE、SQL_ATTR_AUTOCOMMIT、SQL_ATTR_LOGIN_TIMEOUT、SQL_ATTR_ODBC_CURSORS、SQL_ATTR_TRACE、および SQL_ATTR_TRACEFILE です。  
  
 変換接続属性 (SQL_ATTR_TRANSLATE_DLL および SQL_ATTR_TRANSLATE_OPTION) は、接続後に設定する必要があります。  
  
 その他のすべての接続属性は、いつでも設定できます。 詳細については、 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md) 関数の説明を参照してください。 ( **SQLSetEnvAttr**を呼び出すことによって、環境レベルで接続属性を設定することはできません)。
