---
description: DrilldownLevelBottom (MDX)
title: DrilldownLevelBottom (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6f761c0af97cf6a9d2a5dda4e26ac2e4503a8b4b
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193994"
---
# <a name="drilldownlevelbottom-mdx"></a>DrilldownLevelBottom (MDX)


  指定されたレベルで、セットの最下位メンバーを1レベル下にドリルダウンします。  
  
## <a name="syntax"></a>構文  
  
```  
DrilldownLevelBottom(Set_Expression, Count [,[<Level_Expression>] [,[<Numeric_Expression>][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Count*  
 返す組の数を指定する有効な数値式です。  
  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression*  
 省略可能。 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Include_Calc_Members*  
 省略可能。 ドリルダウン結果に計算されるメンバーを追加するキーワード。  
  
## <a name="remarks"></a>注釈  
 数値式が指定されている場合、 **DrilldownLevelBottom** 関数は、指定されたセット内の各メンバーの子を、子メンバーのセットに対して評価されるように、指定された値に従って昇順で並べ替えます。 数値式が指定されていない場合、指定されたセット内の各メンバーの子を、クエリ コンテキストから判別した子メンバーのセットが表すセルの値に基づいて、昇順で並べ替えます。この動作は、並べ替えを行わずに自然な順序でメンバーのセットを返す、BottomCount および Tail (MDX) 関数に似ています。  
  
 並べ替えの後、 **DrilldownLevelBottom** 関数は、親メンバーと、 *Count*で指定した子メンバーの数のうち、最小値を含むセットを返します。  
  
 **DrilldownLevelBottom**関数は、[ドリルダウンレベル](../mdx/drilldownlevel-mdx.md)関数に似ていますが、指定されたレベルで各メンバーのすべての子を含めるのではなく、 **DrilldownLevelBottom**関数は、子メンバーの最下位の数を返します。  
  
 XMLA プロパティ MdpropMdxDrillFunctions に対してクエリを実行すると、ドリル機能に対してサーバーが提供するサポートのレベルを確認できます。詳細については、「 [サポートされる Xmla プロパティ &#40;xmla&#41;](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、既定のメジャーに基づいて Product Category レベルの子を最小のものから 3 つ返します。 Adventure Works のサンプルキューブでは、アクセサリの下部の3つの子はタイヤ、チューブ、ポンプ、および Panになっています。 Management Studio では、[MDX クエリ] ウィンドウで [製品] に移動します。製品カテゴリ |Members |すべての製品 |[アクセサリ] を参照して、完全な一覧を表示します。 Count 引数を増やすと、さらに多くのメンバーを返すことができます。  
  
```  
SELECT DrilldownLevelBottom   
   ([Product].[Product Categories].children,  
   3,  
   [Product].[Product Categories].[Category])  
   ON 0  
   FROM [Adventure Works]  
```  
  
 次の例では、ドリルダウンレベルで計算されるメンバーを含めるために使用する **include_calc_members** フラグの使用方法を示します。 メジャー [再販業者の注文数] が **DrilldownLevelBottom** ステートメントに追加され、結果がそのメジャーで並べ替えられるようになります。 計算されるメンバーを表示するには、カウントを少なくとも9に増やす必要があります。  
  
```  
WITH MEMBER   
[Product].[Product Categories].[Category].&[3].[Premium Clothes] AS  
[Product].[Product Categories].[Subcategory].&[18] +  
[Product].[Product Categories].[Subcategory].&[21]  
SELECT [Measures].[Reseller Order Count] ON 0,  
DRILLDOWNLEVELBOTTOM(  
  [Product].[Product Categories].children ,  
  9,  
  [Product].[Product Categories].[Category] ,  
  [Measures].[Reseller Order Count],  
  INCLUDE_CALC_MEMBERS ) ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX&#41;&#40;ドリルダウンレベル ](../mdx/drilldownlevel-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
