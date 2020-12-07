---
description: Name プロパティ (ADO MD)
title: Name プロパティ (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level::Name
- CubeDef::Name
- Member::Name
- Catalog::Name
- Dimension::Name
- Name
- Axis::Name
- Hierarchy::Name
helpviewer_keywords:
- Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
author: rothja
ms.author: jroth
ms.openlocfilehash: 4dfec86bb631dda661b957e02667cd320c20fec6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986243"
---
# <a name="name-property-ado-md"></a>Name プロパティ (ADO MD)
オブジェクトの名前を示します。  
  
## <a name="return-values"></a>戻り値  
 は **文字列** を返し、読み取り専用です。  
  
## <a name="remarks"></a>解説  
 オブジェクトの **name** プロパティは、序数参照によって取得できます。その後、オブジェクトを名前で直接参照できます。 たとえば、に `cdf.CubeDefs(0).Name` よって "Bobs ビデオストア" が生成された場合、この [CubeDef](./cubedef-object-ado-md.md) をと呼び出すことができ `cdf.CubeDefs("Bobs Video Store")` ます。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Axis オブジェクト (ADO MD)](./axis-object-ado-md.md)  
        [Catalog オブジェクト (ADO MD)](./catalog-object-ado-md.md)  
        [CubeDef オブジェクト (ADO MD)](./cubedef-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Dimension オブジェクト (ADO MD)](./dimension-object-ado-md.md)  
        [Hierarchy オブジェクト (ADO MD)](./hierarchy-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Level オブジェクト (ADO MD)](./level-object-ado-md.md)  
        [Member オブジェクト (ADO MD)](./member-object-ado-md.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [カタログの例 (VB)](./catalog-example-vb.md)   
 [Caption プロパティ (ADO MD)](./caption-property-ado-md.md)   
 [Description プロパティ (ADO MD)](./description-property-ado-md.md)   
 [UniqueName プロパティ (ADO MD)](./uniquename-property-ado-md.md)