---
description: Description プロパティ (ADO MD)
title: Description プロパティ (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Description
- Level::Description
- CubeDef::Description
- Hierarchy::Description
- Description
- Dimension::Description
helpviewer_keywords:
- Description property [ADO MD]
ms.assetid: 6d626d35-0bf3-4f24-9934-ad9c9c91273a
author: rothja
ms.author: jroth
ms.openlocfilehash: 726a49da64c36b487868068affad65164b9b3c5e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986903"
---
# <a name="description-property-ado-md"></a>Description プロパティ (ADO MD)
現在のオブジェクトの説明テキストを返します。  
  
## <a name="return-values"></a>戻り値  
 は **文字列** を返し、読み取り専用です。  
  
## <a name="remarks"></a>解説  
 [メンバー](./member-object-ado-md.md)オブジェクトの場合、**説明**はメジャーおよび数式メンバーにのみ適用されます。 **説明** は、他のすべての種類のメンバーに対して空の文字列 ("") を返します。 さまざまな種類のメンバーの詳細については、「 [Type](./type-property-ado-md.md) プロパティ」を参照してください。  
  
 このプロパティは、[レベル](./level-object-ado-md.md)オブジェクトに属している**メンバー**オブジェクトでのみサポートされます。 このプロパティが、 [Position](./position-object-ado-md.md)オブジェクトに属する**メンバー**オブジェクトから参照されている場合に、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [CubeDef オブジェクト (ADO MD)](./cubedef-object-ado-md.md)  
        [Dimension オブジェクト (ADO MD)](./dimension-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Hierarchy オブジェクト (ADO MD)](./hierarchy-object-ado-md.md)  
        [Level オブジェクト (ADO MD)](./level-object-ado-md.md)  
    :::column-end:::
    :::column:::
        [Member オブジェクト (ADO MD)](./member-object-ado-md.md)  
    :::column-end:::
:::row-end:::