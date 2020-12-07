---
description: SQLGetPrivateProfileString 関数
title: SQLGetPrivateProfileString 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetPrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetPrivateProfileString
helpviewer_keywords:
- SQLGetPrivateProfileString function [ODBC]
ms.assetid: b72ca065-4d67-48df-baac-e18379a8320a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2223d46d507df2a9cf82e7feb800caf5b8f82cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421236"
---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString 関数
**互換性**  
 導入されたバージョン: ODBC 2.0  
  
 **まとめ**  
 **Sqlgetprivateprofilestring** システム情報の値に対応する値またはデータの名前の一覧を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
int SQLGetPrivateProfileString(  
     LPCSTR   lpszSection,  
     LPCSTR   lpszEntry,  
     LPCSTR   lpszDefault,  
     LPCSTR   RetBuffer,  
     INT      cbRetBuffer,  
     LPCSTR   lpszFilename);  
```  
  
## <a name="arguments"></a>引数  
 *lpszSection*  
 代入キー名を含むセクションを指定する null で終わる文字列を指します。 この引数が NULL の場合、関数は、指定されたバッファーにファイル内のすべてのセクション名をコピーします。  
  
 *lpszEntry*  
 代入関連付けられた文字列を取得するキー名を格納している null で終わる文字列を指します。 この引数が NULL の場合、 *Lpszsection* 引数で指定されたセクション内のすべてのキー名が、 *retbuffer* 引数で指定されたバッファーにコピーされます。  
  
 *lpszDefault*  
 代入キーが初期化ファイルに見つからない場合は、指定されたキーの既定値を指定する null で終わる文字列を指します。 この引数を NULL にすることはできません。  
  
 *RetBuffer*  
 Output取得した文字列を受け取るバッファーを指します。  
  
 *cbRetBuffer*  
 代入 *Retbuffer* 引数が指すバッファーのサイズを文字数で指定します。  
  
 *lpszFilename*  
 代入は、初期化ファイルに名前を指定する null で終わる文字列を指します。 この引数にファイルへの完全パスが含まれていない場合は、既定のディレクトリが検索されます。  
  
## <a name="returns"></a>戻り値  
 **Sqlgetprivateprofilestring** は、読み取られた文字数を示す整数値を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlgetprivateprofilestring**の呼び出しが失敗した場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **Sqlgetprivateprofilestring** は、Microsoft® windows®から MICROSOFT windows NT®/windows 2000 にドライバーおよびドライバーのセットアップ dll を移植する簡単な方法として提供されています。 Odbc.ini ファイルからプロファイル文字列を取得する **Getprivateprofilestring** への呼び出しは、 **Sqlgetprivateprofilestring**への呼び出しで置き換える必要があります。 **Sqlgetprivateprofilestring** は、WIN32® API の関数を呼び出して、システム情報の Odbc.ini サブキーの値に対応する、要求された値またはデータの名前を取得します。  
  
 ( **SQLSetConfigMode**によって設定された) 構成モードは、DSN 値を一覧表示する Odbc.ini エントリのシステム情報の場所を示します。 DSN がユーザー DSN (構成モードが USERDSN_ONLY) の場合、関数は HKEY_CURRENT_USER の Odbc.ini エントリから読み取ります。 DSN がシステム DSN (SYSTEMDSN_ONLY) の場合、関数は HKEY_LOCAL_MACHINE の Odbc.ini エントリから読み取ります。 構成モードが両方とも DSN の場合、HKEY_CURRENT_USER が試行され、失敗した場合は HKEY_LOCAL_MACHINE が使用されます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|システム情報への値の書き込み|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
