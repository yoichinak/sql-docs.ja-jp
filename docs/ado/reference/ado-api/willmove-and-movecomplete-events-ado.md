---
description: WillMove および MoveComplete イベント (ADO)
title: 移動イベントと MoveComplete イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Recordset::MoveComplete
- WillMove
- MoveComplete
- Recordset::WillMove
helpviewer_keywords:
- MoveComplete event [ADO]
- WillMove event [ADO]
ms.assetid: 1a3d1042-4f30-4526-a0c7-853c242496db
author: rothja
ms.author: jroth
ms.openlocfilehash: 46c28cd74fcf7a580d6695e21cd1e5e2750f0519
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99166255"
---
# <a name="willmove-and-movecomplete-events-ado"></a>WillMove および MoveComplete イベント (ADO)
"イベントの **移動** " は、保留中の操作が [レコードセット](./recordset-object-ado.md)内の現在の位置を変更する前に呼び出されます。 **MoveComplete** イベントは、**レコードセット** 内の現在の位置が変更された後に呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *adReason*  
 このイベントの理由を指定する [Eventreason 列挙](./eventreasonenum.md) 値。 この値には、 **Adrsnmovefirst**、 **adrsnmovefirst**、 **adrsnmovefirst**、 **adRsnMovePrevious**、 **Adrsnmovefirst**、または **adrsnmovefirst** を指定できます。  
  
 *pError*  
 [エラー](./error-object.md)オブジェクトです。 *Adstatus* の値が **adstatuserrorて** いる場合に発生したエラーについて説明します。それ以外の場合、パラメーターは設定されません。  
  
 *adStatus*  
 [Eventstatusenum](./eventstatusenum.md)状態の値です。  
  
 を呼び **出すと、** イベントの原因となった操作が成功した場合、このパラメーターは **adstatusok** に設定されます。 このイベントが保留中の操作の取り消しを要求できない場合は、 **Adstatuscantdeny** に設定されます。  
  
 **MoveComplete** が呼び出されると、このパラメーターは、イベントの原因となった操作が成功した場合は **adstatusok** に、操作が失敗した場合は **Adstatuserror curred** に設定されます。  
  
 が **戻る前に** 、このパラメーターを **adstatuscancel** に設定して保留中の操作の取り消しを要求するか、このパラメーターを **adStatusUnwantedEvent** に設定して、後続の通知が行われないようにします。  
  
 **MoveComplete** が返される前に、このパラメーターを **adStatusUnwantedEvent** に設定して、後続の通知が行われないようにします。  
  
 *pRecordset*  
 [レコードセット](./recordset-object-ado.md)オブジェクトです。 このイベントが発生した **レコードセット** 。  
  
## <a name="remarks"></a>コメント  
 [Open](./open-method-ado-recordset.md)、 [Move](./move-method-ado.md)、 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveLast](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveNext](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [AddNew](./addnew-method-ado.md)、および [Requery](./requery-method.md)の各 **レコードセット** 操作によって、 **MoveComplete** イベントが **発生する可能性** があります。 これらのイベントは、 [Filter](./filter-property.md)、 [Index](./index-property.md)、 [Bookmark](./bookmark-property-ado.md)、 [AbsolutePage](./absolutepage-property-ado.md)、および [AbsolutePosition](./absoluteposition-property-ado.md)の各プロパティによって発生することがあります。 これらのイベントは、子 **レコード** セットに **レコードセット** イベントが関連付けられていて、親 **レコードセット** が移動された場合にも発生します。  
  
 *AdReason* パラメーターを含むイベントのイベント通知を完全に停止するには、使用可能な *adReason* 値ごとに *adstatus* パラメーターを **adStatusUnwantedEvent** に設定する必要があります。  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](./ado-events-model-example-vc.md)   
 [ADO イベントハンドラーの概要](../../guide/data/ado-event-handler-summary.md)   
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)