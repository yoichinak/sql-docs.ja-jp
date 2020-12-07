---
description: SQLSetConnectAttrForDbcInfo 関数
title: SQLSetConnectAttrForDbcInfo 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttrForDbcInfo function [ODBC]
ms.assetid: a28fadb9-b998-472a-b252-709507e92005
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7380ba8682deb7424c363b28d42ecf3980755daf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499562"
---
# <a name="sqlsetconnectattrfordbcinfo-function"></a>SQLSetConnectAttrForDbcInfo 関数
**互換性**  
 導入されたバージョン: ODBC 3.81 標準準拠: ODBC  
  
 **まとめ**  
 **SQLSetConnectAttrForDbcInfo** は **SQLSetConnectAttr**と同じですが、接続ハンドルではなく、接続情報トークンの属性を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN  SQLSetConnectAttrForDbcInfo(  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                SQLINTEGER            Attribute,  
                SQLPOINTER            ValuePtr,  
                SQLINTEGER            StringLength );  
```  
  
## <a name="arguments"></a>引数  
 *hDbcInfoToken*  
 代入トークンハンドル。  
  
 *属性*  
 代入設定する属性。 有効な属性の一覧は、ドライバー固有であり、 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)の場合と同じです。  
  
 *ValuePtr*  
 代入 *属性*に関連付けられる値へのポインター。 *属性*の値に応じて、 *valueptr*は32ビットの符号なし整数値になるか、null で終わる文字列を指します。 *属性*引数がドライバー固有の値の場合、 *valueptr*の値は符号付き整数であることに注意してください。  
  
 *StringLength*  
 代入 *属性* が ODBC 定義の属性であり、 *valueptr* が文字列またはバイナリバッファーを指している場合、この引数は **valueptr*の長さである必要があります。 文字列データの場合、この引数には文字列のバイト数を含める必要があります。  
  
 *属性*が ODBC 定義の属性であり、 *valueptr*が整数の場合、 *stringlength*は無視されます。  
  
 *属性*がドライバーで定義された属性の場合、アプリケーションは*stringlength*引数を設定することによって、ドライバーマネージャーに対する属性の性質を示します。 *Stringlength* には次の値を指定できます。  
  
-   *Valueptr*が文字列へのポインターである場合、 *stringlength*は文字列または SQL_NTS の長さを示します。  
  
-   *Valueptr*がバイナリバッファーへのポインターである場合、アプリケーションは、SQL_LEN_BINARY_ATTR (*長さ*) マクロの結果を*stringlength*に配置します。 これにより、 *文字列長*に負の値が挿入されます。  
  
-   *Valueptr*が文字列またはバイナリ文字列以外の値へのポインターである場合、 *stringlength*には SQL_IS_POINTER 値を指定する必要があります。  
  
-   *Valueptr*に固定長の値が含まれている場合は、必要に応じて*stringlength*が SQL_IS_INTEGER か SQL_IS_UINTEGER になります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)と同じですが、Driver Manager では SQL_HANDLE_DBC_INFO_TOKEN の**Handletype**と*Hdbcinfotoken*の**ハンドル**が使用される点が異なります。  
  
## <a name="remarks"></a>解説  
 **SQLSetConnectAttrForDbcInfo** は **SQLSetConnectAttr**と同じですが、接続ハンドルではなく、接続情報トークンの属性を設定します。 たとえば、 **SQLSetConnectAttr** が属性を認識しない場合、 **SQLSetConnectAttrForDbcInfo** はその属性の SQL_ERROR も返す必要があります。  
  
 ドライバーが SQL_ERROR または SQL_INVALID_HANDLE を返すたびに、ドライバーはこの属性を無視してプール ID を計算する必要があります。 また、ドライバーマネージャーは *Hdbcinfotoken*から診断情報を取得し、 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) と [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)のアプリケーションに SQL_SUCCESS_WITH_INFO を返します。 そのため、アプリケーションでは、一部の属性を設定できない理由に関する詳細を取得できます。  
  
 アプリケーションでは、この関数を直接呼び出すことはできません。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ODBC ドライバーの開発には sqlspi. h を含めます。  
  
## <a name="see-also"></a>関連項目  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
