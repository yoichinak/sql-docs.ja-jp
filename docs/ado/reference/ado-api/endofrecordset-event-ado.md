---
description: EndOfRecordset イベント (ADO)
title: EndOfRecordset イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c0bd91666040a87d104ff4a9c0036596b711a51
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973799"
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset イベント (ADO)
**Endofrecordset**イベントは、[レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)の末尾を越えて行を移動しようとしたときに呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *その他のデータ*  
 **VARIANT_BOOL**値。 VARIANT_TRUE に設定した場合、**レコードセット**に追加された行が多いことを示します。  
  
 *adStatus*  
 [Eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md)状態の値です。  
  
 **Endofrecordset**が呼び出されると、このパラメーターは、イベントの原因となった操作が成功した場合に**adstatusok**に設定されます。 このイベントの原因となった操作のキャンセルをこのイベントが要求できない場合は、 **Adstatuscantdeny** に設定されます。  
  
 **Endofrecordset**が返される前に、このパラメーターを**adStatusUnwantedEvent**に設定して、後続の通知が行われないようにします。  
  
 *pRecordset*  
 **レコードセット**オブジェクトです。 このイベントが発生した **レコードセット** 。  
  
## <a name="remarks"></a>解説  
 MoveNext **レコードセット** イベントは、 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 操作が失敗した場合に発生する可能性があります。  
  
 このイベントハンドラーは、おそらく**MoveNext**を呼び出した結果として、**レコードセット**オブジェクトの末尾を越えて移動しようとしたときに呼び出されます。 ただし、このイベントでは、データベースからより多くのレコードを取得し、レコード **セット**の末尾に追加することができます。 その場合は、 *Ffar データ* を VARIANT_TRUE に設定し、 **endofrecordset**からを返します。 次に、再度 **MoveNext** を呼び出して、新しく取得したレコードにアクセスします。  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
