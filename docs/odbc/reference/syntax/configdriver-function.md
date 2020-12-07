---
description: ConfigDriver 関数
title: ConfigDriver 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- ConfigDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- ConfigDriver
helpviewer_keywords:
- ConfigDriver [ODBC]
ms.assetid: 9473f48f-bcae-4784-89c1-7839bad4ed13
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d59765d1b6a6a662c02b459e07bac10895838a2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428954"
---
# <a name="configdriver-function"></a>ConfigDriver 関数
**互換性**  
 導入されたバージョン: ODBC 2.5  
  
 **まとめ**  
 **Configdriver** を使用すると、プログラムが **configdriver**を呼び出さなくても、インストールおよびアンインストール機能を実行できます。 この関数では、ドライバー固有のシステム情報の作成やインストール時の DSN 変換の実行、アンインストール中のシステム情報のクリーンアップなど、ドライバー固有の機能が実行されます。 この関数は、ドライバーのセットアップ DLL または別のセットアップ DLL によって公開されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL ConfigDriver(  
      HWND    hwndParent,  
      WORD    fRequest,  
      LPCSTR  lpszDriver,  
      LPCSTR  lpszArgs,  
      LPSTR   lpszMsg,  
      WORD    cbMsgMax,  
      WORD *  pcbMsgOut);  
```  
  
## <a name="arguments"></a>引数  
 *hwndParent*  
 代入親ウィンドウハンドル。 ハンドルが null の場合、この関数はダイアログボックスを表示しません。  
  
 *fRequest*  
 代入要求の種類。 *Frequest*引数には、次のいずれかの値が含まれている必要があります。  
  
 ODBC_INSTALL_DRIVER: 新しいドライバーをインストールします。  
  
 ODBC_REMOVE_DRIVER: ドライバーを削除します。  
  
 このオプションは、ドライバー固有のものにすることもできます。この場合、最初のオプションの *Frequest* 引数は ODBC_CONFIG_DRIVER_MAX + 1 から始める必要があります。 任意の追加オプションの *Frequest* 引数も ODBC_CONFIG_DRIVER_MAX + 1 よりも大きい値から開始する必要があります。  
  
 *lpszDriver*  
 代入システム情報の Odbcinst.ini キーに登録されているドライバーの名前。  
  
 *lpszArgs*  
 代入ドライバー固有の *Frequest*の引数を格納している null で終わる文字列。  
  
 *lpszMsg*  
 Outputドライバーセットアップからの出力メッセージを格納している null で終わる文字列。  
  
 *cbMsgMax*  
 代入 *Lpszmsg*の長さ。  
  
 *pcbMsgOut*  
 Output *Lpszmsg*で返される、使用可能な合計バイト数。  
  
 返すことのできるバイト数が *Cbmsgmax*以上の場合、 *lpszmsg* の出力メッセージは、 *cbmsgmax* から null 終了文字を引いた値に切り捨てられます。 *Pcbmsgout*引数には null ポインターを指定できます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Configdriver**が FALSE を返す場合、関連する* \* Pferrorcode*値は、 **sqlpostインストーラエラー**の呼び出しによってインストーラーエラーバッファーにポストされ、 **sqlインストーラエラー**を呼び出すことによって取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|ウィンドウハンドルが無効です|*HwndParent*引数が無効でした。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の種類が無効です|*Frequest*引数は、次のいずれかではありませんでした:<br /><br /> ODBC_INSTALL_DRIVER ODBC_REMOVE_DRIVER<br /><br /> ドライバー固有のオプションは ODBC_CONFIG_DRIVER_MAX 以下です。|  
|ODBC_ERROR_INVALID_NAME|ドライバーまたは翻訳者名が無効です|*Lpszdriver*引数が無効でした。 レジストリに見つかりませんでした。|  
|ODBC_ERROR_REQUEST_FAILED|失敗した*要求*|*Frequest*引数によって要求された操作を実行できませんでした。|  
|ODBC_ERROR_DRIVER_SPECIFIC|ドライバーまたはトランスレーター固有のエラー|ODBC インストーラーエラーが定義されていないドライバー固有のエラー。 **Sqlpostインストーラ error**関数の呼び出しの*szerror*引数には、ドライバー固有のエラーメッセージが含まれている必要があります。|  
  
## <a name="comments"></a>コメント  
  
### <a name="driver-specific-options"></a>ドライバー固有のオプション  
 アプリケーションは、 *Frequest* 引数を使用して、ドライバーによって公開されているドライバー固有の機能を要求できます。 最初のオプションの *Frequest* は 1 ODBC_CONFIG_DRIVER_MAX 加算され、追加のオプションはその値から1ずつ増加します。 その関数のドライバーに必要な引数は、 *Lpszargs* 引数で渡される null で終わる文字列で指定する必要があります。 このような機能を提供するドライバーでは、ドライバー固有のオプションの表を保持する必要があります。 これらのオプションは、ドライバーのドキュメントに記載されています。 ドライバー固有のオプションを使用するアプリケーションライターでは、アプリケーションの相互運用性が低下することに注意してください。  
  
### <a name="messages"></a>メッセージ  
 ドライバーのセットアップルーチンは、テキストメッセージを *Lpszmsg* バッファー内の null で終わる文字列としてアプリケーションに送信できます。 このメッセージは、cbmsgmax*文字以上*の場合、 **configdriver**関数によって*cbmsgmax*から null 終了文字を引いた値に切り捨てられます。
