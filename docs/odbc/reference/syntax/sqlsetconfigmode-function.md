---
description: SQLSetConfigMode 関数
title: SQLSetConfigMode 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConfigMode
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConfigMode
helpviewer_keywords:
- SQLSetConfigMode function [ODBC]
ms.assetid: 09eb88ea-b6f6-4eca-b19d-0951cebc6c0a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5aab5274403a654362c5732d8ec3f6eccae3be96
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499585"
---
# <a name="sqlsetconfigmode-function"></a>SQLSetConfigMode 関数
**互換性**  
 導入されたバージョン: ODBC 3.0  
  
 **まとめ**  
 **SQLSetConfigMode** は、DSN 値を一覧表示する Odbc.ini エントリのシステム情報の場所を示す構成モードを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLSetConfigMode(  
     UWORD     wConfigMode);  
```  
  
## <a name="arguments"></a>引数  
 *wConfigMode*  
 代入インストーラー構成モード (「コメント」を参照してください)。 *Wconfigmode*の値は次のようになります。  
  
 ODBC_USER_DSN  
  
 ODBC_SYSTEM_DSN  
  
 ODBC_BOTH_DSN  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **SQLSetConfigMode**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|無効なパラメーターシーケンス|*Wconfigmode*引数に ODBC_USER_DSN、ODBC_SYSTEM_DSN、または ODBC_BOTH_DSN が含まれていませんでした。|  
  
## <a name="comments"></a>コメント  
 この関数は、DSN 値を一覧表示する Odbc.ini エントリのシステム情報の場所を設定するために使用されます。 *Wconfigmode*が ODBC_USER_DSN の場合、Dsn はユーザー dsn で、関数は HKEY_CURRENT_USER の Odbc.ini エントリから読み取ります。 ODBC_SYSTEM_DSN の場合、DSN はシステム DSN であり、関数は HKEY_LOCAL_MACHINE の Odbc.ini エントリから読み取ります。 ODBC_BOTH_DSN されている場合は HKEY_CURRENT_USER が試行され、失敗した場合は HKEY_LOCAL_MACHINE が使用されます。  
  
 この関数は、 **Sqlcreatedatasource** および **SQLDriverConnect**には影響しません。 構成モードは、ドライバーが **Sqlgetprivateprofilestring** を呼び出してレジストリから読み取るとき、または **sqlgetprivateprofilestring**を呼び出してレジストリに書き込むときに設定する必要があります。 **Sqlgetprivateprofilestring**および**sqlgetprivateprofilestring**への呼び出しでは、構成モードを使用して、操作するレジストリの部分を認識します。  
  
> [!CAUTION]  
>  **SQLSetConfigMode** は、必要な場合にのみ呼び出す必要があります。モードが不適切に設定されていると、ODBC インストーラーが正常に機能しなくなる可能性があります。  
  
 **SQLSetConfigMode** は、構成モードの直接レジストリ変更を行います。 これは、 **Sqlconfigdatasource**への呼び出しによって構成モードを変更するプロセスとは異なります。 **Sqlconfigdatasource**を呼び出すと、dsn を変更するときにユーザーとシステムの dsn を区別するように構成モードが設定されます。 返される前に、 **Sqlconfigdatasource** によって構成モードが DSN の両方にリセットされます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|データソースの作成|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|  
|接続文字列またはダイアログボックスを使用したデータソースへの接続|[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|構成モードを取得しています|[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|
