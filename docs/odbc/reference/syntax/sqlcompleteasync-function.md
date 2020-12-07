---
description: SQLCompleteAsync 関数
title: SQLCompleteAsync 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb5ec8ff7c0aa96e37ce66cabb1e18c9993e95f7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448763"
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync 関数
**互換性**  
 導入されたバージョン: ODBC 3.8 標準準拠: なし  
  
 **まとめ**  
 **Sqlcompleteasync** を使用すると、通知またはポーリングベースの処理のいずれかを使用して非同期関数が完了したかどうかを判断できます。 非同期操作の詳細については、「 [非同期実行](../../../odbc/reference/develop-app/asynchronous-execution.md)」を参照してください。  
  
 **Sqlcompleteasync** は、ODBC ドライバーマネージャーでのみ実装されます。  
  
 通知に基づく非同期処理モードでは、ドライバーマネージャーによって通知に使用されるイベントオブジェクトが生成された後に、 **Sqlcompleteasync** を呼び出す必要があります。 **Sqlcompleteasync** が非同期処理を完了すると、非同期関数によってリターンコードが生成されます。  
  
 ポーリングベースの非同期処理モードでは、元の非同期関数呼び出しで引数を指定しなくても、 **Sqlcompleteasync** を使用して元の非同期関数を呼び出すことができます。 **Sqlcompleteasync** は、ODBC カーソルライブラリが有効になっているかどうかに関係なく使用できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>引数  
 *HandleType*  
 代入非同期処理を完了するハンドルの型。 有効な値は、SQL_HANDLE_DBC または SQL_HANDLE_STMT です。  
  
 *扱え*  
 代入非同期処理を完了するハンドル。 *Handle*が*handletype*によって指定された型の有効なハンドルでない場合、 **sqlcompleteasync**は SQL_INVALID_HANDLE を返します。  
  
 *Handle*が*handletype*によって指定された型の有効なハンドルでない場合、 **sqlcompleteasync**は SQL_INVALID_HANDLE を返します。  
  
 *AsyncRetCodePtr*  
 Output非同期 API のリターンコードを格納するバッファーへのポインター。 *AsyncRetCodePtr*が NULL の場合、 **sqlcompleteasync**は SQL_ERROR を返します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_ERROR、SQL_NO_DATA、または SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診断  
 **Sqlcompleteasync**が SQL_SUCCESS を返す場合、アプリケーションは、 *AsyncRetCodePtr*が指すバッファーから非同期関数のリターンコードを取得する必要があります。 関連する SQLSTATE (存在する場合) は、SQLGetDiagRec SQL_HANDLE_STMT の*Handletype*を使用して**SQLGetDiagRec**を呼び出し、ステートメントハンドル、または SQL_HANDLE_DBC の*handletype*と接続ハンドルを呼び出すことによって取得できます。 これらの診断レコードは、 **Sqlcompleteasync** 関数ではなく、非同期関数に関連付けられています。  
  
 **Sqlcompleteasync** は、 **sqlcompleteasync** が正しく呼び出されないことを示す SQL_SUCCESS 以外のコードを返します。 この場合、 **Sqlcompleteasync**は診断レコードを通知しません。 考えられるリターンコードは次のとおりです。  
  
-   SQL_INVALID_HANDLE: *Handletype* と *handle* によって示されたハンドルが有効なハンドルではありません。  
  
-   SQL_ERROR: *AsyncRetCodePtr* が NULL であるか、ハンドルで非同期処理が有効になっていません。  
  
-   SQL_NO_DATA: 通知モードで、非同期操作が進行中でないか、またはドライバーマネージャーによってアプリケーションに通知されませんでした。 ポーリングモードでは、非同期操作は実行されていません。  
  
## <a name="comments"></a>コメント  
 ポーリングベースの非同期処理モードでは、 **Sqlcompleteasync**が SQL_SUCCESS を返すときに*AsyncRetCodePtr*が SQL_STILL_EXECUTING される可能性があります。 *AsyncRetCodePtr*が SQL_STILL_EXECUTING されないようにするには、アプリケーションでポーリングを続ける必要があります。 通知ベースの非同期処理モードでは、 *AsyncRetCodePtr* が SQL_STILL_EXECUTING されることはありません。  
  
## <a name="see-also"></a>関連項目  
 [非同期実行 (ポーリングメソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
