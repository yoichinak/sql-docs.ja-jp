---
description: MDX データ操作 - DROP CELL CALCULATION
title: DROP CELL CALCULATION ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a407d6325168e2287fc6b815b3b45f0130dd1a4d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429804"
---
# <a name="mdx-data-definition---drop-cell-calculation"></a>MDX データ操作 - DROP CELL CALCULATION


  指定されたセルの計算を削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DROP [ SESSION ] CELL CALCULATION CURRENTCUBE | Cube_Name.CellCalc_Name  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブ式の名前を指定する有効な文字列式です。  
  
 *CellCalc_Name*  
 削除するセル計算の名前を指定する有効な文字列式です。  
  
## <a name="see-also"></a>参照  
 [CREATE CELL CALCULATION ステートメント &#40;MDX&#41;](../mdx/mdx-data-definition-create-cell-calculation.md)   
 [Mdx&#41;&#40;mdx データ定義ステートメント ](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
