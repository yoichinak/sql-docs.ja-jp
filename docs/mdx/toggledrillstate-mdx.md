---
description: ToggleDrillState (MDX)
title: ToggleDrillState (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: dd716e631adc3ded77f81278c20f754b28199b49
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192322"
---
# <a name="toggledrillstate-mdx"></a>ToggleDrillState (MDX)


  ドリルダウンモードと drillllup モード間でメンバーのドリル状態を切り替えます。  
  
## <a name="syntax"></a>構文  
  
```  
  
ToggleDrillState(Set_Expression1,Set_Expression2 [, [RECURSIVE] [,INCLUDE_CALC_MEMBERS] ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *繰り返し*  
 (省略可能)。 セットの再帰的な比較を示すキーワードです。 **ToggleDrillState**関数は、**ドリルスルーメンバー**関数と**ドリルダウンメンバー**関数を組み合わせたものです。 再帰は、メンバーが **ドリルダウンメンバー** の状態にある場合にのみ適用されます。  
  
 *Include_calc_members*  
 (省略可能)。 計算されるメンバーがドリルダウン レベルに存在する場合にそれらを含めるかどうかを示すフラグです。  
  
## <a name="remarks"></a>注釈  
 **ToggleDrillState**関数は、最初のセット内に存在する2番目のセットの各メンバーのドリル状態を切り替えます。 最初のセットには、任意の次元の組を含めることができますが、2番目のセットには1つの次元のメンバーが含まれている必要があります。 **ToggleDrillState**関数は、**ドリルスルーメンバー**関数と**ドリルダウンメンバー**関数を組み合わせたものです。 2番目のセットのメンバー *m*が1番目のセットに存在し、そのメンバーがドリルダウンされている (つまり、直下に子孫がある) 場合は、 `DrillupMember(Set_Expression1, {m})` 1 番目のセット内のメンバーまたは組にが適用されます。 その*m*メンバーがドリルアップされている場合 (つまり、m の直下に*m*の直後*にある子孫*が存在しない場合)、 `DrilldownMember(Set_Expression1, {m}[, RECURSIVE])` は1番目のセットに適用されます。  
  
 省略可能な **RECURSIVE** フラグが使用されている場合、ドリルアップとドリルダウンは再帰的に適用されます。 Recursive フラグの詳細については、「 [ドリルアップメンバー](../mdx/drillupmember-mdx.md) 関数と [ドリルダウンメンバー](../mdx/drilldownmember-mdx.md) 関数」を参照してください。  
  
 XMLA プロパティ MdpropMdxDrillFunctions に対してクエリを実行すると、ドリル機能に対してサーバーが提供するサポートのレベルを確認できます。詳細については、「 [サポートされる Xmla プロパティ &#40;xmla&#41;](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 」を参照してください。  
  
 この関数を含むシナリオと例について [は、「Database Journal: MDX Set Functions: ToggleDrillState () 関数](https://go.microsoft.com/fwlink/?LinkId=517759) 」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、1番目のセットのオーストラリアメンバーをドリルダウンし、1番目のセットの米国メンバーをドリルアップします。  
  
```  
SELECT ToggleDrillState  
   ({[Geography].[Geography].[Country].Members, [Geography].[Geography].[Country].&[United States].Children},  
      {[Geography].[Geography].[Country].[Australia]  
      , [Geography].[Geography].[Country].&[United States]}  
      --, recursive  
      --, include_calc_members  
   ) ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
