---
description: LastPeriods (MDX)
title: LastPeriods (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 60e8adf1dba453fb536f95a4fa113e16f6950f62
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494885"
---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)


  指定されたメンバーまでのメンバーのセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Index*  
 期間の数を指定する有効な数値式です。  
  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 指定された期間の数が正の場合、 **lastperiods** 関数は、指定されたメンバー式から *インデックス* -1 を遅延するメンバーで始まり、指定されたメンバーで終わるメンバーのセットを返します。 関数によって返されるメンバーの数は、 *Index*と同じです。  
  
 指定された期間の数が負の値の場合、 **lastperiods** 関数は、指定されたメンバーで始まり、指定されたメンバーから (- *Index* -1) のメンバーで終わるメンバーのセットを返します。 関数によって返されるメンバーの数は、 *インデックス*の絶対値と同じです。  
  
 指定された期間の数が0の場合、 **lastperiods** 関数は空のセットを返します。 これは **Lag** 関数とは異なり、0が指定されている場合は、指定されたメンバーを返します。  
  
 メンバーが指定されていない場合、 **Lastperiods** 関数は、 **Time. currentmember**を使用します。 ディメンションが時間ディメンションとしてマークされていない場合、関数はエラーを発生させずに解析して実行しますが、クライアントアプリケーションではセルエラーが発生します。  
  
## <a name="examples"></a>例  
 次の例では、2002会計年度の第2第3四半期と第4四半期の既定のメジャー値が返されます。  
  
```  
SELECT LastPeriods(3,[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]) ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  この例は、: (コロン) 演算子を使用して記述することもできます。  
>   
>  `[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]: [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2002]`  
  
 次の例では、2002会計年度の最初の会計四半期の既定のメジャー値が返されます。 指定された期間の数は 3 ですが、この会計年度より前の期間が存在しないため、返すことができる期間は 1 つだけです。  
  
```  
SELECT LastPeriods  
   (3,[Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
