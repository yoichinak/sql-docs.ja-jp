---
description: SQLConfigDriver 関数
title: SQLConfigDriver 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDriver
helpviewer_keywords:
- SQLConfigDriver function [ODBC]
ms.assetid: 4f681961-ac9f-4d88-b065-5258ba112642
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 04ee54bba13730504ed08cfc1307858edea56282
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476158"
---
# <a name="sqlconfigdriver-function"></a>SQLConfigDriver 関数
**互換性**  
 導入されたバージョン: ODBC 2.5  
  
 **まとめ**  
 **Sqlconfigdriver** は適切なドライバーセットアップ DLL を読み込み、 **configdriver** 関数を呼び出します。  
  
 **Sqlconfigdriver**の機能には、 [ODBCCONF.EXE](../../../odbc/odbcconf-exe.md)でアクセスすることもできます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLConfigDriver(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszArgs,  
     LPSTR    lpszMsg,  
     WORD     cbMsgMax,  
     WORD *   pcbMsgOut);  
```  
  
## <a name="arguments"></a>引数  
 *hwndParent*  
 代入親ウィンドウハンドル。 ハンドルが null の場合、この関数はダイアログボックスを表示しません。  
  
 *fRequest*  
 代入要求の種類。 *Frequest* には、次のいずれかの値が含まれている必要があります。  
  
 ODBC_CONFIG_DRIVER: ドライバーによって使用される接続プーリングのタイムアウトを変更します。  
  
 ODBC_INSTALL_DRIVER: 新しいドライバーをインストールします。  
  
 ODBC_REMOVE_DRIVER: 既存のドライバーを削除します。  
  
 このオプションは、ドライバー固有のものにすることもできます。この場合、最初のオプションの *Frequest* は ODBC_CONFIG_DRIVER_MAX + 1 から始める必要があります。 また、任意の追加オプションの *Frequest* は、ODBC_CONFIG_DRIVER_MAX + 1 よりも大きい値から始める必要があります。  
  
 *lpszDriver*  
 代入システム情報に登録されているドライバーの名前。  
  
 *lpszArgs*  
 代入ドライバー固有の *Frequest*の引数を格納している null で終わる文字列。  
  
 *lpszMsg*  
 Outputドライバーセットアップからの出力メッセージを含む null で終わる文字列。  
  
 *cbMsgMax*  
 代入*Lpszmsg*の長さ。  
  
 *pcbMsgOut*  
 Output *Lpszmsg*で返される、使用可能な合計バイト数。 返すことのできるバイト数が *Cbmsgmax*以上の場合、 *lpszmsg* の出力メッセージは、 *cbmsgmax* から null 終了文字を引いた値に切り捨てられます。 *Pcbmsgout*引数には null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlconfigdriver**が FALSE を返す場合は、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_INVALID_BUFF_LEN|バッファーの長さが無効です|*Lpszmsg*引数が無効でした。|  
|ODBC_ERROR_INVALID_HWND|ウィンドウハンドルが無効です|*HwndParent*引数が無効でした。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の種類が無効です|*Frequest*引数は、次のいずれかではありませんでした:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> *Frequest*引数は、ODBC_CONFIG_DRIVER_MAX 以下のドライバー固有のオプションでした。|  
|ODBC_ERROR_INVALID_NAME|ドライバーまたは翻訳者名が無効です|*Lpszdriver*引数が無効でした。 レジストリに見つかりませんでした。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無効なキーワードと値のペア|*Lpszargs*引数に構文エラーが含まれていました。|  
|ODBC_ERROR_REQUEST_FAILED|失敗した*要求*|インストーラーは、 *Frequest* 引数によって要求された操作を実行できませんでした。 **Configdriver**を呼び出すことができませんでした。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|ドライバーまたはトランスレーターセットアップライブラリを読み込めませんでした|ドライバーセットアップライブラリを読み込めませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **Sqlconfigdriver** を使用すると、アプリケーションはドライバーの **configdriver** ルーチンを呼び出すことができます。その際、名前を知り、ドライバー固有のセットアップ DLL を読み込む必要はありません。 セットアッププログラムは、ドライバーのセットアップ DLL がインストールされた後に、この関数を呼び出します。 呼び出し元プログラムでは、この関数がすべてのドライバーで使用できるとは限りません。 このような場合、呼び出し元のプログラムはエラーなしで続行されます。  
  
## <a name="driver-specific-options"></a>ドライバー固有のオプション  
 アプリケーションは、 *Frequest* 引数を使用して、ドライバーによって公開されているドライバー固有の機能を要求できます。 最初のオプションの *Frequest* は ODBC_CONFIG_DRIVER_MAX + 1 になり、追加のオプションはその値から1ずつ増加します。 その関数のドライバーに必要な引数は、 *Lpszargs* 引数で渡される null で終わる文字列で指定する必要があります。 このような機能を提供するドライバーでは、ドライバー固有のオプションの表を保持する必要があります。 これらのオプションは、ドライバーのドキュメントに記載されています。 ドライバー固有のオプションを使用するアプリケーションライターでは、この使用によってアプリケーションの相互運用性が低下することに注意してください。  
  
## <a name="setting-connection-pooling-timeout"></a>接続プールのタイムアウトを設定しています  
 接続プールのタイムアウトプロパティは、ドライバーの構成を設定するときに設定できます。 **Sqlconfigdriver**は、ODBC_CONFIG_DRIVER の*Frequest*と、 **cptimeout**に設定された*lpszargs*を使用して呼び出されます。 **Cptimeout** は、接続が使用されないまま接続プールに保持できる期間を決定します。 タイムアウトが経過すると、接続が閉じられ、プールから削除されます。 既定のタイムアウトは60秒です。  
  
 *Frequest*が ODBC_INSTALL_DRIVER または ODBC_REMOVE_DRIVER に設定された状態で**sqlconfigdriver**が呼び出されると、ドライバーマネージャーは適切なドライバーセットアップ DLL を読み込み、 **configdriver**関数を呼び出します。 ODBC_CONFIG_DRIVER の*Frequest*を使用して**sqlconfigdriver**が呼び出されると、すべての処理が ODBC インストーラーで実行されるため、ドライバーのセットアップ DLL を読み込む必要がなくなります。  
  
## <a name="messages"></a>メッセージ  
 ドライバーのセットアップルーチンは、テキストメッセージを *Lpszmsg* バッファー内の null で終わる文字列としてアプリケーションに送信できます。 このメッセージは、cbmsgmax*文字以上*の場合、 **configdriver**関数によって*cbmsgmax*から null 終了文字を引いた値に切り捨てられます。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ドライバーの追加、変更、または削除|[Configdriver](../../../odbc/reference/syntax/configdriver-function.md)(セットアップ DLL 内)|  
|既定のデータソースの削除|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|
