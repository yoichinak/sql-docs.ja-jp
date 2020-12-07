---
description: FetchComplete イベント (ADO)
title: FetchComplete イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- FetchComplete event [ADO]
ms.assetid: a28d3858-566c-468d-b070-d1de4339fbea
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ef8df9f6d4ea113d5cca9ad9ffba9c4888776d8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973353"
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete イベント (ADO)
**Fetchcomplete**イベントは、長い非同期操作内のすべてのレコードが[レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)に取得された後に呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>パラメーター  
 *pError*  
 [エラー](../../../ado/reference/ado-api/error-object.md)オブジェクトです。 **Adstatus**の値が**adstatuserrorて**いる場合に発生したエラーについて説明します。それ以外の場合は設定されません。  
  
 *adStatus*  
 [Eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md)状態の値です。 このイベントが呼び出されると、このパラメーターは、イベントの原因となった操作が成功した場合は **Adstatusok** に、操作が失敗した場合は **Adstatuserrorの curred** に設定されます。  
  
 このイベントが返される前に、このパラメーターを **adStatusUnwantedEvent** に設定して、後続の通知が行われないようにします。  
  
 *pRecordset*  
 **レコードセット**オブジェクトです。 レコードを取得したオブジェクト。  
  
## <a name="remarks"></a>解説  
 Microsoft Visual Basic で **Fetchcomplete** を使用するには Visual Basic 6.0 以降が必要です。  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
