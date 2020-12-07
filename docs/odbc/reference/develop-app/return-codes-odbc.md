---
description: リターン コード (ODBC)
title: リターンコード ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 79a06ad170f747c3841c42eadef0288af6fef39a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494638"
---
# <a name="return-codes-odbc"></a>リターン コード (ODBC)
ODBC の各関数は、関数の全体的な成功または失敗を示す *リターンコード* と呼ばれるコードを返します。 一般的に、プログラミング ロジックはリターン コードを基に組み立てます。  
  
 たとえば、次のコードでは、 **Sqlfetch** を呼び出して結果セットの行を取得します。 関数のリターンコードをチェックして、結果セットの末尾に到達したか (SQL_NO_DATA)、警告情報が返されたかどうか (SQL_SUCCESS_WITH_INFO)、またはエラーが発生したか (SQL_ERROR) を確認します。  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
while ((rc=SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (rc == SQL_SUCCESS_WITH_INFO) {  
      // Call function to display warning information.  
   } else if (rc == SQL_ERROR) {  
      // Call function to display error information.  
      break;  
   }  
   // Process row.  
}  
```  
  
 リターン コード SQL_INVALID_HANDLE は常にプログラミング エラーを示します。実行時にはこのコードが返されないようにしてください。 それ以外のリターン コードは実行時の情報を含んでいます。ただし、SQL_ERROR はプログラミング エラーを示す場合もあります。  
  
 次の表では、リターンコードを定義します。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|SQL_SUCCESS|関数は正常に完了しました。 アプリケーションは **SQLGetDiagField** を呼び出して、ヘッダーレコードから追加情報を取得します。|  
|SQL_SUCCESS_WITH_INFO|関数が正常に完了しました。致命的でないエラーが発生した可能性があります (警告)。 アプリケーションは、 **SQLGetDiagRec** または **SQLGetDiagField** を呼び出して、追加情報を取得します。|  
|SQL_ERROR|関数が失敗しました。 アプリケーションは、 **SQLGetDiagRec** または **SQLGetDiagField** を呼び出して、追加情報を取得します。 関数の出力引数の内容は未定義です。|  
|SQL_INVALID_HANDLE|環境、接続、ステートメント、または記述子ハンドルが無効なため、関数が失敗しました。 これは、プログラミングエラーを示します。 **SQLGetDiagRec**または**SQLGetDiagField**から追加情報は入手できません。 このコードは、ハンドルが null ポインターである場合、または接続ハンドルを必要とする引数に対してステートメントハンドルが渡された場合など、間違った型である場合にのみ返されます。|  
|SQL_NO_DATA|使用できるデータがありませんでした。 アプリケーションは、 **SQLGetDiagRec** または **SQLGetDiagField** を呼び出して、追加情報を取得します。 クラス02xxx に1つ以上のドライバーで定義された状態レコードが返される場合があります。 **注:**  ODBC 2 の場合。*x*では、このリターンコードに SQL_NO_DATA_FOUND という名前が付けられていました。|  
|SQL_NEED_DATA|実行時にパラメーターデータを送信する場合や、追加の接続情報が必要な場合など、さらに多くのデータが必要になります。 アプリケーションは、 **SQLGetDiagRec** または **SQLGetDiagField** を呼び出して、追加情報 (存在する場合) を取得します。|  
|SQL_STILL_EXECUTING|非同期的に開始された関数はまだ実行されています。 アプリケーションは、 **SQLGetDiagRec** または **SQLGetDiagField** を呼び出して、追加情報 (存在する場合) を取得します。|
