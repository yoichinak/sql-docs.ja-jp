---
description: Exists (MDX)
title: Exists (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9c879d9091c692cfa7a93490b34c70ad84fa81c4
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193974"
---
# <a name="exists-mdx"></a>Exists (MDX)


  1 番目に指定されている組のセットのうち、2 番目に指定されているセットの 1 つ以上の組と共存する組のセットを返します。 この関数は、自動 exists が自動的に実行する内容を手動で実行します。 自動 exists の詳細については、「 [MDX &#40;Analysis Services&#41;の主要概念 ](/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)」を参照してください。  
  
 省略可能なが指定されている場合、 \<Measure Group Name> 関数は、2番目のセットの1つ以上の組と、指定されたメジャーグループのファクトテーブル内の行に関連付けられている組を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Exists( Set_Expression1 , Set_Expression2 [, MeasureGroupName] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *MeasureGroupName*  
 メジャーグループ名を指定する有効な文字列式です。  
  
## <a name="remarks"></a>注釈  
  
1.  Null 値を含んでいるメジャーを含むメジャーグループ行は、MeasureGroupName 引数が指定されている場合に **存在** することになります。 この形式の Exists と空でない関数の違いは次のようになります。これらのメジャーの NullProcessing プロパティが Preserve に設定されている場合、キューブのその部分に対してクエリを実行すると、メジャーで Null 値が表示されることを意味します。空でない場合は、メジャー値が Null のセットからは常にタプルが削除されます。一方、MeasureGroupName 引数を指定すると、メジャー値が Null の場合でも、メジャーグループ行に関連付けられているタプルはフィルター処理されません。  
  
2.  *Measuregroupname*パラメーターが使用されている場合、結果は、参照先のメジャーグループに表示されるメジャーがあるかどうかによって異なります。参照先のメジャーグループに表示されるメジャーがない場合、EXISTS は、 *Set_Expression1*と*Set_Expression2*の値に関係なく、常に空のセットを返します。  
  
## <a name="examples"></a>例  
 カリフォルニア州在住のお客様:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
) ON 1   
FROM [Adventure Works]  
  
```  
  
 売上があるカリフォルニア在住のお客様:  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Customer].[State-Province].&[CA]&[US]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 売上があった顧客  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, , "Internet Sales") ON 1   
FROM [Adventure Works]  
  
```  
  
 自転車を購入した顧客  
  
```  
SELECT [Measures].[Internet Sales Amount] ON 0,  
EXISTS(  
[Customer].[Customer].[Customer].MEMBERS  
, {[Product].[Product Categories].[Category].&[1]}  
, "Internet Sales") ON 1   
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [Mdx 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Crossjoin &#40;MDX&#41;](../mdx/crossjoin-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX&#41;](../mdx/nonemptycrossjoin-mdx.md)   
 [空でない &#40;MDX の&#41;](../mdx/nonempty-mdx.md)   
 [IsEmpty &#40;MDX&#41;](../mdx/isempty-mdx.md)  
  
