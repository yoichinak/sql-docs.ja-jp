---
description: SQLValidDSN 関数
title: SQLValidDSN 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLValidDSN
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLValidDSN
helpviewer_keywords:
- SQLValidDSN [ODBC]
ms.assetid: 930d1d89-337a-4429-85a2-84ee10555ac9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62692ed4b5d0ab600ceb36e87e7f796c77120c89
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99191708"
---
# <a name="sqlvaliddsn-function"></a>SQLValidDSN 関数
**互換性**  
 導入されたバージョン: ODBC 2.0  
  
 **要約**  
 **Sqlvaliddsn** は、システム情報に名前を追加する前に、データソース名の長さと有効性をチェックします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
BOOL SQLValidDSN(  
     LPCSTR    lpszDSN);  
```  
  
## <a name="arguments"></a>引数  
 *lpszDSN*  
 代入確認するデータソース名。  
  
## <a name="returns"></a>戻り値  
 関数は、データソース名が有効である場合に TRUE を返します。 データソース名が無効な場合、または関数呼び出しが失敗した場合は、FALSE を返します。  
  
## <a name="diagnostics"></a>診断  
 **Sqlvaliddsn** から FALSE が返された場合、 **sqlインストーラエラー** を呼び出すことによって、関連する *\* pferrorcode* 値を取得できます。 データソース名が無効であるために FALSE が返された場合にのみ、関数呼び出しが失敗した場合にのみ、 *\* pferrorcode* が返されます。 次の表は、 **Sqlインストーラエラー** によって返される可能性がある *\* pferrorcode* 値と、この関数のコンテキストにおけるそれぞれの値を示しています。  
  
|*\*pfErrorCode*|エラー|説明|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|一般的なインストーラーエラー|特定のインストーラーエラーがなかったためにエラーが発生しました。|  
|ODBC_ERROR_OUT_OF_MEM|メモリ不足|メモリ不足のため、インストーラーで関数を実行できませんでした。|  
  
## <a name="comments"></a>説明  
 **Sqlvaliddsn** は、データソース名の長さとデータソース名の個々の文字の有効性を確認するために、ドライバーの [configdsn](../../../odbc/reference/syntax/configdsn-function.md) によって呼び出されます。 名前の長さが SQL_MAX_DSN_LENGTH より大きいかどうかをチェックします。 Sqlext の定義に従ってください。 (データソース名の長さも [Sqlwritedsntoini](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)によって確認されます)。 **Sqlvaliddsn** は、次の無効な文字のいずれかがデータソース名に含まれているかどうかを確認します。  
  
 [ ] { } ( ) , ; ? * = ! \@ \  
  
## <a name="related-functions"></a>関連する関数  
  
|対象|解決方法については、|  
|---------------------------|---------|  
|データソースの追加、変更、または削除|[Configdsn](../../../odbc/reference/syntax/configdsn-function.md) (セットアップ DLL 内)|  
|データソースの追加、変更、または削除|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|システム情報へのデータソース名の書き込み|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|
