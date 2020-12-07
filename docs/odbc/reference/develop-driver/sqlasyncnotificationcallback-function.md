---
description: SQLAsyncNotificationCallback 関数
title: SQLAsyncNotificationCallback 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b9d03e8a3fa7e62c19dd09a210dca3a56348c692
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476231"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 関数
**互換性**  
 導入されたバージョン: ODBC 3.8  
  
 標準への準拠: なし  
  
 **まとめ**  
 ドライバーが SQL_STILL_EXECUTING を返した後、現在の非同期操作の進行状況が発生したときに、ドライバーがドライバーマネージャーにコールバックできるようにするには、 **Sqlasyncnotificationcallback**を使用します。 **Sqlasyncnotificationcallback** は、ドライバーによってのみ呼び出すことができます。  
  
 ドライバーは、 **sqlasyncnotificationcallback 関数名を**指定して**sqlasyncnotificationcallback**を呼び出しません。 代わりに、ドライバーマネージャーは、対応する接続ハンドルまたはステートメントハンドルの SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK または SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 属性の値として、関数ポインターをドライバーに渡します。 異なるハンドルに異なる関数ポインターの値を割り当てることができます。 関数ポインターの型は SQL_ASYNC_NOTIFICATION_CALLBACK として定義されます。  
  
 **Sqlasyncnotificationcallback** はスレッドセーフです。 ドライバーでは、複数のスレッドを使用して、異なるハンドルで同時に **Sqlasyncnotificationcallback** を呼び出すことができます。  
  
## <a name="syntax"></a>構文  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>引数  
 *Pcontrol Ex*  
 ドライバーマネージャーによって定義されたデータ構造体へのポインター。 値は、SQLSetConnectAttr (SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) または SQLSetStmtAttr (SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT) を使用してドライバーに渡されます。  ドライバーは、値にアクセスできません。  
  
 *fLast*  
 このコールバック関数呼び出しが、現在の非同期操作の最後の呼び出しであることを示すために、ドライバーによって使用されます。 ドライバーマネージャーが関数を再度呼び出すときに、ドライバーは SQL_STILL_EXECUTING 以外のリターンコードを返します。 ドライバーマネージャーは、たとえば、この情報を使用して、非同期操作が完了する前にアプリケーションに通知することができます。  
  
 *Handle*が*handletype*によって指定された型の有効なハンドルでない場合、 **sqlcancelhandle**は SQL_INVALID_HANDLE を返します。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS または SQL_ERROR。  
  
## <a name="diagnostics"></a>診断  
 **Sqlasyncnotificationcallback** は、次の2つの状況で SQL_ERROR を返すことができます (これらは、ドライバーまたはドライバーマネージャーの実装の問題を示します)。  
  
|エラー|説明|  
|-----------|-----------------|  
|接続またはステートメントが通知を要求しませんでした。||  
|無効な *ハンドル*|ドライバーが無効なハンドルで渡されました。このハンドルは、内部ドライバーマネージャーの検証テストに失敗しました。|  
  
## <a name="see-also"></a>関連項目  
 [非同期実行 (ポーリングメソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
