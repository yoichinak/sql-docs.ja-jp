---
description: Avg (MDX)
title: Avg (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e5cac19b597139274502d455fb5f8f4e5087c8a2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477064"
---
# <a name="avg-mdx"></a>Avg (MDX)


  セットを評価し、セット内のセルの空でない値の平均を返します。この値は、セット内のメジャーまたは指定されたメジャーに対して平均します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Avg( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 空の組のセットまたは空のセットを指定した場合、 **Avg** 関数は空の値を返します。  
  
 **Avg**関数は、指定されたセット内のセルの空でない値の平均を計算します。最初に、指定したセット内のセルの値の合計を計算し、次に、指定されたセット内の空でないセルの数で計算された合計を除算します。  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、数値セットの平均値が計算される際、NULL 値は無視されます。  
  
 特定の数値式 (通常はメジャー) が指定されていない場合、 **Avg** 関数は、現在のクエリコンテキスト内で各メジャーの平均を計算します。 特定のメジャーが指定されている場合、 **Avg** 関数はまずセットに対してメジャーを評価し、次に関数は、指定されたメジャーに基づいて平均を計算します。  
  
> [!NOTE]  
>  計算されるメンバーのステートメントで **currentmember** 関数を使用する場合は、数値式を指定する必要があります。これは、このようなクエリコンテキストの現在の座標に既定のメジャーが存在しないためです。  
  
 空のセルを強制的に含めるには、アプリケーションで [CoalesceEmpty](../mdx/coalesceempty-mdx.md) 関数を使用するか、空の値にゼロ (0) の値を指定する有効な *Numeric_Expression* を指定する必要があります。 空のセルの詳細については、OLE DB のドキュメントを参照してください。  
  
## <a name="examples"></a>例  
 次の例では、指定されたセットに対するメジャーの平均値を返しています。 指定されたメジャーは、指定されたセットのメンバーの既定のメジャーであるか、または指定されたメジャーであることに注意してください。  
  
 `WITH SET [NW Region] AS`  
  
 `{[Geography].[State-Province].[Washington]`  
  
 `, [Geography].[State-Province].[Oregon]`  
  
 `, [Geography].[State-Province].[Idaho]}`  
  
 `MEMBER [Geography].[Geography].[NW Region Avg] AS`  
  
 `AVG ([NW Region]`  
  
 `--Uncomment the line below to get an average by Reseller Gross Profit Margin`  
  
 `--otherwise the average will be by whatever the default measure is in the cube,`  
  
 `--or whatever measure is specified in the query`  
  
 `--, [Measures].[Reseller Gross Profit Margin]`  
  
 `)`  
  
 `SELECT [Date].[Calendar Year].[Calendar Year].Members ON 0`  
  
 `FROM [Adventure Works]`  
  
 `WHERE ([Geography].[Geography].[NW Region Avg])`  
  
 次の例では、 `Measures.[Gross Profit Margin]` **Adventure works** キューブから、2003会計年度の各月の日付に対して計算された、メジャーの日次平均を返します。 **Avg**関数は、階層の各月に含まれる日数のセットから平均を計算し `[Ship Date].[Fiscal Time]` ます。 最初のバージョンの計算では、平均値から売上を記録しなかった日を除く Avg の既定の動作が示されています。2番目のバージョンでは、売上のない日を平均に含める方法を示しています。  
  
 `WITH MEMBER Measures.[Avg Gross Profit Margin] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `Measures.[Gross Profit Margin]`  
  
 `), format_String='percent'`  
  
 `MEMBER Measures.[Avg Gross Profit Margin Including Empty Days] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `CoalesceEmpty(Measures.[Gross Profit Margin],0)`  
  
 `), Format_String='percent'`  
  
 `SELECT`  
  
 `{Measures.[Avg Gross Profit Margin],Measures.[Avg Gross Profit Margin Including Empty Days]} ON COLUMNS,`  
  
 `[Ship Date].[Fiscal].[Fiscal Year].Members ON ROWS`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Product].&[344])`  
  
 次の例では、 `Measures.[Gross Profit Margin]` **Adventure works** キューブから、2003会計年度の各半期の日をまたいで計算された、メジャーの日次平均を返します。  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS  
   Avg(  
      Descendants(  
         [Ship Date].[Fiscal].CurrentMember,   
            [Ship Date].[Fiscal].[Date]  
      ),   
      Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
      [Ship Date].[Fiscal].[Fiscal Year].[FY 2003].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
