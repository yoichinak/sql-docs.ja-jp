---
description: WillChangeRecord および RecordChangeComplete イベント (ADO)
title: Changerecord イベントと RecordChangeComplete イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
author: rothja
ms.author: jroth
ms.openlocfilehash: e22e922a240643d499408dda3941fdf638a529ff
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987863"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord および RecordChangeComplete イベント (ADO)
この **イベントは、** [レコードセット](./recordset-object-ado.md) の1つ以上のレコード (行) が変更される前に呼び出されます。 **RecordChangeComplete**イベントは、1つ以上のレコードが変更された後に呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *adReason*  
 このイベントの理由を指定する [Eventreason 列挙](./eventreasonenum.md) 値。 この値には、 **Adrsnaddnew**、 **adrsnaddnew**、 **adrsnaddnew**、 **adRsnUndoUpdate**、 **AdRsnUndoAddNew**、 **adRsnUndoDelete**、または **adrsnfirstchange**を指定できます。  
  
 *cRecords*  
 変更されるレコードの数を示す **Long** 値 (影響を受けます)。  
  
 *pError*  
 [エラー](./error-object.md)オブジェクトです。 *Adstatus*の値が**adstatuserrorて**いる場合に発生したエラーについて説明します。それ以外の場合は設定されません。  
  
 *adStatus*  
 [Eventstatusenum](./eventstatusenum.md)状態の値です。  
  
 が **呼び出されたときに** 、イベントを発生させた操作が成功した場合、このパラメーターは **adstatusok** に設定されます。 このイベントが保留中の操作の取り消しを要求できない場合は、 **Adstatuscantdeny** に設定されます。  
  
 **RecordChangeComplete**が呼び出されると、このパラメーターは、イベントの原因となった操作が成功した場合は**adstatusok**に、操作が失敗した場合は**Adstatuserror curred**に設定されます。  
  
 このパラメーターを**Adstatuscancel**に設定し**てから、** このイベントの原因となった操作の取り消しを要求するか、このパラメーターを**adStatusUnwantedEvent**に設定して後続の通知を防止します。  
  
 **RecordChangeComplete**が返される前に、このパラメーターを**adStatusUnwantedEvent**に設定して、後続の通知が行われないようにします。  
  
 *pRecordset*  
 **レコードセット**オブジェクトです。 このイベントが発生した **レコードセット** 。  
  
## <a name="remarks"></a>解説  
 [Update](./update-method.md)、 [Delete](./delete-method-ado-recordset.md)、 [CancelUpdate](./cancelupdate-method-ado.md)、 [AddNew](./addnew-method-ado.md)、 [UpdateBatch](./updatebatch-method.md)、および[CancelBatch](./cancelbatch-method-ado.md)の各**レコードセット**操作により、行の最初に変更されたフィールドに対して、 **RecordChangeComplete**イベントが**発生する可能性**があります。 **レコードセット** [CursorType](./cursortype-property-ado.md)の値によって、イベントを発生させる操作が決定されます。  
  
 このイベントでは、**レコードセット**[フィルター](./filter-property.md)プロパティが**adFilterAffectedRecords**に設定さ**れてい**ます。 イベントの処理中にこのプロパティを変更することはできません。  
  
 **AdReason**パラメーターを含むイベントのイベント通知を完全に停止するには、使用可能な**adReason**値ごとに**adstatus**パラメーターを**adStatusUnwantedEvent**に設定する必要があります。  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](./ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../guide/data/ado-event-handler-summary.md)