---
description: イベント パラメーター
title: イベントパラメーター |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
author: rothja
ms.author: jroth
ms.openlocfilehash: cc36f0ab059bb7b605b02316008a969411663a8d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991303"
---
# <a name="event-parameters"></a>イベント パラメーター
すべてのイベントハンドラーには、イベントハンドラーを制御する状態パラメーターがあります。 完全なイベントの場合、このパラメーターは、イベントを生成した操作の成功または失敗を示すためにも使用されます。 ほとんどの完全なイベントには、発生したエラーに関する情報や、操作の実行に使用される ADO オブジェクトを参照する1つ以上のオブジェクトパラメーターも含まれています。 たとえば、 [ExecuteComplete](../../reference/ado-api/executecomplete-event-ado.md) イベントには、イベントに関連付けられている **コマンド**、 **レコードセット**、および **接続** オブジェクトのオブジェクトパラメーターが含まれます。 次の Microsoft® Visual Basic®例では、 **Execute**メソッドによって使用される**コマンド**、**レコードセット**、および**接続**オブジェクトを表す Pcommand、pcommand、および pcommand オブジェクトを確認できます。  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 **Error**オブジェクトを除き、同じパラメーターがイベントに渡されます。 これにより、保留中の操作で使用される各オブジェクトを確認し、操作の完了を許可する必要があるかどうかを判断できます。  
  
 一部のイベントハンドラーには *Reason* パラメーターがあり、これによってイベントが発生した理由に関する追加情報が提供されます。 たとえば、 **MoveComplete**イベントが発生するのは、いずれかのナビゲーションメソッド (**MoveNext**、 **MovePrevious**など) が呼び出されているか、または再クエリの結果として発生**したため**です。  
  
## <a name="status-parameter"></a>状態パラメーター  
 イベントハンドラールーチンが呼び出されると、 *Status* パラメーターは次のいずれかの値に設定されます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**adStatusOK**|両方に渡され、イベントが完了します。 この値は、イベントの原因となった操作が正常に完了したことを示します。|  
|**Adstatuserrorの Curred**|完全なイベントにのみ渡されます。 この値は、イベントの原因となった操作が失敗したことを意味します。または、イベントによって操作が取り消されます。 詳細については、 *エラー* パラメーターを確認してください。|  
|**adStatusCantDeny**|に渡されるのはイベントのみです。 この値は、operation イベントによって操作を取り消すことができないことを意味します。 実行する必要があります。|  
  
 操作を続行するかどうかをイベントで判断した場合は、 *Status* パラメーターを変更しないままにします。 ただし、着信状態パラメーターが **Adstatuscantdeny**に設定されていない限り、 *状態* を **adstatuscancel**に変更することによって保留中の操作を取り消すことができます。 これを行うと、操作に関連付けられている Complete イベントの *Status* パラメーターが **Adstatuserrorの curred**に設定されます。 Complete イベントに渡される **Error** オブジェクトには、値 **adErrOperationCancelled**が含まれます。  
  
 イベントを処理する必要がなくなった場合は、 *Status* を **adStatusUnwantedEvent** に設定すると、アプリケーションはそのイベントの通知を受信しなくなります。 ただし、一部のイベントは複数の理由で発生する可能性があることに注意してください。 その場合は、考えられる理由ごとに **adStatusUnwantedEvent** を指定する必要があります。 たとえば、保留中の**Recordchange**イベントの通知の受信を停止するには、 **Adrsnaddnew**、 **adrsnaddnew**、 **adrsnaddnew**、 **AdRsnUndoUpdate**、 **adRsnUndoAddNew**、 **adRsnUndoDelete**、および**Adrsnfirstchange**が発生したときに、 *Status*パラメーターを**adStatusUnwantedEvent**に設定する必要があります。  
  
|[値]|説明|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|このイベントハンドラーがこれ以上通知を受信しないことを要求します。|  
|**adStatusCancel**|発生しようとしている操作のキャンセルを要求します。|  
  
## <a name="error-parameter"></a>エラーパラメーター  
 *Error*パラメーターは ADO [error](../../reference/ado-api/error-object.md)オブジェクトへの参照です。 *Status*パラメーターを**Adstatuserrorの curred**に設定すると、**エラー**オブジェクトには、操作が失敗した理由の詳細が含まれます。 Complete イベントに関連付けられているイベントが、 *Status* パラメーターを **adstatuscancel**に設定して操作を取り消した場合、error オブジェクトは常に **adErrOperationCancelled**に設定されます。  
  
## <a name="object-parameter"></a>オブジェクトパラメーター  
 各イベントは、操作に関係するオブジェクトを表す1つ以上のオブジェクトを受け取ります。 たとえば、 **ExecuteComplete** イベントは、 **コマンド** オブジェクト、 **レコードセット** オブジェクト、および **接続** オブジェクトを受け取ります。  
  
## <a name="reason-parameter"></a>理由パラメーター  
 *Reason*パラメーター *adReason*は、イベントが発生した理由に関する追加情報を提供します。 *AdReason*パラメーターを持つイベントは、同じ操作でも、毎回異なる理由で複数回呼び出すことができます。 たとえば、レコードの挿入、削除、または変更を実行しようとしている操作に対して **、イベントハンドラー** が呼び出されます。 特定の理由で発生したイベントのみを処理する場合は、 *adReason* パラメーターを使用して、関心のないオカレンスを除外することができます。 たとえば、レコードが追加されたことが原因でレコード変更イベントが発生した場合にのみ処理するには、次のようにします。  
  
```  
' BeginEventExampleVB01  
Private Sub rsTest_WillChangeRecord(ByVal adReason As ADODB.EventReasonEnum, ByVal cRecords As Long, adStatus As ADODB.EventStatusEnum, ByVal pRecordset As ADODB.Recordset)  
   If adReason = adRsnAddNew Then  
       ' Process event  
       '...  
   Else  
       ' Cancel event notification for all  
       ' other possible adReason values.  
       adStatus = adStatusUnwantedEvent  
   End If  
End Sub  
' EndEventExampleVB01  
```  
  
 この場合、その他の理由ごとに通知が発生する可能性があります。 ただし、これは、それぞれの理由で1回だけ発生します。 各理由で通知が1回発生すると、新しいレコードの追加についてのみ通知が送信されます。  
  
 これに対して、 *Adstatus* を **adStatusUnwantedEvent** に1回だけ設定して、 **adReason** パラメーターを持たないイベントハンドラーがイベント通知の受信を停止するように要求する必要があります。  
  
## <a name="see-also"></a>参照  
 [ADO イベントハンドラーの概要](./ado-event-handler-summary.md)   
 [言語による ADO イベントのインスタンス化](./ado-event-instantiation-by-language.md)   
 [イベントハンドラーの連携方法](./how-event-handlers-work-together.md)   
 [イベントの種類](./types-of-events.md)