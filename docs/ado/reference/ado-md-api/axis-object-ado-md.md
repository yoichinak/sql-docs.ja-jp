---
description: Axis オブジェクト (ADO MD)
title: Axis オブジェクト (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Axis
helpviewer_keywords:
- Axis object [ADO MD]
ms.assetid: 5f498c9a-b1e7-4e6e-9ae6-71eadaf9aada
author: rothja
ms.author: jroth
ms.openlocfilehash: 6206ee753e42853dc0f209cb80fb9571806f68d6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987393"
---
# <a name="axis-object-ado-md"></a>Axis オブジェクト (ADO MD)
1つ以上のディメンションの選択されたメンバーを含むセルセットの位置指定軸またはフィルター軸を表します。  
  
## <a name="remarks"></a>解説  
 **軸**オブジェクトは、[軸](./axes-collection-ado-md.md)コレクションに含めることも、[セルセット](./cellset-object-ado-md.md)の[filteraxis](./filteraxis-property-ado-md.md)プロパティによって返すこともできます。  
  
 **軸**オブジェクトのコレクションとプロパティを使用して、次の操作を実行できます。  
  
-   [Name](./name-property-ado-md.md)プロパティを使用して、**軸**を識別します。  
  
-   位置のコレクションを使用し[て、](./positions-collection-ado-md.md) **軸**に沿って各位置を反復処理します。  
  
-   [Dimensioncount](./dimensioncount-property-ado-md.md)プロパティを使用して、**軸**上のディメンションの数を取得します。  
  
-   標準の ADO[プロパティ](../ado-api/properties-collection-ado.md)コレクションを使用して、**軸**のプロバイダー固有の属性を取得します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [プロパティ、メソッド、およびイベント](./axis-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Axis の例 (VBScript)](./axis-example-vbscript.md)   
 [Axes コレクション (ADO MD)](./axes-collection-ado-md.md)   
 [位置コレクション (ADO MD)](./positions-collection-ado-md.md)   
 [Properties コレクション (ADO)](../ado-api/properties-collection-ado.md)