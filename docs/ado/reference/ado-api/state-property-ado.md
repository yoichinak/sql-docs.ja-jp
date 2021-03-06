---
description: State プロパティ (ADO)
title: State プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
author: rothja
ms.author: jroth
ms.openlocfilehash: 7357d21aa58bca15e1fbbeb3c9cec542ef40ce8b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100051323"
---
# <a name="state-property-ado"></a>State プロパティ (ADO)
オブジェクトの状態が開いているか閉じられているかにかかわらず、適用可能なすべてのオブジェクトを示します。 オブジェクトが非同期メソッドを実行している場合は、オブジェクトの現在の状態が接続中、実行中、または取得中かどうかを示します。  
  
## <a name="return-value"></a>戻り値  
 [ObjectStateEnum](./objectstateenum.md)値を指定できる **Long 型** の値を返します。 既定値は **adStateClosed** です。  
  
## <a name="remarks"></a>解説  
 **State** プロパティを使用して、特定のオブジェクトの現在の状態をいつでも確認できます。  
  
 オブジェクトの **State** プロパティは、値の組み合わせを持つことができます。 たとえば、ステートメントが実行されている場合、このプロパティには **Adstateopen** と **adstateopen** の合計値が設定されます。  
  
 **State** プロパティは読み取り専用です。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Command オブジェクト (ADO)](./command-object-ado.md)  
        [Connection オブジェクト (ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Record オブジェクト (ADO)](./record-object-ado.md)  
        [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [Stream オブジェクト (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [ConnectionString、ConnectionTimeout、State プロパティの例 (VB)](./connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、ConnectionTimeout、State プロパティの例 (VC + +)](./connectionstring-connectiontimeout-and-state-properties-example-vc.md)