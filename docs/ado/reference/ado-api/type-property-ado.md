---
description: Type プロパティ (ADO)
title: Type プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords:
- Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
author: rothja
ms.author: jroth
ms.openlocfilehash: 9f4dcfd3c22363ab4950e03844647f990a34f4d5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988313"
---
# <a name="type-property-ado"></a>Type プロパティ (ADO)
[パラメーター](./parameter-object.md)、[フィールド](./field-object.md)、または[プロパティ](./property-object-ado.md)オブジェクトの操作の種類またはデータ型を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 [DataTypeEnum](./datatypeenum.md)値を設定または返します。  
  
## <a name="remarks"></a>解説  
 **Parameter**オブジェクトの場合、 **Type**プロパティは読み取り/書き込み可能です。 [レコード](./record-object-ado.md)の[フィールド](./fields-collection-ado.md)コレクションに追加された新しい**フィールド**オブジェクトの場合は、**フィールド**の [[値](./value-property-ado.md)] プロパティが指定され、データプロバイダーが**フィールド**コレクションの[Update](./update-method.md)メソッドを呼び出して新しい**フィールド**を正常に追加した後にのみ、「読み取り/書き込み専用」と**入力**します。  
  
 他のすべてのオブジェクトについては、 **Type** プロパティは読み取り専用です。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Field オブジェクト](./field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter オブジェクト](./parameter-object.md)  
    :::column-end:::
    :::column:::
        [Property オブジェクト (ADO)](./property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [Type プロパティの例 (Field) (VB)](./type-property-example-field-vb.md)   
 [Type プロパティの例 (プロパティ) (VC + +)](./type-property-example-property-vc.md)   
 [RecordType プロパティ (ADO)](./recordtype-property-ado.md)   
 [Type プロパティ (ADO Stream)](./type-property-ado-stream.md)