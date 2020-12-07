---
description: AllMembers (MDX)
title: AllMembers (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba70d4ad8b301cbd8af2fd76ce058f2dab2e4a4c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461674"
---
# <a name="allmembers-mdx"></a>AllMembers (MDX)


  階層またはレベル式のいずれかを評価し、階層またはレベルのすべての計算されるメンバーを含む、指定した階層またはレベルのすべてのメンバーを含むセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.AllMembers  
  
Level syntax  
Level_Expression.AllMembers  
```  
  
## <a name="arguments"></a>引数  
 *Hierarchy_Expression*  
 階層を返す有効な多次元式 (MDX) 式です。  
  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **Allmembers**関数は、指定された階層またはレベルで、計算されるメンバーを含むすべてのメンバーを含むセットを返します。 **Allmembers**関数は、指定された階層またはレベルに表示可能なメンバーが含まれていない場合でも、計算されるメンバーを返します。  
  
> [!IMPORTANT]  
>  ディメンションに含まれる階層が1つだけの場合、階層は、ディメンション名または階層名で参照できます。この場合、ディメンション名は、表示されている唯一の階層に解決されるためです。 たとえば、 `Measures.AllMembers` は、Measures ディメンション内の唯一の階層に解決されるため、有効な MDX 式です。  
  
> [!NOTE]  
>  **Allmembers**関数は、 [add演算メンバー (MDX)](../mdx/addcalculatedmembers-mdx.md)関数と意味が似ています。  
  
## <a name="examples"></a>例  
 次の例では、列軸の [属性階層のすべてのメンバーを返し `Date].[Calendar Year]` ます。これには、計算されるメンバーと、 `[Product].[Model Name]` **Adventure works** キューブの行軸にある属性階層のすべての子のセットが含まれます。  
  
```  
SELECT  
   [Date].[Calendar Year].AllMembers ON COLUMNS,  
   [Product].[Model Name].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
 次の例では、列軸上の **Measures** ディメンションのすべてのメンバーを返します。これには、すべての計算されるメンバーと、 `[Product].[Model Name]` **Adventure works** キューブの行軸にある属性階層のすべての子のセットが含まれます。  
  
```  
SELECT  
    Measures.AllMembers ON COLUMNS,  
    [Product].[Model Name].Children ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX&#41;&#40;の Add演算メンバー ](../mdx/addcalculatedmembers-mdx.md)   
 [子 &#40;MDX&#41;](../mdx/children-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
