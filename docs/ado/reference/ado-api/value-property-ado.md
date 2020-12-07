---
description: Value プロパティ (ADO)
title: Value プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
author: rothja
ms.author: jroth
ms.openlocfilehash: bc7ea2b5f571429d05b8201d8e23dc594bb896e8
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987993"
---
# <a name="value-property-ado"></a>Value プロパティ (ADO)

[フィールド](./field-object.md)、[パラメーター](./parameter-object.md)、または[プロパティ](./property-object-ado.md)オブジェクトに割り当てられた値を示します。
  
## <a name="settings-and-return-values"></a>設定と戻り値

オブジェクトの値を示す **バリアント** 値を設定または返します。 既定値は [Type](./type-property-ado.md) プロパティによって異なります。
  
## <a name="remarks"></a>解説

**Value**プロパティを使用して、**フィールド**オブジェクトのデータを設定または取得します。また、**パラメーターオブジェクトを**使用してパラメーター値を設定または取得するか、プロパティオブジェクトを使用し**てプロパティ設定**を設定または取得します。 **値**プロパティが読み取り/書き込みか、読み取り専用かは、さまざまな要因によって決まります。 詳細については、各オブジェクトのトピックを参照してください。

ADO では、 **Value** プロパティを使用して長いバイナリデータを設定し、返すことができます。
  
> [!NOTE]
> **パラメーター**オブジェクトの場合、ADO は、プロバイダーから**値**プロパティを1回だけ読み取ります。 **値**プロパティが空である**パラメーター**がコマンドに含まれていて、コマンドから[レコードセット](./recordset-object-ado.md)を作成する場合は、まず、**値**プロパティを取得する前に**レコードセット**を閉じてください。 それ以外の場合、一部のプロバイダーでは、 **value** プロパティが空で、適切な値が含まれません。
> 
> [レコード](./record-object-ado.md)オブジェクトの[Fields](./fields-collection-ado.md)コレクションに追加された新しい**Field**オブジェクトの場合は、他の**フィールド**プロパティを指定する前に、 **Value**プロパティを設定する必要があります。 最初に、**値**プロパティの特定の値が割り当てられており、という**フィールド**コレクションで[更新](./update-method.md)されている必要があります。 その後、 [型](./type-property-ado.md) や [属性](./attributes-property-ado.md) などの他のプロパティにアクセスできます。
  
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

[Value プロパティの例 (VB)](./value-property-example-vb.md) 
[Value プロパティの例 (VC + +)](./value-property-example-vc.md)