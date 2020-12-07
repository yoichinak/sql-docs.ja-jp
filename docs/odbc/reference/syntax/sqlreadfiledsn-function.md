---
description: SQLReadFileDSN 関数
title: SQLReadFileDSN 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLReadFileDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLReadFileDSN
helpviewer_keywords:
- SQLReadFileDSN function [ODBC]
ms.assetid: ead464aa-cdc3-47dd-a0c0-997711205d31
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 76f6cdb3dfc423cba4eed6981ce540b5192288e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487104"
---
# <a name="sqlreadfiledsn-function"></a>SQLReadFileDSN 関数
**互換性**  
 導入されたバージョン: ODBC 3.0  
  
 **まとめ**  
 **SQLReadFileDSN** ファイル DSN から情報を読み取ります。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLReadFileDSN(  
     LPCSTR   lpszFileName,  
     LPCSTR   lpszAppName,  
     LPCSTR   lpszKeyName,  
     LPSTR    lpszString,  
     WORD     cbString,  
     WORD *   pcbString);  
```  
  
## <a name="arguments"></a>引数  
 *lpszFileName*  
 代入Dsn ファイルの名前を格納しているデータバッファーへのポインター。 . Dsn 拡張子は、まだ dsn 拡張子のないすべてのファイル名に追加されます。 * \* Lpszfilename*の値は、null で終わる文字列である必要があります。  
  
 *lpszAppName*  
 代入アプリケーションの名前を格納しているデータバッファーへのポインター。 ODBC セクションの場合は "ODBC" です。 * \* Lpszappname*の値は、null で終わる文字列である必要があります。  
  
 *lpszKeyName*  
 代入読み取るキーの名前を格納しているデータバッファーへのポインター。 予約済みキーワードについては、「コメント」を参照してください。 * \* Lpszappname*の値は、null で終わる文字列である必要があります。  
  
 *lpszString*  
 Output読み取るキーに関連付けられている文字列を格納しているデータバッファーへのポインター。  
  
 * \* Lpszfilename*が有効な dsn ファイル名ですが、 *lpszfilename*引数が Null ポインターであり、 *lpszfilename*引数が null ポインターの場合は、 * \* lpszfilename*に有効なアプリケーションの一覧が含まれています。 * \* Lpszfilename*が有効な. dsn ファイル名であり、 * \* lpszfilename*が有効なアプリケーション名であるにもかかわらず、 *lpszfilename*引数が null ポインターである場合、 * \* lpszfilename*には、dsn ファイルの該当セクションにある有効な予約済みキーワードの一覧がセミコロンで区切られて含まれています。 * \* Lpszfilename*が有効な dsn ファイル名ですが、 * \* lpszfilename*が null ポインターで、 *lpszfilename*引数が null ポインターである場合、 * \* lpszfilename*には、dsn ファイル内のセクションのリストがセミコロンで区切られて含まれています。  
  
 *cbString*  
 代入* \* Lpszstring*バッファーの長さ。  
  
 *pcbString*  
 Output* \* Lpszstring*で返される、使用可能な合計バイト数。 返すことのできるバイト数が*Cbstring*以上の場合、 * \* lpszstring*の出力文字列は*cbstring*から null 終了文字を引いた値に切り捨てられます。 *Pcbstring*引数には null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **SQLReadFileDSN**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_INVALID_BUFF_LEN|バッファーの長さが無効です|*Lpszstring*引数が NULL でした。<br /><br /> *Cbstring*引数が0以下でした。|  
|ODBC_ERROR_INVALID_PATH|無効なインストールパス|*Lpszfilename*引数で指定されたファイル名のパスが無効です。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の種類が無効です|*Lpszappname*引数が NULL でしたが、 *lpszappname*引数が有効でした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
|ODBC_ERROR_OUTPUT_STRING_TRUNCATED|出力文字列が切り捨てられました|Lpszstring の値が* \* pcbstring*の値以下で*あった*ため、 * \* lpszstring*で返された文字列が切り捨てられました。|  
|ODBC_ERROR_REQUEST_FAILED|要求が失敗しました|キーワードがファイル DSN に存在しませんでした。|  
  
## <a name="comments"></a>コメント  
 ODBC では、接続情報を格納するセクション名 [ODBC] が予約されています。 このセクションの予約済みキーワードは、 **SQLDriverConnect**の接続文字列用に予約されているキーワードと同じです。 (詳細については、 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) 関数の説明を参照してください。)  
  
 アプリケーションでは、これらの予約済みキーワードを使用して、ファイル DSN の情報を読み取ることができます。 アプリケーションで、ファイル DSN に関連付けられている DSN のない接続文字列を調べる必要がある場合、[ODBC] セクションの予約されている接続文字列キーワードに対して **SQLReadFileDSN** を呼び出すことができます。 DSN のない接続で渡される完全な接続文字列は、[ODBC] セクションのすべてのキーワード (予約およびドライバー固有) を組み合わせたものです。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ファイル DSN への情報の書き込み|[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|
