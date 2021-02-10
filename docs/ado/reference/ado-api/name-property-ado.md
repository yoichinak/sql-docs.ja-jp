---
description: Name プロパティ (ADO)
title: Name プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
author: rothja
ms.author: jroth
ms.openlocfilehash: 150951c91a58e966bbcd02e8a11a5a495026a129
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100041622"
---
# <a name="name-property-ado"></a>Name プロパティ (ADO)
オブジェクトの名前を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 オブジェクトの名前を示す **文字列** 値を設定または返します。  
  
## <a name="remarks"></a>解説  
 **Name プロパティを** 使用して、**コマンド**、**プロパティ**、**フィールド**、または **パラメーター** オブジェクトの名前を割り当てるか、名前を取得します。  
  
 この値は、 **Command** オブジェクトでは読み取り/書き込みが可能で、 **プロパティ** オブジェクトでは読み取り専用です。  
  
 **Field** オブジェクトの場合、通常、**名前** は読み取り専用です。 ただし、[レコード](./record-object-ado.md)の [フィールド](./fields-collection-ado.md)コレクションに追加された新しい **フィールド** オブジェクトの場合、 **Name** は、**フィールド** の [Value](./value-property-ado.md)プロパティが指定され、データプロバイダーが **フィールド** コレクションの [Update](./update-method.md)メソッドを呼び出すことによって新しい **フィールド** を正常に追加した後にのみ、読み取り/書き込みになります。  
  
 [Parameters](./parameters-collection-ado.md)コレクションにまだ追加されていない **パラメーター** オブジェクトの場合、 **Name** プロパティは読み取り/書き込み可能です。 追加された **パラメーター** オブジェクトおよびその他すべてのオブジェクトについては、 **Name** プロパティは読み取り専用です。 名前はコレクション内で一意である必要はありません。  
  
 オブジェクトの **name** プロパティは、序数参照によって取得できます。その後、オブジェクトを名前で直接参照できます。 たとえば、がを生成した場合、 `rstMain.Properties(20).Name` `Updatability` このプロパティをとして参照でき `rstMain.Properties("Updatability")` ます。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Command オブジェクト (ADO)](./command-object-ado.md)  
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