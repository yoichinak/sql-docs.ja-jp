---
description: SQLInstallTranslatorEx 関数
title: SQLInstallTranslatorEx 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslatorEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslatorEx
helpviewer_keywords:
- SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7957a04e0dafaeb2177401f775c5cdbb75135569
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421146"
---
# <a name="sqlinstalltranslatorex-function"></a>SQLInstallTranslatorEx 関数
**互換性**  
 導入されたバージョン: ODBC 3.0  
  
 **まとめ**  
 **SQLInstallTranslatorEx** は、翻訳者に関する情報をシステム情報 (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INI \ ODBC translator レジストリキー) の Odbcinst.ini セクションに追加します。  
  
 **SQLInstallTranslatorEx**の機能には、 [ODBCCONF.EXE](../../../odbc/odbcconf-exe.md)でもアクセスできます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLInstallTranslatorEx(  
     LPCSTR    lpszTranslator,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引数  
 *lpszTranslator*  
 代入これには、トランスレーターを記述する、二重の null で終わるキーワードと値のペアの一覧が含まれている必要があります。 キーワードと値のペアの構文の詳細については、「 [トランスレーター指定サブキー](../../../odbc/reference/install/translator-specification-subkeys.md)」を参照してください。  
  
 **トランスレーター**と**セットアップ**のキーワードは、 *lpsztranslator*文字列に含まれている必要があります。 Translation DLL が **translator** キーワードと共に一覧表示され、TRANSLATOR セットアップ Dll が **setup** キーワードと共に一覧表示されます。 各ペアは NULL バイトで終了し、リスト全体は NULL バイトで終了します。 (つまり、2つの NULL バイトはリストの末尾をマークします)。 *Lpsztranslator* の形式は次のとおりです。  
  
 \0Translator =*translator-filename*\ 0 [setup =*setup-dll-filename*\ 0] \ 0  
  
 *lpszPathIn*  
 代入トランスレーターがインストールされる場所の完全パスまたは null ポインター。 *Lpszpath*が null ポインターの場合、翻訳者はシステムディレクトリにインストールされます。  
  
 *lpszPathOut*  
 Outputトランスレーターをインストールするターゲットディレクトリのパス。 翻訳ツールがインストールされていない場合、 *Lpszpathout* は *lpszpathout*と同じです。 トランスレーターの以前のインストールが存在する場合、 *Lpszpathout* は以前のインストールのパスです。  
  
 *cbPathOutMax*  
 代入*Lpszpathout*の長さ。  
  
 *pcbPathOut*  
 Output *Lpszpathout*で返される、使用可能な合計バイト数。 返される使用可能なバイト数が *Cbpathoutmax*以上の場合、 *lpszpathout* の出力パスは *pcbpathoutmax* から null 終端文字に切り捨てられます。 *Pcbpathout*引数は null ポインターにすることができます。  
  
 *fRequest*  
 代入要求の種類。 *Frequest* には、次のいずれかの値が含まれている必要があります。  
  
 ODBC_INSTALL_INQUIRY: トランスレーターをインストールできる場所について問い合わせます。  
  
 ODBC_INSTALL_COMPLETE: インストール要求を完了します。  
  
 *lpdwUsageCount*  
 Outputこの関数が呼び出された後のトランスレーターの使用回数。  
  
 アプリケーションで使用状況カウントを設定しないでください。 ODBC ではこのカウントが維持されます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **SQLInstallTranslatorEx**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_INVALID_BUFF_LEN|バッファーの長さが無効です|*Lpszpathout*引数は、出力パスを格納するのに十分な大きさではありませんでした。 バッファーには、切り捨てられたパスが含まれています。<br /><br /> *Cbpathoutmax*引数が0で、 *frequest*引数が ODBC_INSTALL_COMPLETE でした。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の種類が無効です|*Frequest*引数は、次のいずれかではありませんでした:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無効なキーワードと値のペア|*Lpsztranslator*引数に構文エラーが含まれていました。|  
|ODBC_ERROR_INVALID_PATH|無効なインストールパス|*Lpszpathin*引数に無効なパスが含まれています。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|無効なパラメーターシーケンス|*Lpsztranslator*引数にキーワードと値のペアのリストが含まれていませんでした。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|レジストリのコンポーネントの使用回数をインクリメントまたはデクリメントできませんでした|インストーラーで、トランスレーターの使用回数をインクリメントできませんでした。|  
  
## <a name="comments"></a>コメント  
 **SQLInstallTranslatorEx** は、翻訳ツールだけをインストールするメカニズムを提供します。 この関数は、実際にはファイルをコピーしません。 呼び出し元のプログラムは、翻訳ファイルをコピーします。  
  
 **SQLInstallTranslatorEx** は、インストールされている変換プログラムのコンポーネントの使用回数を1ずつ増やします。 翻訳者のバージョンが既に存在していても、変換プログラムのコンポーネント使用量が存在しない場合、新しいコンポーネントの使用状況のカウント値は2に設定されます。  
  
 アプリケーションセットアッププログラムは、翻訳ファイルを物理的にコピーし、ファイルの使用量を維持する役割を担います。 トランスレーターファイルが以前にインストールされていない場合は、アプリケーションセットアッププログラムによってファイルがコピーされ、ファイルまたはファイルの使用状況の数が作成されます。 ファイルが既にインストールされている場合は、セットアッププログラムによってファイルの使用量が単純にインクリメントされます。  
  
 以前のバージョンの変換プログラムがアプリケーションによって以前にインストールされていた場合は、translator コンポーネントの使用回数が有効になるように、翻訳ツールをアンインストールしてから再インストールする必要があります。 コンポーネントの使用量を減らすには、 **Sqlremovetranslator**を呼び出す必要があります。その後、 **SQLInstallTranslatorEx**を呼び出して、コンポーネントの使用量を増やします。 アプリケーションセットアッププログラムは、古いファイルを新しいファイルに置き換える必要があります。 ファイルの使用量は同じままになり、古いバージョンのファイルを使用する他のアプリケーションでは、新しいバージョンが使用されるようになります。  
  
 **SQLInstallTranslatorEx**の*lpszpathout*のパスの長さにより、2フェーズのインストールプロセスが可能になるため、アプリケーションでは、 *Frequest* for ODBC_INSTALL_INQUIRY モードで**SQLInstallTranslatorEx**を呼び出すことによって、どの*cbpathoutmax*が必要かを判断できます。 これにより、 *Pcbpathout* バッファーで使用可能な合計バイト数が返されます。 **SQLInstallTranslatorEx** は、ODBC_INSTALL_COMPLETE の *frequest* を使用して呼び出すことができます。また、 *Cbpathoutmax* 引数を *pcbpathout* バッファーの値に設定し、null 終了文字を指定して呼び出すこともできます。  
  
 **SQLInstallTranslatorEx**に2フェーズモデルを使用しない場合は、stdlib.h> で定義されているように、ターゲット _MAX_PATH ディレクトリのパスのストレージのサイズを定義する*Cbpathoutmax*を設定して、切り捨てが行われないようにする必要があります。  
  
 *Frequest*が ODBC_INSTALL_COMPLETE 場合、 **SQLInstallTranslatorEx**では、 *lpszpathout*を NULL (または*cbpathoutmax*を0にする) は許可されません。 *Frequest*が ODBC_INSTALL_COMPLETE の場合、返されるバイト数が*Cbpathoutmax*以上であるときに FALSE が返され、その結果、切り捨てが発生します。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|既定の翻訳オプションを返す|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|翻訳者の選択|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|トランスレーターの削除|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
