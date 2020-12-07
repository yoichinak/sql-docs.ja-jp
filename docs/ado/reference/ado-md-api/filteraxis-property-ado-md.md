---
description: FilterAxis プロパティ (ADO MD)
title: FilterAxis プロパティ (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset::FilterAxis
- FilterAxis
helpviewer_keywords:
- FilterAxis property [ADO MD]
ms.assetid: 9c656963-531e-4cd1-b698-d5f42a9b7ba3
author: rothja
ms.author: jroth
ms.openlocfilehash: 13ede9a2780a55d79e1b8c53868a409599510688
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986713"
---
# <a name="filteraxis-property-ado-md"></a>FilterAxis プロパティ (ADO MD)
現在の [セルセット](./cellset-object-ado-md.md)に関するフィルター情報を示します。  
  
## <a name="return-values"></a>戻り値  
 は [軸](./axis-object-ado-md.md) オブジェクトを返し、は読み取り専用です。  
  
## <a name="remarks"></a>解説  
 データのスライスに使用されたディメンションに関する情報を返すには、 **Filteraxis** プロパティを使用します。 **軸**の[dimensioncount](./dimensioncount-property-ado-md.md)プロパティは、スライサーディメンションの数を返します。 通常、この軸には1行しかありません。  
  
 **Filteraxis**によって返された**軸**は、[セルセット](./cellset-object-ado-md.md)オブジェクトの[Axes](./axes-collection-ado-md.md)コレクションに含まれていません。  
  
## <a name="applies-to"></a>適用対象  
 [CellSet オブジェクト (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [Axis オブジェクト (ADO MD)](./axis-object-ado-md.md)   
 [Dimension オブジェクト (ADO MD)](./dimension-object-ado-md.md)   
 [DimensionCount プロパティ (ADO MD)](./dimensioncount-property-ado-md.md)