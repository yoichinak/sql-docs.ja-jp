---
description: BeginTransComplete、CommitTransComplete、および RollbackTransComplete イベント (ADO)
title: BeginTrans、CommitTrans、RollbackTrans イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CommitTransComplete
- Connection::BeginTransComplete
- Connection::RollbackTransComplete
- Connection::CommitTransComplete
- RollbackTransComplete
- BeginTransComplete
helpviewer_keywords:
- CommitTransComplete event [ADO]
- RollbackTransComplete event [ADO]
- BeginTransComplete event [ADO]
ms.assetid: ec4e4b38-e9c6-4757-b2ef-4e468ae5f1d8
author: rothja
ms.author: jroth
ms.openlocfilehash: 91f5d573d62ef5000cdd6ed85a52866a0ee7f544
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975873"
---
# <a name="begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado"></a>BeginTransComplete、CommitTransComplete、および RollbackTransComplete イベント (ADO)
これらのイベントは、 [接続](./connection-object-ado.md) オブジェクトの関連付けられた操作の実行が終了した後に呼び出されます。  
  
-   **Begintranscomplete** は、 [BeginTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 操作の後に呼び出されます。  
  
-   **Committranscomplete** は、 [CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 操作の後に呼び出されます。  
  
-   **RollbackTransComplete** は、 [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) 操作の後に呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
BeginTransComplete TransactionLevel, pError, adStatus, pConnection  
CommitTransComplete pError, adStatus, pConnection  
RollbackTransComplete pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *TransactionLevel*  
 このイベントの原因となった**BeginTrans**の新しいトランザクションレベルを含む**Long**値。  
  
 *pError*  
 [エラー](./error-object.md)オブジェクトです。 EventStatusEnum の値が **Adstatuserrorerrorcode Curred**; の場合に発生したエラーについて説明します。それ以外の場合は設定されません。  
  
 *adStatus*  
 [Eventstatusenum](./eventstatusenum.md)状態の値です。 これらのイベントのいずれかが呼び出されると、このパラメーターは、イベントの原因となった操作が成功した場合は **Adstatusok** に、操作が失敗した場合は **Adstatuserrorの curred** に設定されます。  
  
 これらのイベントは、イベントが返される前に、このパラメーターを **adStatusUnwantedEvent** に設定することにより、後続の通知を防ぐことができます。  
  
 *pConnection*  
 このイベントが発生した **接続** オブジェクト。  
  
## <a name="remarks"></a>解説  
 Visual C++ では、複数の **接続** で同じイベント処理方法を共有できます。 メソッドは、返された **接続** オブジェクトを使用して、イベントの原因となったオブジェクトを特定します。  
  
 [Attributes](./attributes-property-ado.md)プロパティが**AdXactCommitRetaining**または**Adxactabortretaining 保持**するように設定されている場合、トランザクションをコミットまたはロールバックした後に新しいトランザクションが開始されます。 **Begintranscomplete**イベントを使用すると、最初のトランザクション開始イベント以外はすべて無視されます。  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](./ado-events-model-example-vc.md)   
 [BeginTrans、CommitTrans、および RollbackTrans メソッドの例 (VB)](./begintrans-committrans-and-rollbacktrans-methods-example-vb.md)   
 [ADO イベントハンドラーの概要](../../guide/data/ado-event-handler-summary.md)   
 [BeginTrans、CommitTrans、および RollbackTrans メソッド (ADO)](./begintrans-committrans-and-rollbacktrans-methods-ado.md)