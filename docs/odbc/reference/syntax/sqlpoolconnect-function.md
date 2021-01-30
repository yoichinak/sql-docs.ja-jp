---
description: SQLPoolConnect 関数
title: SQLPoolConnect 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8317e159a5a438bb22e8077f3a6635a79f9baefd
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99204559"
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect 関数
**互換性**  
 導入されたバージョン: ODBC 3.8 標準準拠: ODBC  
  
 **要約**  
 プール内の接続を再利用できない場合は、 **Sqlpoolconnect** を使用して新しい接続を作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>引数  
 *hDbc*  
 代入接続ハンドル。  
  
 *hDbcInfoToken*  
 代入新しいアプリケーション接続要求のトークンハンドル。  
  
 *wszOutConnectString*  
 Output完了した接続文字列のバッファーへのポインター。 ターゲットデータソースへの接続に成功すると、このバッファーには完了した接続文字列が含まれます。 アプリケーションでは、このバッファーに対して少なくとも1024文字を割り当てる必要があります。  
  
 *WszOutConnectString* が NULL の場合でも、 *Cchconnectstringlen* は *wszOutConnectString* が指すバッファー内で返すことができる文字の合計数 (文字データの null 終端文字を除く) を返します。  
  
 *cchConnectStringBuffer*  
 代入**WszOutConnectString* バッファーの長さ (文字数)。  
  
 *cchConnectStringLen*  
 OutputWszOutConnectString で返すことができる文字の合計数 (null 終了文字を除く) を返すバッファーへのポインター \* 。 返すことのできる文字数が *Cchconnectstringbuffer* 以上の場合、wszOutConnectString 内の完了した接続文字列 \* は *cchconnectstringbuffer* から null 終端文字の長さを差し引いた値に切り捨てられます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)に似ていますが、ドライバーマネージャーでは SQL_HANDLE_DBC_INFO_TOKEN の **Handletype** と *Hdbcinfotoken* の **ハンドル** が使用される点が異なります。  
  
## <a name="remarks"></a>コメント  
 ドライバーマネージャーは、 *hDbc* と *Hdbcinfotoken* の親の henv ハンドルが同じであることを保証します。  
  
 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)とは異なり、接続情報の入力をユーザーに求める *drivercompletion* 引数はありません。 プールのシナリオでは、プロンプトダイアログは許可されません。  
  
 アプリケーションでは、この関数を直接呼び出すことはできません。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ドライバーが SQL_ERROR または SQL_INVALID_HANDLE を返すたびに、ドライバーマネージャーはそのエラーをアプリケーションに返します ( [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) または [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 ドライバーが SQL_SUCCESS_WITH_INFO を返すたびに、ドライバーマネージャーは *Hdbcinfotoken* から診断情報を取得し、SQL_SUCCESS_WITH_INFO を [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) および [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)のアプリケーションに返します。  
  
 アプリケーションで [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)を使用する場合、 *wszOutConnectString* は null バッファーになります (最後の3つのパラメーターはすべて NULL、0、null に設定されます)。 それ以外の場合、ドライバーは出力接続文字列を返す必要があります。出力接続文字列は、アプリケーションの [SQLDriverConnect 関数](../../../odbc/reference/syntax/sqldriverconnect-function.md) 呼び出しに返されます。  
  
 ODBC ドライバーの開発には sqlspi. h を含めます。  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
