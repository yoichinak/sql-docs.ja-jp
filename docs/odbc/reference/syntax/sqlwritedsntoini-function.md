---
description: SQLWriteDSNToIni 関数
title: SQLWriteDSNToIni 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWriteDSNToIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWriteDSNToIni
helpviewer_keywords:
- SQLWriteDSNToIni [ODBC]
ms.assetid: dc7018b2-18d4-4657-96d0-086479a47474
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 08a1094d29bbba9dc52974bd1cef5cd6645aa5dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421016"
---
# <a name="sqlwritedsntoini-function"></a>SQLWriteDSNToIni 関数
**互換性**  
 導入されたバージョン: ODBC 1.0  
  
 **まとめ**  
 **Sqlwritedsntoini** は、システム情報にデータソースを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLWriteDSNToIni(  
     LPCSTR   lpszDSN,  
     LPCSTR   lpszDriver);  
```  
  
## <a name="arguments"></a>引数  
 *lpszDSN*  
 代入追加するデータソースの名前。  
  
 *lpszDriver*  
 代入物理ドライバー名の代わりにユーザーに提示されるドライバーの説明 (通常は、関連付けられている DBMS の名前)。  
  
## <a name="returns"></a>戻り値  
 関数は、成功した場合は TRUE、失敗した場合は FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlwritedsntoini**が FALSE を返す場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_INVALID_DSN|無効な DSN|*Lpszdsn*引数に、dsn に対して無効な文字列が含まれていました。|  
|ODBC_ERROR_INVALID_NAME|ドライバーまたは翻訳者名が無効です|*Lpszdriver*引数が無効でした。|  
|ODBC_ERROR_REQUEST_FAILED|要求が失敗しました|インストーラーで、レジストリに DSN を作成できませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **Sqlwritedsntoini** によって、データソースがシステム情報の [ODBC データソース] セクションに追加されます。 次に、データソースの仕様セクションを作成し、その値としてドライバー DLL の名前を持つ単一のキーワード (**driver**) を追加します。 [データソースの指定] セクションが既に存在する場合は、新しいセクションを作成する前に、 **Sqlwritedsntoini** によって古いセクションが削除されます。  
  
 この関数の呼び出し元は、ドライバー固有のキーワードと値を、システム情報のデータソースの仕様セクションに追加する必要があります。  
  
 データソースの名前が既定値の場合、 **Sqlwritedsntoini** は、システム情報の既定のドライバー仕様セクションも作成します。  
  
 この関数は、セットアップ DLL からのみ呼び出す必要があります。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|データソースの追加、変更、または削除|[Configdsn](../../../odbc/reference/syntax/configdsn-function.md)(セットアップ DLL 内)|  
|データソースの追加、変更、または削除|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|システム情報からのデータソース名の削除|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|
