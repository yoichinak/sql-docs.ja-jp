---
description: CoalesceEmpty (MDX)
title: CoalesceEmpty (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4fd02400d6b560e1cc0b21908b788a257f56b26c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487585"
---
# <a name="coalesceempty-mdx"></a>CoalesceEmpty (MDX)


  空のセル値を、指定した空でないセル値に変換します。数値または文字列を指定できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Numeric syntax  
CoalesceEmpty( Numeric_Expression1 [ ,Numeric_Expression2,...n] )  
  
String syntax  
CoalesceEmpty(String_Expression1 [ ,String_Expression2,...n] )  
```  
  
## <a name="arguments"></a>引数  
 *Numeric_Expression1*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Numeric_Expression2*  
 有効な数値式です。通常は、指定された数値です。  
  
 *String_Expression1*  
 有効な文字列式です。通常は、文字列を返すセル座標の多次元式 (MDX) 式です。  
  
 *String_Expression2*  
 有効な文字列式です。通常は、最初の文字列式によって返される NULL 値に置き換えられる、指定された文字列値です。  
  
## <a name="remarks"></a>解説  
 1つ以上の数値式が指定されている場合、 **CoalesceEmpty** 関数は、空でない値に解決できる最初の数値式 (左から右) の数値を返します。 指定されている数値式に、空でない値に解決される式がない場合、この関数は、空のセル値を返します。 通常、2番目の数値式の値は、最初の数値式によって返される NULL 値に置き換えられる数値です。  
  
 1つ以上の文字列式が指定されている場合、関数は、空でない値に解決できる最初の文字列式 (左から右) の文字列値を返します。 指定された文字列式のいずれも空でない値に解決できない場合、関数は空のセル値を返します。 通常、2番目の文字列式の値の値は、最初の文字列式から返された NULL を置き換える文字列値です。  
  
 **CoalesceEmpty**関数は、同じ型の値のみを受け取ることができます。 つまり、指定した値式は、すべて 1 つの数値データ型または空のセル値に評価されるか、すべて 1 つの文字列データ型または空のセル値に評価される必要があります。 この関数の 1 回の呼び出しで、数値式と文字列式を両方含めることはできません。  
  
 空のセルの詳細については、OLE DB のドキュメントを参照してください。  
  
## <a name="example"></a>例  
 次の例では、 **Adventure works** キューブに対してクエリを実行します。 この例では、各製品の注文数量と、カテゴリ別の注文数量の割合を返します。 **CoalesceEmpty**関数は、計算されるメンバーの書式を設定するときに、null 値がゼロ (0) として表されるようにします。  
  
```  
WITH   
   MEMBER [Measures].[Order Percent by Category] AS  
   CoalesceEmpty(   
      ([Product].[Product Categories].CurrentMember,  
        Measures.[Order Quantity]) /   
          (  
           Ancestor  
           ( [Product].[Product Categories].CurrentMember,   
             [Product].[Product Categories].[Category]  
           ), Measures.[Order Quantity]  
       ), 0  
   ), FORMAT_STRING='Percent'  
SELECT   
   {Measures.[Order Quantity],  
      [Measures].[Order Percent by Category]} ON COLUMNS,  
{[Product].[Product].Members} ON ROWS  
FROM [Adventure Works]  
WHERE {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
