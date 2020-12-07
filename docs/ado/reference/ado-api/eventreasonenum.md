---
description: EventReasonEnum
title: Event理由 Enum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventReasonEnum
helpviewer_keywords:
- EventReasonEnum enumeration [ADO]
ms.assetid: 7d4a5496-ec2d-4936-b36a-7049a82be4b4
author: rothja
ms.author: jroth
ms.openlocfilehash: b676ee2b8585f2bab467cc9f09580721d06fab0c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973573"
---
# <a name="eventreasonenum"></a>EventReasonEnum
イベントの発生原因となった理由を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adRsnAddNew**|1|操作によって新しいレコードが追加されました。|  
|**adRsnClose**|9|操作が **レコードセット**を閉じました。|  
|**adRsnDelete**|2|操作によってレコードが削除されました。|  
|**adRsnFirstChange**|11|レコードに対する最初の変更を行った操作。|  
|**adRsnMove**|10|操作によってレコード **セット**内のレコードポインターが移動されました。|  
|**adRsnMoveFirst**|12|操作は、レコードポインターをレコード **セット**内の最初のレコードに移動しました。|  
|**adRsnMoveLast**|15|操作はレコードポインターをレコード **セット**内の最後のレコードに移動しました。|  
|**adRsnMoveNext**|13|操作は、レコードポインターをレコード **セット**内の次のレコードに移動しました。|  
|**adRsnMovePrevious**|14|操作はレコードポインターをレコード **セット**内の前のレコードに移動しました。|  
|**adRsnRequery**|7|操作は、 [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)を再度実行します。|  
|**adRsnResynch 同期**|8|操作は、データベースを使用して **レコードセット** を再同期します。|  
|**adRsnUndoAddNew**|5|操作によって、新しいレコードの追加が取り消されました。|  
|**adRsnUndoDelete**|6|操作により、レコードの削除が取り消されました。|  
|**adRsnUndoUpdate**|4|操作により、レコードの更新が取り消されました。|  
|**adRsnUpdate**|3|操作により、既存のレコードが更新されました。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums. ADDNEW|  
|AdoEnums を終了します。|  
|AdoEnums を削除します。|  
|AdoEnums の変更|  
|AdoEnums。移動|  
|AdoEnums. MOVEFIRST|  
|AdoEnums. MOVELAST|  
|AdoEnums. MOVENEXT|  
|AdoEnums. MOVEPREVIOUS|  
|AdoEnums。 REQUERY|  
|AdoEnums の再同期|  
|AdoEnums. UNDOADDNEW|  
|AdoEnums. UNDODELETE|  
|AdoEnums. UNDOUPDATE|  
|AdoEnums を更新します。|  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [WillChangeRecord および RecordChangeComplete イベント (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)  

        [WillChangeRecordset および RecordsetChangeComplete イベント (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)  
    :::column-end:::
    :::column:::
        [WillMove および MoveComplete イベント (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)  
    :::column-end:::
:::row-end:::
