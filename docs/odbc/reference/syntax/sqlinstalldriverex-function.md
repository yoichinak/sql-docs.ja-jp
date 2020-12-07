---
description: SQLInstallDriverEx 関数
title: SQLInstallDriverEx 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverEx
helpviewer_keywords:
- SQLInstallDriverEx function [ODBC]
ms.assetid: 1dd74544-f4e9-46e1-9b5f-c11d84fdab4c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2c200615c9d3bc71ccb146d3b898517611b53eed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421186"
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx 関数
**互換性**  
 導入されたバージョン: ODBC 3.0  
  
 **まとめ**  
 **Sqlinstalldriverex** は、ドライバーに関する情報をシステム情報の Odbcinst.ini エントリに追加し、ドライバーの *usagecount* を1だけインクリメントします。 ただし、ドライバーのバージョンが既に存在していても、ドライバーの *Usagecount* の値が存在しない場合、新しい *usagecount* の値は2に設定されます。  
  
 この関数は、実際にはファイルをコピーしません。 ドライバーのファイルをターゲットディレクトリに適切にコピーするのは、呼び出し元のプログラムの役割です。  
  
 **Sqlinstalldriverex**の機能には、 [ODBCCONF.EXE](../../../odbc/odbcconf-exe.md)でもアクセスできます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLInstallDriverEx(  
     LPCSTR    lpszDriver,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引数  
 *lpszDriver*  
 代入物理ドライバー名の代わりにユーザーに提示されるドライバーの説明 (通常は、関連付けられている DBMS の名前)。 *Lpszdriver*引数には、ドライバーを記述する2つのキーワードと値のペアの二重の null で終わるリストが含まれている必要があります。 キーワードと値のペアの詳細については、「 [ドライバー仕様のサブキー](../../../odbc/reference/install/driver-specification-subkeys.md)」を参照してください。 双方向の null で終わる文字列の詳細については、「 [Configdsn 関数](../../../odbc/reference/syntax/configdsn-function.md)」を参照してください。  
  
 *lpszPathIn*  
 代入インストール先ディレクトリの完全パス、または null ポインター。 *Lpszpathin*が null ポインターの場合、ドライバーはシステムディレクトリにインストールされます。  
  
 *lpszPathOut*  
 Outputドライバーをインストールするターゲットディレクトリのパス。 ドライバーがまだインストールされていない場合、 *Lpszpathout* は *lpszpathout*と同じである必要があります。 ドライバーが既にインストールされている場合、 *Lpszpathout* は以前のインストールのパスです。  
  
 *cbPathOutMax*  
 代入 *Lpszpathout*の長さ。  
  
 *pcbPathOut*  
 Output *Lpszpathout*で返すことができる合計バイト数 (null 終端文字を除く)。 返される使用可能なバイト数が *Cbpathoutmax*以上の場合、 *lpszpathout* の出力パスは *cbpathoutmax* から null 終端文字に切り捨てられます。 *Pcbpathout*引数は null ポインターにすることができます。  
  
 *fRequest*  
 代入要求の種類。 *Frequest*引数には、次のいずれかの値が含まれている必要があります。  
  
 ODBC_INSTALL_INQUIRY: ドライバーをインストールできる場所について問い合わせます。  
  
 ODBC_INSTALL_COMPLETE: インストール要求を完了します。  
  
 *lpdwUsageCount*  
 Outputこの関数が呼び出された後のドライバーの使用カウント。  
  
 アプリケーションで使用状況カウントを設定しないでください。 ODBC ではこのカウントが維持されます。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlinstalldriverex**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_INVALID_BUFF_LEN|バッファーの長さが無効です|*Lpszpathout*引数は、出力パスを格納するのに十分な大きさではありませんでした。 バッファーには、切り捨てられたパスが含まれています。<br /><br /> *Cbpathoutmax*引数が0で、 *frequest*が ODBC_INSTALL_COMPLETE でした。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の種類が無効です|*Frequest*引数は、次のいずれかではありませんでした:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無効なキーワードと値のペア|*Lpszdriver*引数に構文エラーが含まれていました。|  
|ODBC_ERROR_INVALID_PATH|無効なインストールパス|*Lpszpathin*引数に無効なパスが含まれています。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|ドライバーまたはトランスレーターセットアップライブラリを読み込めませんでした|ドライバーセットアップライブラリを読み込めませんでした。|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|無効なパラメーターシーケンス|*Lpszdriver*引数にキーワードと値のペアのリストが含まれていませんでした。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|コンポーネントの使用状況カウントをインクリメントまたはデクリメントできませんでした|インストーラーでドライバーの使用量を増やすことができませんでした。|  
  
## <a name="comments"></a>コメント  
 *Lpszdriver*引数は、キーワードと値のペアの形式の属性の一覧です。 各ペアは null バイトで終了し、リスト全体は null バイトで終了します。 (つまり、2つの null バイトはリストの末尾をマークします)。この一覧の形式は次のとおりです。  
  
 _ドライバー-desc_ **\\**0Driver **=** _DRIVER-dll-filename_ **\\** 0 [setup **=** _setup-dll-filename_ <b>\\</b> 0]  
  
 [_keyword1_ **=**_value1_ <b>\\</b>0] [_keyword2_ **=** _value2_ <b>\\</b> 0]... <b>\\</b>0  
  
 ここで、\ 0 は null バイトで、 *driver-attr* は any driver attribute キーワードです。 キーワードは、指定された順序で表示される必要があります。 たとえば、フォーマットされたテキストファイルのドライバーに個別のドライバーおよびセットアップ Dll があり、.txt 拡張子と .csv 拡張子を持つファイルを使用できるとします。 このドライバーの *lpszdriver* 引数は、次のようになります。  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 SQL Server 用のドライバーが個別のセットアップ DLL を持たず、driver 属性キーワードを持っていないとします。 このドライバーの *lpszdriver* 引数は、次のようになります。  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 **Sqlinstalldriverex**は、 *lpszdriver*引数からドライバーに関する情報を取得した後、システム情報の Odbcinst.ini エントリの [ODBC ドライバー] セクションにドライバーの説明を追加します。 次に、ドライバーの説明というセクションを作成し、ドライバー DLL とセットアップ DLL の完全なパスを追加します。 最後に、インストール先ディレクトリのパスを返しますが、ドライバーファイルはコピーされません。 呼び出し元のプログラムは、実際にはドライバーファイルをターゲットディレクトリにコピーする必要があります。  
  
 **Sqlinstalldriverex** は、インストールされているドライバーのコンポーネントの使用量を1つ増やします。 ドライバーのバージョンが既に存在していても、そのドライバーのコンポーネントの使用量が存在しない場合、新しいコンポーネントの使用状況のカウント値は2に設定されます。  
  
 アプリケーションセットアッププログラムは、ドライバーファイルを物理的にコピーし、ファイルの使用量を維持する役割を担います。 ドライバーファイルが以前にインストールされていない場合、アプリケーションセットアッププログラムは、 *Lpszpathin* パスのファイルをコピーして、ファイルの使用状況カウントを作成する必要があります。 ファイルが既にインストールされている場合、セットアッププログラムは単にファイルの使用状況カウントをインクリメントし、 *Lpszpathout* 引数内の以前のインストールのパスを返します。  
  
> [!NOTE]  
>  コンポーネントの使用量とファイルの使用量のカウントの詳細については、「 [使用量のカウント](../../../odbc/reference/install/usage-counting.md)」を参照してください。  
  
 以前のバージョンのドライバーファイルがアプリケーションによって既にインストールされている場合は、ドライバーコンポーネントの使用回数が有効になるように、ドライバーをアンインストールしてから再インストールする必要があります。 **Sqlconfigdriver** (ODBC_REMOVE_DRIVER の *frequest* を含む) を最初に呼び出してから、 **sqlconfigdriver** を呼び出して、コンポーネントの使用量を減らす必要があります。 次に、ドライバーを再インストールするために**Sqlinstalldriverex**を呼び出して、コンポーネントの使用量を増やします。 アプリケーションセットアッププログラムは、古いファイルを新しいファイルに置き換える必要があります。 ファイルの使用量は同じままで、古いバージョンのファイルを使用した他のアプリケーションでは、新しいバージョンが使用されるようになります。  
  
> [!NOTE]  
>  ドライバーが既にインストールされていて、別のディレクトリにドライバーをインストールするために **Sqlinstalldriverex** が呼び出されている場合、関数は TRUE を返しますが、 *lpszpathout* には、ドライバーが既にインストールされているディレクトリが含まれます。 *Lpszdriver*引数に入力されたディレクトリは含まれません。  
  
 **Sqlinstalldriverex**でのパスの長さは、2フェーズのインストールプロセスを*可能にし*ます。そのため、アプリケーションでは、 **sqlinstalldriverex**を ODBC_INSTALL_INQUIRY モードの*frequest*で呼び出すことによって、どの*cbpathoutmax*が必要かを判断できます。 これにより、 *Pcbpathout* バッファーで使用可能な合計バイト数が返されます。 その後、 **Sqlinstalldriverex**は、ODBC_INSTALL_COMPLETE の*Frequest*と*Cbpathoutmax*引数を*pcbpathout*バッファーの値に設定し、null 終了文字を指定して呼び出すことができます。  
  
 **Sqlinstalldriverex**に2フェーズモデルを使用しない場合は、stdlib.h> で定義されているように、ターゲット _MAX_PATH ディレクトリのパスのストレージのサイズを定義する*Cbpathoutmax*を設定して、切り捨てが行われないようにする必要があります。  
  
 *Frequest*が ODBC_INSTALL_COMPLETE 場合、 **Sqlinstalldriverex**では、 *lpszpathout*を NULL (または*cbpathoutmax*を0にすることは許可されません) にすることはできません。 *Frequest*が ODBC_INSTALL_COMPLETE の場合、返されるバイト数が*Cbpathoutmax*以上であるときに FALSE が返され、その結果、切り捨てが発生します。  
  
 **Sqlinstalldriverex**が呼び出され、アプリケーションセットアッププログラムによってドライバーファイル (必要に応じて) がコピーされた後、ドライバーのセットアップ DLL は**sqlconfigdriver**を呼び出してドライバーの構成を設定する必要があります。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ドライバー マネージャーのインストール|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
