---
description: Precision プロパティ (ADO)
title: Precision プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords:
- Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
author: rothja
ms.author: jroth
ms.openlocfilehash: e7a166077bd0237ff822193297d57dc364d17bef
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990053"
---
# <a name="precision-property-ado"></a>Precision プロパティ (ADO)
[パラメーター](./parameter-object.md)オブジェクトまたは数値[フィールド](./field-object.md)オブジェクトの数値の有効桁数を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 値を表すために使用される最大桁数を示す **バイト** 値を設定または返します。  
  
## <a name="remarks"></a>解説  
 数値**パラメーター**または**フィールド**オブジェクトの値を表すために使用される最大桁数を決定するには、 **Precision**プロパティを使用します。  
  
 値は、 **パラメーター** オブジェクトの読み取り/書き込みです。  
  
 **Field**オブジェクトの場合、通常、**有効桁数**は読み取り専用です。 ただし、[レコード](./record-object-ado.md)の[フィールド](./fields-collection-ado.md)コレクションに追加された新しい**フィールド**オブジェクトでは、**フィールド**の[Value](./value-property-ado.md)プロパティが指定され、データプロバイダーが**フィールド**コレクションの[Update](./update-method.md)メソッドを呼び出すことによって新しい**フィールド**を正常に追加した後にのみ、**有効桁数**が読み取り/書き込みになります。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Field オブジェクト](./field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter オブジェクト](./parameter-object.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [NumericScale および Precision プロパティの例 (VB)](./numericscale-and-precision-properties-example-vb.md)   
 [NumericScale および Precision プロパティの例 (VC + +)](./numericscale-and-precision-properties-example-vc.md)   
 [NumericScale プロパティ (ADO)](./numericscale-property-ado.md)