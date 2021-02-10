---
description: LockTypeEnum
title: LockTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
author: rothja
ms.author: jroth
ms.openlocfilehash: b141a5cd21e73208772c617ddb6e8c0a7e0d5a85
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100041813"
---
# <a name="locktypeenum"></a>LockTypeEnum
編集中にレコードに適用されるロックの種類を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|オプティミスティックバッチ更新を示します。 バッチ更新モードでは必須です。|  
|**adLockOptimistic**|3|オプティミスティックロック、レコードごとのレコードを示します。 プロバイダーはオプティミスティックロックを使用し、 [Update](./update-method.md) メソッドを呼び出したときにのみレコードをロックします。|  
|**adLockPessimistic**|2|ペシミスティックロック、レコードごとのレコードを示します。 プロバイダーは、レコードを正常に編集するために必要な処理を実行します。通常は、編集後すぐにデータソースのレコードをロックします。|  
|**adLockReadOnly**|1|読み取り専用レコードを示します。 データを変更することはできません。|  
|**adLockUnspecified**|-1|はロックの種類を指定していません。 複製の場合、複製は元と同じロックの種類で作成されます。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Clone メソッド (ADO)](./clone-method-ado.md)  
        [LockType プロパティ (ADO)](./locktype-property-ado.md)  
    :::column-end:::
    :::column:::
        [Open メソッド (ADO Recordset)](./open-method-ado-recordset.md)  
        [WillExecute イベント (ADO)](./willexecute-event-ado.md)  
    :::column-end:::
:::row-end:::