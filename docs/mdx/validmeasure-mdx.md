---
description: ValidMeasure (MDX)
title: ValidMeasure (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cd2bc2385a3445076636fb1b4001120463d1cd89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494834"
---
# <a name="validmeasure-mdx"></a>ValidMeasure (MDX)


  キューブ内のメジャーの値を返します。指定した組の結果を返すときに、適用されていないディメンション (集計可能でない場合は既定のメンバー) を強制的に適用します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ValidMeasure(Tuple_Expression)   
```  
  
## <a name="arguments"></a>引数  
 *Tuple_Expression*  
 組を返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **Validmeasure**関数は、組の値を返します。タプルが返す値を持つメジャーグループとのリレーションシップを持たない属性は無視されます。 属性にメジャーとの間のリレーションシップが存在しない理由は 2 つ考えられます。  
  
-   属性のディメンションに、タプル内のメジャーのメジャーグループとのリレーションシップがありません。  
  
-   属性のディメンションには、メジャーのメジャーグループとのリレーションシップがありませんが、粒度属性はキー属性ではなく、粒度属性には組の属性との直接的な関係がありません。  
  
 この関数によって指定される動作は、既定のサーバー側の動作であり、メジャーグループオブジェクトの **Ignoreun関連性ディメンション** プロパティによって制御されます。  
  
 指定された組の各属性に粒度が指定されている場合 (つまり、組のメンバーが All メンバーでない場合)、各属性の現在の座標は次のように移動されます。  
  
-   指定された属性メンバーに関連する属性は、現在のメンバーと共に存在するメンバーに移動されます。  
  
-   指定された属性メンバーに関連する属性は、All メンバー (階層が集計可能でない場合は既定のメンバー) に移動されます。  
  
-   関連しない属性は、(メジャーに基づいて) All メンバーに移動されます。  
  
## <a name="example"></a>例  
 次のクエリは、ValidMeasure 関数を使用して、Ignoreun関連性のある Dimensions プロパティの動作をオーバーライドする方法を示しています。 Adventure Works キューブでは、Sales Targets メジャーグループは Ignoreun関連性のあるディメンションを False に設定しています。Date ディメンションは Calendar Quarter の粒度でこのメジャーグループに結合されるので、Sales Quota メジャーは既定では、Calendar Quarter の下に null を返します (ただし、MDX スクリプトには、月レベルに値を割り当てる計算もあります)。 計算されるメジャーで ValidMeasure 関数を使用すると、Sales Quota メジャーは IgnoreUnrelatedDimensions が True に設定されている場合と同じように動作し、Sales Quota が現在の Calendar Quarter の値を表示するように強制できます。  
  
```  
WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])  
SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,  
[Date].[Calendar].MEMBERS ON 1  
FROM [Adventure Works]  
```  
  
 同様に、Sales Targets メジャーグループには、プロモーションディメンションとのリレーションシップはまったくありません。そのため、昇格時に階層の All メンバーの下に null が返されます。 ここでも、この動作は、ValidMeasure を使用して変更できます。  
  
 `WITH MEMBER MEASURES.VTEST AS VALIDMEASURE([Measures].[Sales Amount Quota])`  
  
 `SELECT {[Measures].[Sales Amount Quota], MEASURES.VTEST} ON 0,`  
  
 `[Promotion].[Promotions].members ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
