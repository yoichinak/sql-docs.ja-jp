---
description: ドリルダウンメンバートップ (MDX)
title: ドリルダウンメンバートップ (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d90c382ca34316225760c1a25288034ba26ab726
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193505"
---
# <a name="drilldownmembertop-mdx"></a>ドリルダウンメンバートップ (MDX)


  2番目に指定したセット内に存在する、指定したセットのメンバーをドリルダウンします。結果セットは、指定した数のメンバーに制限されます。 または、この関数は、最初の組階層または必要に応じて指定された階層を使用して、組のセットをドリルダウンします。  
  
## <a name="syntax"></a>構文  
  
```  
  
DrillDownMemberTop(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expression>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Count*  
 返す組の数を指定する有効な数値式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Hierarchy*  
 階層を返す有効な多次元式 (MDX) 式です。  
  
 *繰り返し*  
 セットの再帰的な比較を示すキーワードです。  
  
 *Include_Calc_Members*  
 計算されるメンバーがドリルダウン結果に含まれるようにするキーワード。  
  
## <a name="remarks"></a>注釈  
 数値式が指定されている場合、 **ドリルダウン Membertop** 関数は、1番目のセット内の各メンバーの子を、子メンバーのセットに対して評価される数値式の値に基づいて降順で並べ替えます。 数値式が指定されていない場合、関数は、クエリコンテキストによって決定される子メンバーのセットによって表されるセルの値に基づいて、最初のセット内の各メンバーの子を降順で並べ替えます。 この動作は、並べ替えを行わずに、一連のメンバーを自然な順序で返す TopCount および Head (MDX) 関数に似ています。  
  
 並べ替えの後、 **ドリルダウン Membertop** 関数は、親メンバーと子メンバーの数を含むセットを返します。これは、最大値で、 *Count* で指定したもので、両方のセットに含まれています。  
  
 **RECURSIVE**が指定されている場合、関数は、前に説明したように最初のセットを並べ替えてから、階層に編成されている最初のセットのメンバーを2番目のセットに対して再帰的に比較します。 関数は、1番目のセット内の各メンバーについて、2番目のセットにも存在する子の最上位の数を取得します。  
  
 1番目のセットには、メンバーではなく組を含めることができます。 組のドリルダウンは OLE DB の拡張機能であり、メンバーではなく組のセットを返します。  
  
 **ドリルダウンメンバートップ**関数は、[ドリルダウンメンバー](../mdx/drilldownmember-mdx.md)関数と似ていますが、2番目のセットにも含まれている最初のセット内の各メンバーのすべての子を含めるのではなく、**ドリルダウン membertop**関数は、各メンバーの子メンバーの最上位の数を返します。  
  
 XMLA プロパティ MdpropMdxDrillFunctions に対してクエリを実行すると、ドリル機能に対してサーバーが提供するサポートのレベルを確認できます。詳細については、「 [サポートされる Xmla プロパティ &#40;xmla&#41;](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、衣料カテゴリにドリルダウンして、出荷された注文の上位数量を持つ衣料の3つのサブカテゴリを返します。  
  
```  
SELECT DrilldownMemberTop   ({[Product].[Product Categories].[All Products],        
[Product].[Product Categories].[Category].Bikes,        
[Product].[Product Categories].[Category].Clothing},     
{[Product].[Product Categories].[Category].Clothing},     
3,     
[Measures].[Reseller Order Quantity])     
ON 0     
FROM [Adventure Works]     
WHERE [Measures].[Reseller Order Quantity]  
  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
