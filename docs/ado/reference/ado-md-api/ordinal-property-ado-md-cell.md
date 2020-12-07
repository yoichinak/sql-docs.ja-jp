---
description: Ordinal プロパティ (ADO MD セル)
title: Ordinal プロパティ (ADO MD Cell) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: a6001168-b954-47f0-ba0d-c05c4cc40c58
author: rothja
ms.author: jroth
ms.openlocfilehash: b4d14b2cdfc61fd76221a2071f15593807b5f1ba
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986223"
---
# <a name="ordinal-property-ado-md-cell"></a>Ordinal プロパティ (ADO MD セル)
セルセット内の位置によって [セル](./cell-object-ado-md.md) を一意に識別します。  
  
## <a name="return-values"></a>戻り値  
 **長**整数を返し、読み取り専用です。  
  
## <a name="remarks"></a>解説  
 セルの序数値は、セルセット内のセルを一意に識別します。 概念的には、セルセット内のセルには、セルセットが *p*次元配列であるかのように番号が付けられます。ここで、 *p* は [軸](./axes-collection-ado-md.md)の数です。 セルは、行優先順で0から始まる番号が付けられます。 セルの序数を計算するための式を次に示します。  
  
 セルの序数値を[Cellset](./cellset-object-ado-md.md)オブジェクトの[Item](./item-property-ado-md-cellset.md)プロパティと共に使用して、[セル](./cell-object-ado-md.md)をすばやく取得できます。  
  
## <a name="applies-to"></a>適用対象  
 [Cell オブジェクト (ADO MD)](./cell-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [Axis の例 (VBScript)](./axis-example-vbscript.md)   
 [Cellset オブジェクト (ADO MD)](./cellset-object-ado-md.md)   
 [Item プロパティ (ADO MD セルセット)](./item-property-ado-md-cellset.md)   
 [Ordinal プロパティ (ADO MD 位置)](./ordinal-property-ado-md-position.md)