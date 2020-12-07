---
description: SQLManageDataSources
title: SQLManageDataSources ソース |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLManageDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLManageDataSources
helpviewer_keywords:
- SQLManageDataSources [ODBC]
ms.assetid: ac6d186f-b394-406c-94c4-c6331d1ca468
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81f4616cb04d5d17cca687843d28efa1027ff65f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460975"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**互換性**  
 導入されたバージョン: ODBC 2.0  
  
 **まとめ**  
 [ **Sqlmanagedatasources** ] ユーザーがシステム情報でデータソースを設定、追加、および削除できるダイアログボックスを表示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>引数  
 *hwnd*  
 代入親ウィンドウハンドル。  
  
## <a name="returns"></a>戻り値  
 *Hwnd*が有効なウィンドウハンドルでない場合、 **Sqlmanagedatasources データソース**は FALSE を返します。 それ以外の場合には、TRUE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlmanagedatasources ソース**が FALSE を返すと、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_REQUEST_FAILED|失敗した*要求*|**Configdsn**の呼び出しが失敗しました。|  
|ODBC_ERROR_INVALID__HWND|ウィンドウハンドルが無効です|*Hwnd*引数が無効または NULL でした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="managing-data-sources"></a>データ ソースの管理  
 **Sqlmanagedatasources** ソースでは、次の図に示すように、最初に [ **ODBC データソースアドミニストレーター** ] ダイアログボックスが表示されます。  
  
 ![[ODBC データ ソース管理者] ダイアログ ボックス](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 このダイアログボックスには、システム情報に一覧表示されたデータソースが、[ **ユーザー dsn**]、[ **システム dsn**]、[ **ファイル dsn**] の3つのタブに表示されます。 ユーザーがデータソースをダブルクリックするか、データソースを選択して [構成] をクリック **する**と、 **sqlmanagedatasources** は ODBC_CONFIG_DSN オプションを使用してセットアップ DLL 内の **configdsn** を呼び出します。  
  
 ユーザーが [ **追加**] をクリックすると、次の図に示すように、 **Sqlmanagedatasources** ソースで [ **新しいデータソースの作成** ] ダイアログボックスが表示されます。  
  
 ![[新しいデータ ソースの作成] ダイアログ ボックス](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 ダイアログボックスに、インストールされているドライバーの一覧が表示されます。 ユーザーがドライバーをダブルクリックするか、ドライバーを選択して **[OK]** をクリックすると、 **sqlmanagedatasources データソース** はセットアップ DLL で **configdsn** を呼び出し、ODBC_ADD_DSN オプションとして渡します。  
  
 ユーザーがデータソースを選択し、[ **削除**] をクリックすると、 **sqlmanagedatasources** は、ユーザーがデータソースを削除するかどうかを確認します。 ユーザーが **[はい]** をクリックすると、 **sqlmanagedatasources データソース** は、ODBC_REMOVE_DSN オプションを使用してセットアップ DLL 内の **configdsn** を呼び出します。  
  
 ユーザーデータソース、システムデータソース、またはファイルデータソースを追加または削除するには、[ **新しいデータソースの作成** ] ダイアログボックスを使用します。  
  
## <a name="user-dsns"></a>ユーザー Dsn  
 個々のユーザーに対して作成された Dsn は、システム Dsn と区別するために、ユーザー Dsn と呼ばれます。 ユーザー Dsn は、システム情報で次のように登録されます。  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>システム Dsn  
 [ **新しいデータソースの作成** ] ダイアログボックスを使用すると、ローカルコンピューターにシステムデータソースを追加したり、システムデータソースを削除したり、システムデータソースの構成を設定したりできます。  
  
 システムデータソース名 (DSN) を使用して設定されたデータソースは、同じコンピューター上の複数のユーザーが使用できます。 また、システム全体のサービスでも使用できます。これにより、コンピューターにログオンしているユーザーがいない場合でも、データソースにアクセスできます。  
  
 システム DSN は、HKEY_CURRENT_USER エントリではなく、システム情報の HKEY_LOCAL_MACHINE エントリに登録されます。 特定のユーザー名とパスワードでログオンした1人のユーザーには関連付けられていませんが、そのコンピューターの任意のユーザーまたは自動システム全体のサービスによって使用できます。 ただし、システム DSN は、1台のコンピューターに関連付けられています。 コンピューター間でリモート Dsn を使用する機能はサポートされていません。 システム Dsn は、システム情報で次のように登録されます。  
  
 HKEY_LOCAL_MACHINE SOFTWARE ODBC Odbc.ini  
  
## <a name="file-dsns"></a>ファイル Dsn  
 ファイルデータソースには、マシンデータソースと同じようにデータソース名がなく、1つのユーザーまたはコンピューターに登録されていません。 そのデータソースの接続情報は、任意のコンピューターにコピーできる dsn ファイルに格納されています。 ファイルデータソースは、共有することができます。この場合、dsn ファイルはネットワーク上に存在し、ユーザーが適切なドライバーをインストールしていれば、ネットワーク上の複数のユーザーが同時に使用することができます。 ファイルデータソースは unshareable することもできます。この場合、1台のコンピューターでのみ使用できます。  
  
 ファイルデータソースの詳細については、「 [ファイルデータソースを使用した接続](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)」または「 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)」を参照してください。  
  
## <a name="managing-drivers"></a>ドライバーの管理  
 ユーザーが [ **Odbc データソースアドミニストレーター** ] ダイアログボックスの [**ドライバー** ] タブをクリックすると、システムにインストールされている odbc ドライバーの一覧と、ドライバーに関する情報**が表示さ**れます。 表示される日付は、次の図に示すように、ドライバーの作成日です。  
  
 ![[ODBC データ ソース管理者のドライバー] タブ](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>[トレース オプション]  
 ユーザーが [ **ODBC データソースアドミニストレーター** ] ダイアログボックスの [**トレース**] タブをクリックすると、次の図に示すように、 **sqlmanagedatasources**ソースにトレースオプションが表示されます。  
  
 ![[ODBC データ ソース管理者のトレース] タブ](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 ユーザーが [ **今すぐトレースを開始** ] をクリックし、[ **OK]** をクリックすると、 **sqlmanagedatasources データソース** によって、コンピューターで現在実行されているすべてのアプリケーションのトレースが手動で有効になります。  
  
 ユーザーが [ **ログファイルのパス** ] テキストボックスにトレースファイルの名前を指定し、[ **OK**] をクリックすると、 **sqlmanagedatasources ソース** はシステム情報の [ODBC] セクションにある **tracefile** キーワードを指定された名前に設定します。  
  
> [!IMPORTANT]  
>  Visual Studio Analyzer のサポートは、Windows 8 以降で削除されました (Visual Studio Analyzer 以前のバージョンの Visual Studio にのみ含まれていました)。 別のトラブルシューティングメカニズムについては、BID トレースを使用します。  
  
 ユーザーが [ **スタート Visual Studio Analyzer** をクリックし、[ **OK]** をクリックすると、Visual Studio Analyzer が有効になります。 **停止 Visual Studio Analyzer**がクリックされるまで有効のままです。  
  
 トレースの詳細については、「 [トレース](../../../odbc/reference/develop-app/tracing.md)」を参照してください。 **Trace**および**tracefile**キーワードの詳細については、「 [ODBC サブキー](../../../odbc/reference/install/odbc-subkey.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|データ ソースの作成|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
