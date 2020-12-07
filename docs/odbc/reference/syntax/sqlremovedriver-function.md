---
description: SQLRemoveDriver 関数
title: SQLRemoveDriver 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDriver
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDriver
helpviewer_keywords:
- SQLRemoveDriver function [ODBC]
ms.assetid: 9a3b4f8b-982b-44b9-ade6-754ff026dc90
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 503fadfae168a2fc7259cd0507b283563d681bf7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487070"
---
# <a name="sqlremovedriver-function"></a>SQLRemoveDriver 関数
**互換性**  
 導入されたバージョン: ODBC 3.0  
  
 **まとめ**  
 **Sqlremovedriver** は、システム情報の Odbcinst.ini エントリからドライバーに関する情報を変更または削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLRemoveDriver(  
     LPCSTR   lpszDriver,  
     BOOL     fRemoveDSN,  
     LPDWORD  lpdwUsageCount);  
```  
  
## <a name="arguments"></a>引数  
 *lpszDriver*  
 代入システム情報の Odbcinst.ini キーに登録されているドライバーの名前。  
  
 *fRemoveDSN*  
 代入有効な値は次のとおりです。  
  
 TRUE: *Lpszdriver*に指定されているドライバーに関連付けられている Dsn を削除します。 FALSE: *Lpszdriver*に指定されているドライバーに関連付けられている dsn を削除しないでください。  
  
 *lpdwUsageCount*  
 Outputこの関数が呼び出された後のドライバーの使用カウント。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。 この関数が呼び出されたときにシステム情報にエントリが存在しない場合、関数は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlremovedriver**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_COMPONENT_NOT_FOUND|コンポーネントがレジストリに見つかりません|インストーラーはレジストリに存在しないか、レジストリに見つからなかったため、ドライバー情報を削除できませんでした。|  
|ODBC_ERROR_INVALID_NAME|ドライバーまたは翻訳者名が無効です|*Lpszdriver*引数が無効でした。|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|コンポーネントの使用状況カウントをインクリメントまたはデクリメントできませんでした|インストーラーはドライバーの使用状況カウントを減らすことができませんでした。|  
|ODBC_ERROR_REQUEST_FAILED|要求が失敗しました|*Fremovedsn*引数が TRUE でした。ただし、1つまたは複数の Dsn を削除できませんでした。 ODBC_REMOVE_DRIVER 要求で **Sqlconfigdriver** を呼び出すことができませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **Sqlremovedriver** は [Sqlinstalldriverex](../../../odbc/reference/syntax/sqlinstalldriverex-function.md) 関数を補完し、システム情報のコンポーネントの使用量を更新します。 この関数は、セットアップアプリケーションからのみ呼び出す必要があります。  
  
 **Sqlremovedriver** は、コンポーネントの使用状況カウントの値を1だけデクリメントします。 コンポーネントの使用量が0になると、次のようになります。  
  
1.  ODBC_REMOVE_DRIVER オプションを指定した **Sqlconfigdriver** 関数が呼び出されます。 *Fremovedsn*オプションが TRUE に設定されている場合、 **configdsn**関数は、「 *lpszdriver* 」で指定されたドライバーに関連付けられているすべてのデータソースを削除するために、 **sqlremovedsnfromini**を呼び出します。 *Fremovedsn*オプションが FALSE に設定されている場合、データソースは削除されません。  
  
2.  システム情報のドライバーエントリは削除されます。 ドライバーのエントリは、次のドライバー名の下のシステム情報の場所にあります。  
  
     `HKEY_LOCAL_MACHINE`  
  
     `SOFTWARE`  
  
     `ODBC`  
  
     `Odbcinst.ini`  
  
 **Sqlremovedriver** は、実際にはファイルを削除しません。 呼び出し元のプログラムは、ファイルを削除し、ファイルの使用量を保持する役割を担います。 コンポーネントの使用量カウントとファイル使用量カウントの両方がゼロになった後にのみ、ファイルは物理的に削除されます。 ファイルの使用量が増加した他のアプリケーションによってファイルが使用されているかどうかによって、コンポーネント内の一部のファイルを削除したり、他のファイルを削除したりすることはできません。  
  
 **Sqlremovedriver** は、アップグレードプロセスの一部としても呼び出されます。 アプリケーションでアップグレードを実行する必要があることが検出され、ドライバーが既にインストールされている場合は、ドライバーを削除してから再インストールする必要があります。 コンポーネントの使用量を減らすには、まず**Sqlremovedriver**を呼び出す必要があります。その後、コンポーネントの使用量を増やすには、 **Sqlinstalldriverex**を呼び出す必要があります。 アプリケーションセットアッププログラムは、古いファイルを新しいファイルに置き換える必要があります。 ファイルの使用量は変わりません。古いバージョンのファイルを使用するその他のアプリケーションでは、新しいバージョンが使用されるようになります。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|ドライバーの追加、変更、または削除|[Configdriver](../../../odbc/reference/syntax/configdriver-function.md) (セットアップ DLL 内)|  
|ドライバーの追加、変更、または削除|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|  
|ドライバーのインストール|[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|
