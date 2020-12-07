---
description: NumericScale プロパティ (ADO)
title: NumericScale プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
author: rothja
ms.author: jroth
ms.openlocfilehash: 120d88e82f77af622de962ac306442625487ff08
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990413"
---
# <a name="numericscale-property-ado"></a>NumericScale プロパティ (ADO)
[パラメーター](./parameter-object.md)または[フィールド](./field-object.md)オブジェクトの数値の小数点以下桁数を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 数値が解決される小数点以下の桁数を示す **バイト** 値を設定または返します。  
  
## <a name="remarks"></a>解説  
 数値**パラメーター**または**フィールド**オブジェクトの値を表すために使用される、小数点の右側の桁数を決定するには、 **numericscale**プロパティを使用します。  
  
 **パラメーター**オブジェクトの場合、 **numericscale**プロパティは読み取り/書き込み可能です。  
  
 **フィールド**オブジェクトの場合、 **numericscale**は通常読み取り専用です。 ただし、[レコード](./record-object-ado.md)の[フィールド](./fields-collection-ado.md)コレクションに追加された新しい**フィールド**オブジェクトの場合は、**フィールド**の[値](./value-property-ado.md)プロパティが指定され、データプロバイダーが[フィールド](./fields-collection-ado.md)コレクションの[Update](./update-method.md)メソッドを呼び出して新しい**フィールド**を正常に追加した後にのみ、 **numericscale**が読み取り/書き込みになります。  
  
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
 [Precision プロパティ (ADO)](./precision-property-ado.md)