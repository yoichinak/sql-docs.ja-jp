---
description: InfoMessage イベント (ADO)
title: InfoMessage イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
author: rothja
ms.author: jroth
ms.openlocfilehash: 8695dc364a649dff204fcd689ab4722f19e125b9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990803"
---
# <a name="infomessage-event-ado"></a>InfoMessage イベント (ADO)
**Connectionevent**操作中に警告が発生するたびに、 **infomessage**イベントが呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *pError*  
 [エラー](./error-object.md)オブジェクトです。 このパラメーターには、返されたすべてのエラーが含まれます。 複数のエラーが返された場合は、 **エラー** コレクションを列挙して検出します。  
  
 *adStatus*  
 [Eventstatusenum](./eventstatusenum.md)状態の値です。 警告が発生した場合、 *adstatus* は **adstatusok** に設定 *され、* エラーメッセージには警告が含まれます。  
  
 このイベントが返される前に、このパラメーターを **adStatusUnwantedEvent** に設定して、後続の通知が行われないようにします。  
  
 *pConnection*  
 [接続](./connection-object-ado.md)オブジェクトです。 警告が発生した接続。 たとえば、接続オブジェクトを開いたり、**接続**で[コマンド](./command-object-ado.md)を**実行したり**すると、警告が発生することがあります。  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](./ado-events-model-example-vc.md)   
 [ADO イベントハンドラーの概要](../../guide/data/ado-event-handler-summary.md)   
 [Connection オブジェクト (ADO)](./connection-object-ado.md)