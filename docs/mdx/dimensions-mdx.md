---
description: Dimensions (MDX)
title: ディメンション (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c98167516f9e01525ecd351389c885c48626636e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491419"
---
# <a name="dimensions-mdx"></a>Dimensions (MDX)


  数値または文字列式で指定された階層を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Numeric expression syntax  
Dimensions(Hierarchy_Number)  
  
String expression syntax  
Dimensions(Hierarchy_Name)  
```  
  
## <a name="arguments"></a>引数  
 *Hierarchy_Number*  
 階層番号を指定する有効な数値式です。  
  
 *Hierarchy_Name*  
 階層名を指定する有効な文字列式です。  
  
## <a name="remarks"></a>解説  
 階層番号が指定されている場合、 **Dimensions** 関数は、キューブ内の0から始まる位置が指定された階層番号を持つ階層を返します。  
  
 階層名が指定されている場合、 **Dimensions** 関数は、指定された階層を返します。 通常、この文字列バージョンの **Dimensions** 関数は、ユーザー定義関数と共に使用します。  
  
> [!NOTE]  
>  **Measures**ディメンションは、常にによって表され `Dimensions(0)` ます。  
  
## <a name="examples"></a>例  
 次の例では、 **Dimensions** 関数を使用して、数値式と文字列式の両方を使用して、指定した階層の名前、レベル数、およびメンバー数を返します。  
  
```  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Levels.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions  
   ('[Product].[Product Model Lines]').Members.Count  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Name  
SELECT Measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
  
WITH MEMBER Measures.x AS Dimensions(0).Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
