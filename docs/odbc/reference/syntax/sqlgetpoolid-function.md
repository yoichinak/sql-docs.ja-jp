---
description: SQLGetPoolID 関数
title: SQLGetPoolID 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2cd38008b90a1299bdd78c4a56d7394f85876ab0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421256"
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID 関数
**互換性**  
 導入されたバージョン: ODBC 3.81 標準準拠: ODBC  
  
 **まとめ**  
 **SQLGetPoolID** はプール ID を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>引数  
 *hDbcInfoToken*  
 代入すべての接続情報を含むトークンハンドル。  
  
 *pPoolID*  
 Outputプール ID。これは、相互に使用できる一連の接続を識別するために使用されます (追加のリセットが必要になる場合があります)。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **SQLGetPoolID**が SQL_ERROR または SQL_SUCCESS_WITH_INFO を返すと、ドライバーマネージャーは SQL_HANDLE_DBC_INFO_TOKEN の**Handletype**および*Hdbcinfotoken*の**ハンドル**を使用します。  
  
## <a name="remarks"></a>解説  
 **SQLGetPoolID** は、接続情報のセット ( **SQLSetConnectAttrForDbcInfo**、 **SQLSetDriverConnectInfo**、および **SQLSETCONNECTINFO**) を指定してプール ID を取得するために使用されます。 このプール ID は、相互に使用できる接続のセットを識別するために使用されます (追加のリセットが必要になる場合があります)。 プール ID は、その接続グループの接続プールを識別するために使用されます。  
  
 ドライバーが SQL_ERROR または SQL_INVALID_HANDLE を返すたびに、ドライバーマネージャーはそのエラーをアプリケーションに返します ( [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) または [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 ドライバーが SQL_SUCCESS_WITH_INFO を返すたびに、ドライバーマネージャーは *Hdbcinfotoken*から診断情報を取得し、SQL_SUCCESS_WITH_INFO を [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) および [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)のアプリケーションに返します。  
  
 アプリケーションでは、この関数を直接呼び出すことはできません。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ODBC ドライバーの開発には sqlspi. h を含めます。  
  
## <a name="see-also"></a>関連項目  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
