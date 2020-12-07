---
description: SQLWriteFileDSN 関数
title: SQLWriteFileDSN 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteFileDSN
helpviewer_keywords:
- SQLWriteFileDSN [ODBC]
ms.assetid: 9e18f56f-1061-416b-83d4-ffeec42ab5a9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4bd63c368f4055821df41faceb7b9c33cf20bde3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421006"
---
# <a name="sqlwritefiledsn-function"></a>SQLWriteFileDSN 関数
**互換性**  
 導入されたバージョン: ODBC 3.0  
  
 **まとめ**  
 **SQLWriteFileDSN** は、ファイル DSN に情報を書き込みます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLWriteFileDSN(  
     LPCSTR     lpszFileName,  
     LPCSTR     lpszAppName,  
     LPCSTR     lpszKeyName,  
     LPCSTR     lpszString);  
```  
  
## <a name="arguments"></a>引数  
 *lpszFileName*  
 代入ファイル DSN の名前へのポインター。 Dsn の拡張機能は、まだ DSN の拡張子がないすべてのファイル名に追加されます。  
  
 *lpszAppName*  
 代入アプリケーションの名前へのポインター。 ODBC セクションの場合は "ODBC" です。  
  
 *lpszKeyName*  
 代入読み取るキーの名前へのポインター。 予約済みキーワードについては、「コメント」を参照してください。  
  
 *lpszString*  
 Output書き込むキーに関連付けられている文字列を指します。 この引数が指す文字列の最大長は32767バイトです。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **SQLWriteFileDSN**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_INVALID_PATH|無効なインストールパス|*Lpszfilename*引数で指定されたファイル名のパスが無効です。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の種類が無効です|*Lpszappname*、 *lpszappname*、または*lpszappname*引数が NULL でした。|  
  
## <a name="comments"></a>コメント  
 ODBC では、接続情報を格納するセクション名 [ODBC] が予約されています。 このセクションの予約済みキーワードは、 **SQLDriverConnect**の接続文字列用に予約されているキーワードと同じです。 (詳細については、 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 関数の説明を参照してください。)  
  
 アプリケーションでは、これらの予約済みキーワードを使用して、ファイル DSN に直接情報を書き込むことができます。 アプリケーションで、ファイル DSN に関連付けられている DSN のない接続文字列を作成または変更する場合は、[ODBC] セクションの予約されている接続文字列キーワードに対して **SQLWriteFileDSN** を呼び出すことができます。  
  
 *Lpszstring*引数が null ポインターの場合、 *lpszstring*引数が指すキーワードは、dsn ファイルから削除されます。 *Lpszstring*引数と*lpszstring*引数が両方とも null ポインターの場合、 *lpszstring*引数によって示されるセクションは、dsn ファイルから削除されます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ファイル Dsn から情報を読み取っています|[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|
