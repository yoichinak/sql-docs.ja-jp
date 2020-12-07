---
description: EventStatusEnum
title: EventStatusEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EventStatusEnum
helpviewer_keywords:
- EventStatusEnum enumeration [ADO]
ms.assetid: ebfd4cda-4017-4873-9d28-38b1c7db12a8
author: rothja
ms.author: jroth
ms.openlocfilehash: 853dd54afbb8753b05ce95f17b20aa600fea493c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973563"
---
# <a name="eventstatusenum"></a>EventStatusEnum
イベントの実行の現在の状態を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|イベントの発生原因となった操作のキャンセルを要求します。|  
|**adStatusCantDeny**|3|操作が保留中の操作の取り消しを要求できないことを示します。|  
|**Adstatuserrorの Curred**|2|イベントの原因となった操作がエラーまたはエラーのために失敗したことを示します。|  
|**adStatusOK**|1|イベントの原因となった操作が成功したことを示します。|  
|**adStatusUnwantedEvent**|5|イベントメソッドの実行が完了する前に、後続の通知を実行しないようにします。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums (キャンセル)|  
|AdoEnums. CANTDENY|  
|AdoEnums. ERRORの CURRED|  
|AdoEnums。 OK|  
|AdoEnums. UNWANTEDEVENT|  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [BeginTransComplete、CommitTransComplete、および RollbackTransComplete イベント (ADO)](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)  

        [ConnectComplete および Disconnect イベント (ADO)](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)  

        [EndOfRecordset イベント (ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)  

        [ExecuteComplete イベント (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)  
    :::column-end:::
    :::column:::
        [FetchComplete イベント (ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)  

        [InfoMessage イベント (ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)  

        [WillChangeField および FieldChangeComplete イベント (ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)  

        [WillChangeRecord および RecordChangeComplete イベント (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)  
    :::column-end:::
    :::column:::
        [WillChangeRecordset および RecordsetChangeComplete イベント (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)  

        [WillConnect イベント (ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)  

        [WillExecute イベント (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)  

        [WillMove および MoveComplete イベント (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)  
    :::column-end:::
:::row-end:::
