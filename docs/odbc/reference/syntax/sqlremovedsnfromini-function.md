---
description: SQLRemoveDSNFromIni 関数
title: SQLRemoveDSNFromIni 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDSNFromIni
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDSNFromIni
helpviewer_keywords:
- SQLRemoveDSNFromIni function [ODBC]
ms.assetid: bb2e8273-7b61-4113-bfc8-f7ccc607c811
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f49646881539d7c90c057633e7151b31cfe52b52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499615"
---
# <a name="sqlremovedsnfromini-function"></a>SQLRemoveDSNFromIni 関数
**互換性**  
 導入されたバージョン: ODBC 1.0  
  
 **まとめ**  
 **Sqlremovedsnfromini** は、システム情報からデータソースを削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLRemoveDSNFromIni(  
     LPCSTR   lpszDSN);  
```  
  
## <a name="arguments"></a>引数  
 *lpszDSN*  
 代入削除するデータソースの名前。  
  
## <a name="returns"></a>戻り値  
 関数は、データソースが削除された場合、またはデータソースが Odbc.ini ファイル内にない場合に TRUE を返します。 データソースの削除に失敗した場合は、FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlremovedsnfromini**から FALSE が返された場合、 **sqlインストーラエラー**を呼び出すことによって、関連する* \* pferrorcode*値を取得できます。 次の表は、 **Sqlインストーラエラー**によって返される可能性がある* \* pferrorcode*値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_INVALID_DSN|無効な DSN|*Lpszdsn*引数が無効でした。|  
|ODBC_ERROR_REQUEST_FAILED|要求が失敗しました|インストーラーで、レジストリから DSN 情報を削除できませんでした。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>コメント  
 **Sqlremovedsnfromini** は、システム情報の [ODBC データソース] セクションからデータソース名を削除します。 また、システム情報からデータソースの仕様セクションも削除されます。  
  
 この関数は、ドライバーセットアップライブラリからのみ呼び出す必要があります。  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|データソースの追加、変更、または削除|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)|  
|データソースの追加、変更、または削除|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|既定のデータソースの削除|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|システム情報へのデータソース名の追加|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
