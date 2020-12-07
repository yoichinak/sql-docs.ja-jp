---
description: SQLSetDriverConnectInfo 関数
title: SQLSetDriverConnectInfo 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDriverConnectInfo function [ODBC]
ms.assetid: bfd4dfc2-fbca-4ef3-81e5-2706f2389256
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21538fa93328790ad8173e5193ba377b0744d964
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461254"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 関数
**互換性**  
 導入されたバージョン: ODBC 3.81 標準準拠: ODBC  
  
 **まとめ**  
 **SQLSetDriverConnectInfo** は、アプリケーションの **SQLDriverConnect** 呼び出しの接続情報トークンに接続文字列を設定するために使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>引数  
 *TokenHandle*  
 代入トークンハンドル。  
  
 *InConnectionString*  
 代入完全な接続文字列 ( [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)の "Comments" の構文、部分的な接続文字列、または空の文字列)。  
  
 *StringLength1*  
 代入長さ **Inconnectionstring*(文字列が Unicode の場合)、または文字列が ANSI または DBCS の場合はバイト。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 入力検証エラーに関連する[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)と同じです。ただし、ドライバーマネージャーは、SQL_HANDLE_DBC_INFO_TOKEN の**Handletype**と*Hdbcinfotoken*の**ハンドル**を使用します。  
  
## <a name="remarks"></a>解説  
 ドライバーが SQL_ERROR または SQL_INVALID_HANDLE を返すたびに、ドライバーマネージャーはそのエラーをアプリケーションに返します ( [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) または [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 ドライバーが SQL_SUCCESS_WITH_INFO を返すたびに、ドライバーマネージャーは *Hdbcinfotoken*から診断情報を取得し、SQL_SUCCESS_WITH_INFO を [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) および [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)のアプリケーションに返します。  
  
 アプリケーションでは、この関数を直接呼び出すことはできません。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ODBC ドライバーの開発には sqlspi. h を含めます。  
  
## <a name="see-also"></a>関連項目  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
