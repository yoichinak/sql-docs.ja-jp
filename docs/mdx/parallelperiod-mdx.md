---
description: ParallelPeriod (MDX)
title: ParallelPeriod (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4c8a6c91bae50ca06be46926f34de172e424e613
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471724"
---
# <a name="parallelperiod-mdx"></a>ParallelPeriod (MDX)


  指定されたメンバーと同じ相対位置で、前の期間のメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ParallelPeriod( [ Level_Expression [ ,Index [ , Member_Expression ] ] ] )  
```  
  
## <a name="arguments"></a>引数  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式です。  
  
 *Index*  
 遅延する並列期間の数を指定する有効な数値式です。  
  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 [いとこ](../mdx/cousin-mdx.md)関数と同様に、 **parallelperiod**関数は時系列に密接に関連しています。 **Parallelperiod**関数は、指定されたレベルで指定されたメンバーの先祖を受け取り、指定されたラグを持つ先祖の兄弟を検索し、最後に、指定されたメンバーの、兄弟の子孫間での並列期間を返します。  
  
 **Parallelperiod**関数には、次の既定値があります。  
  
-   レベル式もメンバー式も指定されていない場合、既定のメンバー値は、メジャーグループ内の *Time* 型を持つ最初のディメンションの最初の階層の現在のメンバーになります。  
  
-   レベル式が指定されていても、メンバー式が指定されていない場合、既定のメンバー値は *Level_Expression*になります。**Hierarchy. CurrentMember**。  
  
-   既定のインデックス値は1です。  
  
-   既定のレベルは、指定されたメンバーの親のレベルです。  
  
 **Parallelperiod**関数は、次の MDX ステートメントと同じです。  
  
 `Cousin(Member_Expression, Ancestor(Member_Expression, Level_Expression) .Lag(Numeric_Expression))`  
  
## <a name="example"></a>例  
 次の例では、Quarter レベルを基準として、2003 年 10 月から 3 期間さかのぼった並列期間を返します。つまり、2003 年 1 月が返されます。  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Quarter]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 次の例では、Semester  レベルを基準として、2003 年 10 月から 3 期間さかのぼった並列期間を返します。つまり、2002 年 4 月が返されます。  
  
```  
SELECT ParallelPeriod ([Date].[Calendar].[Calendar Semester]  
   , 3  
   , [Date].[Calendar].[Month].[October 2003])  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
