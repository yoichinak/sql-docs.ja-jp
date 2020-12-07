---
description: SQLWritePrivateProfileString 関数
title: SQLWritePrivateProfileString 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWritePrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWritePrivateProfileString
helpviewer_keywords:
- SQLWritePrivateProfileString [ODBC]
ms.assetid: 526f36a4-92ed-4874-9725-82d27c0b86f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1110b60d6dc0ba079804ba8a9f21c06f0c1f78d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420956"
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString 関数
**互換性**  
 導入されたバージョン: ODBC 2.0  
  
 **まとめ**  
 **Sqlwriteprivateprofilestring** は、値の名前とデータをシステム情報の Odbc.ini サブキーに書き込みます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>引数  
 *lpszSection*  
 代入文字列がコピーされるセクションの名前を格納している、null で終わる文字列を指します。 セクションが存在しない場合は、作成されます。 セクションの名前は大文字と小文字が区別されません。文字列には、大文字と小文字の任意の組み合わせを使用できます。  
  
 *lpszEntry*  
 代入文字列に関連付けられるキーの名前を格納している null で終わる文字列を指します。 指定されたセクションにキーが存在しない場合は、作成されます。 この引数が NULL の場合、セクション内のすべてのエントリを含むセクション全体が削除されます。  
  
 *lpszString*  
 代入ファイルに書き込まれる null で終わる文字列を指します。 この引数が NULL の場合、 *lpszEntry* 引数が指すキーが削除されます。  
  
 *lpszFilename*  
 Outputは、初期化ファイルに名前を指定する null で終わる文字列を指します。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlwriteprivateprofilestring**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_REQUEST_FAILED|要求が失敗しました|要求されたシステム情報を書き込めませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **Sqlwriteprivateprofilestring** は、Microsoft® windows®から MICROSOFT windows NT®/windows 2000 にドライバーおよびドライバーのセットアップ dll を移植する簡単な方法として提供されています。 Odbc.ini ファイルにプロファイル文字列を書き込む **Writeprivateprofilestring** への呼び出しは、 **Sqlwriteprivateprofilestring**への呼び出しで置き換える必要があります。 **Sqlwriteprivateprofilestring** は、WIN32® API の関数を呼び出して、指定された値の名前とデータをシステム情報の Odbc.ini サブキーに追加します。  
  
 構成モードは、DSN 値を一覧表示する Odbc.ini エントリがシステム情報に含まれる場所を示します。 DSN がユーザー DSN (状態変数が USERDSN_ONLY) の場合、関数は HKEY_CURRENT_USER の Odbc.ini エントリに書き込みます。 DSN がシステム DSN (SYSTEMDSN_ONLY) の場合、関数は HKEY_LOCAL_MACHINE の Odbc.ini エントリに書き込みます。 状態変数が両方とも DSN の場合、HKEY_CURRENT_USER が試行され、失敗した場合は HKEY_LOCAL_MACHINE が使用されます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|システム情報から値を取得する|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
