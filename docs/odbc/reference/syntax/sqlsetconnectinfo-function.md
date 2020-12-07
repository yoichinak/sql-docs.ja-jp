---
description: SQLSetConnectInfo 関数
title: SQLSetConnectInfo 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ee3480678d228e26b16cc99e7df8955d45ade9e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499547"
---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 関数
**互換性**  
 導入されたバージョン: ODBC 3.81 標準準拠: ODBC  
  
 **まとめ**  
 **SQLSetConnectInfo** は、データソース、ユーザー ID、およびパスワードを、アプリケーションの [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) 呼び出しの接続情報トークンに設定するために使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN  SQLSetConnectInfo(  
                SQLHDBC_INFO_TOKEN   TokenHandle,  
                WCHAR *              ServerName,  
                SQLSMALLINT          NameLength1,  
                WCHAR *              UserName,  
                SQLSMALLINT          NameLength2,  
                WCHAR *              Authentication,  
                SQLSMALLINT          NameLength3 );  
```  
  
## <a name="arguments"></a>引数  
 *TokenHandle*  
 代入トークンハンドル。  
  
 *ServerName*  
 代入データソース名。 データが、プログラムと同じコンピューター、またはネットワーク上の別のコンピューターに配置されている可能性があります。 アプリケーションでデータソースを選択する方法の詳細については、「 [データソースまたはドライバーの選択](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)」を参照してください。  
  
 *NameLength1*  
 代入**ServerName* の長さ (文字数)。  
  
 *UserName*  
 代入ユーザー識別子。  
  
 *NameLength2*  
 代入**ユーザー名* の長さ (文字数)。  
  
 *認証*  
 代入認証文字列 (通常はパスワード)。  
  
 *NameLength3*  
 代入文字での **認証* の長さ。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 入力検証エラーの[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)と同じですが、Driver Manager では SQL_HANDLE_DBC_INFO_TOKEN の**Handletype**と*Hdbcinfotoken*の**ハンドル**が使用される点が異なります。  
  
## <a name="remarks"></a>解説  
 ドライバーが SQL_ERROR または SQL_INVALID_HANDLE を返すたびに、ドライバーマネージャーはそのエラーをアプリケーションに返します ( [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) または [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 ドライバーが SQL_SUCCESS_WITH_INFO を返すたびに、ドライバーマネージャーは *Hdbcinfotoken*から診断情報を取得し、SQL_SUCCESS_WITH_INFO を [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) および [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)のアプリケーションに返します。  
  
 アプリケーションでは、この関数を直接呼び出すことはできません。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ODBC ドライバーの開発には sqlspi. h を含めます。  
  
## <a name="see-also"></a>関連項目  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
