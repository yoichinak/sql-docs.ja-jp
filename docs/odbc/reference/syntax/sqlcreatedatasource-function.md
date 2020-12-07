---
description: SQLCreateDataSource 関数
title: SQLCreateDataSource 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCreateDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCreateDataSource
helpviewer_keywords:
- SQLCreateDataSource function [ODBC]
ms.assetid: 76ee851a-dca9-40cc-8e9e-eb3f74e560ee
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb65e0906e7b69666dd04824f9c4d0819837d2b2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461214"
---
# <a name="sqlcreatedatasource-function"></a>SQLCreateDataSource 関数
**互換性**  
 導入されたバージョン: ODBC 2.0  
  
 **まとめ**  
 **Sqlcreatedatasource** ユーザーがデータソースを追加できるダイアログボックスを表示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLCreateDataSource(  
     HWND    hwnd,  
     LPSTR   lpszDS);  
```  
  
## <a name="arguments"></a>引数  
 *hwnd*  
 代入親ウィンドウハンドル。  
  
 *lpszDS*  
 代入データソース名。 *Lpszds* には、null ポインターまたは空の文字列を指定できます。  
  
## <a name="returns"></a>戻り値  
 データソースが作成された場合、 **Sqlcreatedatasource**は TRUE を返します。 それ以外の場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlcreatedatasource**が FALSE を返す場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_INVALID_HWND|ウィンドウハンドルが無効です|*Hwnd*引数が無効または NULL でした。|  
|ODBC_ERROR_INVALID_DSN|無効な DSN|*Lpszds*引数に、DSN に対して無効な文字列が含まれていました。|  
|ODBC_ERROR_REQUEST_FAILED|失敗した*要求*|ODBC_ADD_DSN オプションを指定して **Configdsn** を呼び出すことができませんでした。|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|ドライバーまたはトランスレーターセットアップライブラリを読み込めませんでした|ドライバーセットアップライブラリを読み込めませんでした。|  
|ODBC_ERROR_USER_CANCELED|ユーザーが操作を取り消しました|ユーザーが新しいデータソースの作成を取り消しました。|  
|ODBC_ERROR_CREATE_DSN_FAILED|要求された DSN を作成できませんでした|データベースに接続できませんでした。ファイル DSN の **SQLDriverConnect** を呼び出すと、正常に接続できませんでした。<br /><br /> ファイルに書き込めませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 *Hwnd*が null の場合、 **SQLCREATEDATASOURCE**は FALSE を返します。 それ以外の場合は、次の図に示すように、設定するデータソースの種類を選択するためのウィザードページを含む [ **新しいデータソースの作成** ] ダイアログボックスが表示されます。  
  
 ![[新しいデータ ソースの作成] ダイアログ ボックス: 種類の選択](../../../odbc/reference/syntax/media/ch23a.gif "CH23A")  
  
 既定のオプションは [ **ファイルデータソース**] です。 データソースが選択され、 **[次へ** ] がクリックされると、インストールされているドライバーの一覧を含む次のウィザードページが表示されます。  
  
 ![[新しいデータ ソースの作成] ダイアログ ボックス: ドライバーの選択](../../../odbc/reference/syntax/media/ch23b.gif "CH23B")  
  
 **[キャンセル**] をクリックすると、ダイアログボックスが表示されなくなり、 **sqlcreatedatasource**はエラーコード ODBC_ERROR_USER_CANCELED で FALSE を返します。 [ **ユーザーデータソース** ] オプションまたは [ **システムデータソース** ] オプションを選択した場合、 **[詳細設定** ] ボタンは使用できません。  
  
 [ **次へ** ] ボタンをクリックすると、選択されたデータソースの種類に応じて、次のいずれかが発生します。  
  
-   [ **ファイルデータソース** ] が選択されている場合、ユーザーがファイル名を入力するためのウィザードページが表示されます。  
  
-   **ユーザーデータソース**または**システムデータソース**が選択されている場合、データソースとドライバーの種類を表示するウィザードページが表示され、 **[完了**] をクリックすると、データソースが設定されます。  
  
 [新しいデータソースの作成ウィザード] ページで **[詳細設定** ] をクリックすると、ユーザーがドライバー固有の情報を入力するためのウィザードページが表示されます。 このダイアログボックスのテキストボックスに、次の図に示すように、によって区切られたドライバーとキーワードを入力します。  
  
 ![[詳細なファイル DSN の作成設定] ダイアログ ボックス](../../../odbc/reference/syntax/media/ch23c.gif "CH23C")  
  
 ドライバー固有のその他のキーワードについては、 **SQLDriverConnect**の説明を参照してください。 **DSN**以外はすべて許可されます。  
  
 [ **この接続を確認** する] オプションの既定値は TRUE です。 この既定値は、このウィザードページがアクティブになっているかどうかにかかわらず適用されます。 **[OK]** をクリックすると、テキストボックスで指定された文字列と [**この接続を確認**する] オプションの値がキャッシュされます。 ([ **閉じる** ] ボタンまたは **[キャンセル** ] をクリックした場合、テキストボックスで指定された文字列と [ **この接続を確認してください** ] オプションの値がキャッシュされていないため、新しく入力したドライバー固有の情報は失われます)。  
  
 最初のウィザードページで [ **ファイルデータソース** ] を選択した場合、ドライバーが選択され、[詳細設定ウィザード] ページでキーワード値が入力されると、ユーザーはファイル名を入力するように求められます。 [ **参照** ] をクリックしてファイル名を検索します。この場合、[ **参照** ] ボックスの既定のディレクトリは、HKEY_LOCAL_MACHINE \software\microsoft\windows\currentversion と "CommonFileDir" で指定されたパスの組み合わせによって指定されます。 (CommonFileDir が "C:\Program Files\Common Files" の場合、既定のディレクトリは "C:\Program Files\Common Files\ODBC\Data Sources" になります)。  
  
 ファイル名を入力し、 **[次へ** ] をクリックすると、入力したファイル名がオペレーティングシステムの標準のファイル名前付け規則に対して有効かどうかがチェックされます。 ファイル名が無効である場合は、無効なファイル名が入力されたことをユーザーに通知するエラーメッセージボックスが表示されます。 ユーザーがメッセージボックスを確認すると、ファイル名が入力されたウィザードページにフォーカスが戻ります。 ファイル名が有効な場合は、次の図に示すように、選択したキーワードと値のペアを示すウィザードページが表示されます。  
  
 ![[新しいデータ ソースの作成] ダイアログ ボックス: 確認](../../../odbc/reference/syntax/media/ch23d.gif "CH23D")  
  
 **[完了**] をクリックし、データソースの種類として [**ファイルデータソース**] を選択した場合、[**この接続を確認**する] オプションが TRUE の場合、 **SQLDriverConnect**は**SAVEFILE**キーワードと**DRIVER**キーワードを使用して呼び出されます。 *Drivercompletion*引数が SQL_DRIVER_COMPLETE に設定されています。 **SAVEFILE**キーワードのファイル名は、入力または選択された名前です。 **driver**キーワードのドライバー名は、選択された名前です。 [詳細設定ウィザード] ページでドライバー固有の接続文字列を指定した場合、その文字列は **driver** キーワードの後に追加されます。  
  
 **SQLDriverConnect**から SQL_SUCCESS が返された場合、ドライバーマネージャーはファイル DSN を作成しました。 **Sqlcreatedatasource** は TRUE を返します。 **SQLDriverConnect**が SQL_SUCCESS を返さない場合、データソースへの接続を確立できなかったことを示す警告メッセージボックスが表示されます。 最小限の接続情報を含む DSN を作成することもできます。 このメッセージボックスを使用すると、ユーザーはファイル DSN の作成をキャンセルまたは続行できます。  
  
 ユーザーが DSN の作成を続行することを選択した場合、このプロセスは、[ **この接続を確認** する] オプションが FALSE に設定されているかのように続行されます。 ユーザーがキャンセルを選択すると、 **Sqlcreatedatasource** に対して FALSE が返され、エラーコード ODBC_ERROR_CREATE_DSN_FAILED が返されます。  
  
 データソースの種類として [ **ファイルデータソース** ] が選択されていて、[ **この接続を確認** する] オプションが [FALSE] の場合は、[詳細設定ウィザード] ページから、 **DRIVER** キーワードとユーザー指定の接続文字列 (存在する場合) を使用してファイル DSN が作成されます。 ファイルの作成が成功した場合は、 **Sqlcreatedatasource**に対して TRUE が返されます。 ファイルの作成が成功しなかった場合、エラーメッセージボックスによって、オペレーティングシステムから返されたエラーがユーザーに通知されます。 エラーコード ODBC_ERROR_CREATE_DSN_FAILED の **Sqlcreatedatasource** に対して FALSE が返されます。 ファイルデータソースの詳細については、「 [ファイルデータソースを使用した接続](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)」または「 [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)」を参照してください。  
  
 **ユーザー**データソースまたは**システムデータソース**がデータソースの種類として選択されている場合は、ドライバーセットアップライブラリの**Configdsn**が ODBC_ADD_DSN *frequest*を使用して呼び出されます。 詳細については、「 [Configdsn](../../../odbc/reference/syntax/configdsn-function.md)」を参照してください。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|データ ソースの管理|[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|
