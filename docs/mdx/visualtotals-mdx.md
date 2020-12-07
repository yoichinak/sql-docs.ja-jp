---
description: VisualTotals (MDX)
title: VisualTotals (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1c1e85f4384c322938f5e7937c32bcd116acdda2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500425"
---
# <a name="visualtotals-mdx"></a>VisualTotals (MDX)


  指定されたセットの子メンバーの合計を動的に算出することによって生成したセットを返します。結果セット内で親メンバーの名前に対してパターンを使用することも可能です。  
  
## <a name="syntax"></a>構文  
  
```  
  
VisualTotals(Set_Expression[,Pattern])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *パターン*  
 親の名前を置き換える文字のアスタリスク (*) を格納した、セットの親メンバーを表す有効な文字列式です。  
  
## <a name="remarks"></a>解説  
 指定されたセット式では、1つのディメンション内の任意のレベルのメンバーを含むセットを指定できます。通常は、先祖と子孫のリレーションシップを持つメンバーです。 **Visualtotals**関数は、指定されたセット内の子メンバーの値の合計を計算し、結果の合計を計算する際にセットに含まれていない子メンバーを無視します。 階層の順序で並べ替えられたセットの合計は視覚的に合計されます。 セット内のメンバーの順序と階層の順序が一致しない場合、結果は表示部分の合計になりません。 たとえば、VisualTotals (USA, WA, CA, Seattle) は WA を Seattle として返すのではなく、WA、CA、および Seattle の値を返してから、これらの値の合計を USA の表示部分の合計として算出します。このため、Seattle の売上は 2 回加算されることになります。  
  
> [!NOTE]  
>  メジャーに関連付けられていないディメンションメンバーまたはメジャーグループの粒度下にあるディメンションメンバーに **Visualtotals** 関数を適用すると、値が null に置き換えられます。  
  
 *パターン*(省略可能) は、合計ラベルの形式を指定します。 *パターン* では、親メンバーの代替文字としてアスタリスク (*) が必要で、文字列内の残りのテキストは、親の名前と連結された結果に示されます。 リテラルのアスタリスクを表示するには、2つのアスタリスク () を使用し \* \* ます。  
  
## <a name="examples"></a>例  
 次の例では、指定された1つの子孫 (7 月) に基づいて、2001年の第3四半期の売上合計が返されます。  
  
```  
SELECT VisualTotals  
   ({[Date].[Calendar].[Calendar Quarter].&[2001]&[3]  
      ,[Date].[Calendar].[Month].&[2001]&[7]}) ON 0  
FROM [Adventure Works]  
```  
  
 次の例では、Product ディメンションの Category 属性階層の [All] メンバーと4つの子のうちの2つを返します。 Internet Sales Amount メジャーについて [All] メンバーに対して返される合計は、Accessories メンバーと Clothing メンバーのみの合計になります。 また、[All Products] 列のラベルを指定するために、Pattern 引数が使用されています。  
  
```  
SELECT  
   VisualTotals  
   ({[Product].[Category].[All Products]  
      ,[Product].[Category].[Accessories]  
      ,[Product].[Category].[Clothing]}  
      , '* - Visual Total'  
   ) ON Columns  
, [Measures].[Internet Sales Amount] ON Rows  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
