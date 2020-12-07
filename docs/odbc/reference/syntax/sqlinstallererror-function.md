---
description: SQLInstallerError 関数
title: Sqlインストーラエラー関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallerError
helpviewer_keywords:
- SQLInstallerError [ODBC]
ms.assetid: e6474b79-4d55-458f-81ce-abfafe357f83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcc5f89a40802e6efa405771474cda3e86f4519c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421166"
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError 関数
**互換性**  
 導入されたバージョン: ODBC 3.0  
  
 **まとめ**  
 **Sqlインストーラエラー** ODBC インストーラー関数のエラーまたは状態の情報を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>引数  
 *iError*  
 代入エラーレコード番号。 有効な値は 1 ~ 8 です。  
  
 *pfErrorCode*  
 Outputインストーラーのエラーコードです。 (詳細については、「コメント」を参照してください)。  
  
 *lpszErrorMsg*  
 Outputエラーメッセージテキストのストレージへのポインター。  
  
 *cbErrorMsgMax*  
 代入 *Szerrormsg* バッファーの最大長。 この値は、null 終了文字を引いた SQL_MAX_MESSAGE_LENGTH 以下である必要があります。  
  
 *cbErrorMsgMax*  
 代入 *Szerrormsg* バッファーの最大長。 この値は、null 終了文字を引いた SQL_MAX_MESSAGE_LENGTH 以下である必要があります。  
  
 *pcbErrorMsg*  
 Output *Lpszerrormsg*で返すことができる合計バイト数 (null 終端文字を除く) へのポインター。 返されるバイト数が *Cberrormsgmax*以上の場合、 *lpszerrormsg* のエラーメッセージテキストは *cberrormsgmax* から null 終端文字のバイトを引いた値に切り捨てられます。 *Pcberrormsg*引数には null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、または SQL_ERROR。  
  
## <a name="diagnostics"></a>診断  
 **Sqlインストーラエラー** は、それ自体のエラー値を通知しません。 **Sqlインストーラエラー** は、エラー情報を取得できない場合に SQL_NO_DATA を返します (この場合、 *pferrorcode* は定義されていません)。 通常 SQL_ERROR を返す何らかの理由で **Sqlインストーラエラー** がエラー値にアクセスできない場合、 **sqlインストーラエラー** は SQL_ERROR を返しますが、エラー値は通知されません。 警告文字列 (*lpszerrormsg*) の長さがわからない場合は、 *LPSZERRORMSG* を NULL に設定し、 **sqlインストーラエラー**を呼び出すことができます。 **Sqlインストーラエラー** は、 *Cberrormsgmax*の警告文字列の長さを返します。 エラーメッセージのバッファーが短すぎる場合、 **Sqlインストーラエラー**は SQL_SUCCESS_WITH_INFO を返し、 **sqlインストーラエラー**の正しい*pferrorcode*値を返します。  
  
 エラーメッセージで切り捨てが発生したかどうかを判断するために、アプリケーションでは、 *Cberrormsgmax* 引数の値と *Pcberrormsg* 引数に書き込まれたメッセージテキストの実際の長さを比較できます。 切り捨てが発生した場合は、 *Lpszerrormsg*に正しいバッファー長を割り当てる必要があります。また、対応する*iError*レコードを使用して**sqlインストーラエラー**を再度呼び出す必要があります。  
  
## <a name="comments"></a>コメント  
 ODBC インストーラー関数の前回の呼び出しで FALSE が返された場合、アプリケーションは **Sqlインストーラエラー** を呼び出します。 ODBC インストーラーとドライバーまたはトランスレーターセットアップ関数は、関数が失敗した場合にのみ0個以上のエラーを通知します (FALSE を返します)。そのため、アプリケーションは ODBC インストーラー関数が失敗した後にのみ **Sqlinstaller エラー** を呼び出します。  
  
 ODBC インストーラーのエラーキューは、新しいインストーラー関数が呼び出されるたびにフラッシュされます。 そのため、アプリケーションは、最後のインストーラー関数呼び出し以外の関数のエラーを取得することを想定できません。  
  
 関数呼び出しの複数のエラーを取得するために、アプリケーションは **Sqlインストーラエラー** を複数回呼び出します。  
  
 追加情報がない場合、 **Sqlインストーラエラー** は SQL_NO_DATA を返し、 *pferrorcode* 引数は定義されていません。 *pcberrormsg* 引数は0になり、 *lpszerrormsg* 引数には1つの Null 終了文字が含まれます ( *cberrormsgmax* 引数が0の場合を除く)。
