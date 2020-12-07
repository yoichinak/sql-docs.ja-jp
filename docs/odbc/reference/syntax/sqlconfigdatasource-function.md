---
description: SQLConfigDataSource 関数
title: SQLConfigDataSource 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLConfigDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDataSource
helpviewer_keywords:
- SQLConfigDataSource function [ODBC]
ms.assetid: f8d6e342-c010-434e-b1cd-f5371fb50a14
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8849ce5528380e4164a420227395bce5aa436eaa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448745"
---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource 関数
**互換性**  
 導入されたバージョン: ODBC 1.0  
  
 **まとめ**  
 **Sqlconfigdatasource** は、データソースを追加、変更、または削除します。  
  
 **Sqlconfigdatasource**の機能には、 [ODBCCONF.EXE](../../../odbc/odbcconf-exe.md)でアクセスすることもできます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLConfigDataSource(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>引数  
 *hwndParent*  
 代入親ウィンドウハンドル。 ハンドルが null の場合、この関数はダイアログボックスを表示しません。  
  
 *fRequest*  
 代入要求の種類。 *Frequest*引数には、次のいずれかの値が含まれている必要があります。  
  
 ODBC_ADD_DSN: 新しいユーザーデータソースを追加します。  
  
 ODBC_CONFIG_DSN: 既存のユーザーデータソースを構成 (変更) します。  
  
 ODBC_REMOVE_DSN: 既存のユーザーデータソースを削除します。  
  
 ODBC_ADD_SYS_DSN: 新しいシステムデータソースを追加します。  
  
 ODBC_CONFIG_SYS_DSN: 既存のシステムデータソースを変更します。  
  
 ODBC_REMOVE_SYS_DSN: 既存のシステムデータソースを削除します。  
  
 ODBC_REMOVE_DEFAULT_DSN: システム情報から既定のデータソースの仕様セクションを削除します。 (これにより、システム情報の Odbcinst.ini エントリから、既定のドライバー仕様セクションも削除されます。 この *Frequest* は、非推奨の **Sqlremovedefaultdatasource** 関数と同じ機能を実行します)。このオプションが指定されている場合、 **Sqlconfigdatasource** への呼び出しに含まれる他のすべてのパラメーターは null である必要があります。NULL でない場合は無視されます。  
  
 *lpszDriver*  
 代入物理ドライバー名の代わりにユーザーに提示されるドライバーの説明 (通常は、関連付けられている DBMS の名前)。  
  
 *lpszAttributes*  
 代入キーワードと値のペアの形式の、二重の null で終わる属性のリスト。 詳細については、「 [Configdsn](../../../odbc/reference/syntax/configdsn-function.md)」を参照してください。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。 この関数が呼び出されたときにシステム情報にエントリが存在しない場合、関数は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlconfigdatasource**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_INVALID_HWND|ウィンドウハンドルが無効です|*HwndParent*引数が無効であるか、NULL でした。|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|要求の種類が無効です|*Frequest*引数は、次のいずれかではありませんでした:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|ドライバーまたは翻訳者名が無効です|*Lpszdriver*引数が無効でした。 レジストリに見つかりませんでした。|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|無効なキーワードと値のペア|*Lpszattributes*引数に構文エラーが含まれています。|  
|ODBC_ERROR_REQUEST_FAILED|失敗した*要求*|インストーラーは、 *Frequest* 引数によって要求された操作を実行できませんでした。 **Configdsn**の呼び出しが失敗しました。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|ドライバーまたはトランスレーターセットアップライブラリを読み込めませんでした|ドライバーセットアップライブラリを読み込めませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **Sqlconfigdatasource** は、 *lpszdriver* の値を使用して、システム情報からドライバーのセットアップ DLL の完全なパスを読み取ります。 DLL を読み込み、渡されたのと同じ引数を使用して **Configdsn** を呼び出します。  
  
 **Sqlconfigdatasource** は、セットアップ DLL が見つからないか、読み込まれない場合、またはユーザーがダイアログボックスをキャンセルした場合に FALSE を返します。 それ以外の場合は、 **Configdsn**から受け取った状態を返します。  
  
 **Sqlconfigdatasource** は、システム Dsn *Frequest*をユーザー dsn *frequest*s にマップします (ODBC_ADD_SYS_DSN ODBC_ADD_DSN、ODBC_CONFIG_SYS_DSN を ODBC_CONFIG_DSN に、ODBC_REMOVE_SYS_DSN に ODBC_REMOVE_DSN)。 ユーザー Dsn とシステム Dsn を区別するために、 **Sqlconfigdatasource** は、次の表に従ってインストーラー構成モードを設定します。 **Sqlconfigdatasource**は、戻る前に、構成モードを両方の dsn にリセットします。 **Configdsn** (ドライバーによって実装されます) は、 **Sqlwritedsntoini** と **sqlwriteprivateprofilestring** を呼び出してシステム DSN をサポートする必要があります。 詳細については、「 [Configdsn 関数](../../../odbc/reference/syntax/configdsn-function.md)」を参照してください。  
  
|*fRequest*|構成モード|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|データソースの追加、変更、または削除|[Configdsn](../../../odbc/reference/syntax/configdsn-function.md) (セットアップ DLL 内)|  
|システム情報からのデータソース名の削除|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|システム情報へのデータソース名の追加|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
