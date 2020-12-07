---
description: DrilldownLevelTop (MDX)
title: DrilldownLevelTop (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: af0ecdd3e53df131793f4703e154f96c51efc4e1
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194004"
---
# <a name="drilldownleveltop-mdx"></a>DrilldownLevelTop (MDX)


  セットの最上位メンバーを、指定されたレベルで1レベル下にドリルダウンします。  
  
## <a name="syntax"></a>構文  
  
```  
  
DrilldownLevelTop(<Set_Expression>, <Count> [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Count*  
 返す組の数を指定する有効な数値式です。  
  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Include_Calc_Members*  
 ドリルダウン結果に計算されるメンバーを追加するためのキーワードです。  
  
## <a name="remarks"></a>注釈  
 数値式が指定されている場合、 **DrilldownLevelTop** 関数は、指定されたセット内の各メンバーの子を、子メンバーのセットに対して評価される数値式の値に基づいて降順で並べ替えます。 数値式が指定されていない場合、指定されたセット内の各メンバーの子を、クエリ コンテキストから判別した子メンバーのセットが表すセルの値に基づいて、降順で並べ替えます。  
  
 並べ替えの後、 **DrilldownLevelTop** 関数は、親メンバーと、 *Count* で指定した子メンバーの数のうち、最大値を含むセットを返します。  
  
 **DrilldownLevelTop**関数は、[ドリルダウンレベル](../mdx/drilldownlevel-mdx.md)関数に似ていますが、指定されたレベルで各メンバーのすべての子を含めるのではなく、 **DrilldownLevelTop**関数は最上位の子メンバーの数を返します。  
  
 XMLA プロパティ MdpropMdxDrillFunctions に対してクエリを実行すると、ドリル機能に対してサーバーが提供するサポートのレベルを確認できます。詳細については、「 [サポートされる Xmla プロパティ &#40;xmla&#41;](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、既定のメジャーに基づいて、製品カテゴリレベルの上位3つの子が返されます。 Adventure Works のサンプルキューブでは、アクセサリの上位3つの子が自転車ラック、自転車のスタンド、瓶とケージです。 Management Studio では、[MDX クエリ] ウィンドウで [製品] に移動します。製品カテゴリ |Members |すべての製品 |[アクセサリ] を参照して、完全な一覧を表示します。 Count 引数を増やすと、さらに多くのメンバーを返すことができます。  
  
```  
SELECT DrilldownLevelTop   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 次の例では、ドリルダウンレベルで計算されるメンバーを含めるために使用する **include_calc_members** フラグの使用方法を示します。 メジャー [再販業者の注文数] は、 **DrilldownLevelTop** ステートメントに含まれており、戻り値がそのメジャーによって並べ替えられていることを確認します。  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELTOP(  
  [Product].[Product Categories].children ,  
  2,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX&#41;&#40;ドリルダウンレベル ](../mdx/drilldownlevel-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
