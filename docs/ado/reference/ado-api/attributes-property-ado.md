---
description: Attributes プロパティ (ADO)
title: Attributes プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
author: rothja
ms.author: jroth
ms.openlocfilehash: ceb141b0ecdbc278e324f19f3bd4b3d7ed1b4eb6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975943"
---
# <a name="attributes-property-ado"></a>Attributes プロパティ (ADO)
オブジェクトの1つまたは複数の特性を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **Long 型**の値を設定または返します。  
  
 [接続](./connection-object-ado.md)オブジェクトの場合、 **Attributes**プロパティは読み取り/書き込み可能であり、その値は1つ以上の[XactAttributeEnum](./xactattributeenum.md)値の合計になります。 既定値は 0 です。  
  
 [Parameter](./parameter-object.md)オブジェクトの場合、 **Attributes**プロパティは読み取り/書き込み可能であり、その値は1つ以上の[parameterattributes 列挙](./parameterattributesenum.md)値の合計になります。 既定値は **Adparamsigned**です。  
  
 [Field](./field-object.md)オブジェクトの場合、 **Attributes**プロパティには1つ以上の[FieldAttributeEnum](./fieldattributeenum.md)値の合計を指定できます。 通常は読み取り専用です。 ただし、[レコード](./record-object-ado.md)の[フィールド](./fields-collection-ado.md)コレクションに追加された新しい**フィールド**オブジェクトの場合、**属性**は、**フィールド**の[Value](./value-property-ado.md)プロパティが指定されていて、**フィールドコレクションの** [Update](./update-method.md)メソッドを呼び出すことによって新しい**フィールド**が正常にデータプロバイダーによって追加された後にのみ、読み取り/書き込みになります。  
  
 [プロパティ](./property-object-ado.md)オブジェクトの場合、 **Attributes**プロパティは読み取り専用であり、その値は1つ以上の[propertyattributes 列挙](./propertyattributesenum.md)値の合計になります。  
  
## <a name="remarks"></a>解説  
 **接続**オブジェクト、**パラメーター**オブジェクト、**フィールド**オブジェクト、または**プロパティ**オブジェクトの特性を設定または取得するには、 **Attributes**プロパティを使用します。  
  
 複数の属性を設定すると、適切な定数を合計することができます。 互換性のない定数を含む合計にプロパティ値を設定すると、エラーが発生します。  
  
> [!NOTE]
>  **リモートデータサービスの使用状況** このプロパティは、クライアント側の **接続** オブジェクトでは使用できません。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Connection オブジェクト (ADO)](./connection-object-ado.md)  
        [Field オブジェクト](./field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter オブジェクト](./parameter-object.md)  
        [Property オブジェクト (ADO)](./property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [Attributes と Name プロパティの例 (VB)](./attributes-and-name-properties-example-vb.md)   
 [Attributes と Name プロパティの例 (VC + +)](./attributes-and-name-properties-example-vc.md)   
 [AppendChunk メソッド (ADO)](./appendchunk-method-ado.md)   
 [BeginTrans、CommitTrans、および RollbackTrans メソッド (ADO)](./begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [GetChunk メソッド (ADO)](./getchunk-method-ado.md)