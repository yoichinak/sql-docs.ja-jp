---
description: Descendants (MDX)
title: 子孫 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b883d1ce73a7259b285748e5a66f283a7d830424
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491441"
---
# <a name="descendants-mdx"></a>Descendants (MDX)


  メンバーの子孫のうち、指定したレベルまたは距離にある子孫のセットを返します。他のレベルの子孫を含めたり除外したりすることもできます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member expression syntax using a level expression  
Descendants(Member_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Member_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
Set expression syntax using a level expression  
Descendants(Set_Expression [ , Level_Expression [ ,Desc_Flag ] ] )  
  
Member expression syntax using a numeric expression  
Descendants(Set_Expression [ , Distance [ ,Desc_Flag ] ] )  
  
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Level_Expression*  
 レベルを返す有効な多次元式 (MDX) 式です。  
  
 *距離*  
 指定されたメンバーからの距離を指定する有効な数値式です。  
  
 *Desc_Flag*  
 子孫のセットを区別するための説明フラグを指定する有効な文字列式です。  
  
## <a name="remarks"></a>解説  
 レベルが指定されている場合、 **子孫** 関数は、指定されたメンバーの子孫または指定されたセットのメンバーの子孫を、 *Desc_Flag*で指定されたフラグによって変更できます。  
  
 *Distance*が指定されている場合、**子孫**関数は、指定されたメンバーの子孫、または指定されたメンバーの階層内で指定されたレベル数を持つ指定されたセットのメンバーを含むセットを返します。これは、 *Desc_Flag*で指定されたフラグによって変更することもできます。 この関数は、不規則階層を対象とする場合に Distance 引数と共に使用されるのが一般的です。 距離に 0 が指定された場合は、指定されたメンバーのみで構成されるセットまたは指定されたセットを返します。  
  
 セット式が指定されている場合、 **子孫** 関数は、セットのメンバーごとに個別に解決され、セットが再度作成されます。 言い換えると、 **子孫** 関数に使用される構文は、機能的には MDX の [Generate](../mdx/generate-mdx.md) 関数と同等です。  
  
 レベルまたは距離が指定されていない場合、関数によって使用されるレベルの既定値は、 [レベル](../mdx/level-mdx.md) 関数 (<> を呼び出すことによって決定され \<Member> ます。レベル) (メンバーが指定されている場合)、または指定されたセットの各メンバーについて **レベル** 関数を呼び出した場合 (セットが指定されている場合)。 レベル式、距離、またはフラグが指定されていない場合、関数は次の構文が使用されているかのようにを実行します。  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Member_Expression.Level ,`  
  
 `SELF_BEFORE_AFTER`  
  
 `)`  
  
 レベルが指定されていて、description フラグが指定されていない場合、関数は次の構文が使用されているかのようにを実行します。  
  
 `Descendants`  
  
 `(`  
  
 `Member_Expression ,`  
  
 `Level_Expression,`  
  
 `SELF`  
  
 `)`  
  
 Description フラグの値を変更することにより、指定されたレベルまたは距離にある子孫、指定されたレベルまたは距離の前後の子 (リーフノードまで)、および指定したレベルまたは距離に関係なくリーフの子を含めたり、除外したりすることができます。 次の表では、 *Desc_Flag* 引数で使用できるフラグについて説明します。  
  
|フラグ|説明|  
|----------|-----------------|  
|SELF|指定されたレベルまたは指定された距離にある子孫メンバーのみを返します。 指定されたレベルが、指定されたメンバーのレベルである場合は、指定されたメンバーを含めます。|  
|AFTER|指定されたレベルまたは距離のすべての下位レベルにある子孫メンバーを返します。|  
|BEFORE|指定されたメンバーと指定されたレベルの間、または指定された距離のすべてのレベルにある子孫メンバーを返します。 指定されたメンバーを含みますが、指定されたレベルまたは距離のメンバーは含まれません。|  
|BEFORE_AND_AFTER|指定されたメンバーのレベルの下位にあるすべてのレベルの子孫メンバーを返します。 指定されたメンバーは含めますが、指定されたレベルまたは指定された距離にあるメンバーは含めません。|  
|SELF_AND_AFTER|指定されたレベルまたは指定された距離にある子孫メンバーと、指定されたレベルまたは指定された距離にあるすべての下位レベルを返します。|  
|SELF_AND_BEFORE|指定されたレベルまたは指定された距離、および指定されたメンバーと指定したレベルの間のすべてのレベル、または指定されたメンバーを含む指定した距離にある子孫メンバーを返します。|  
|SELF_BEFORE_AFTER|すべての下位レベルから指定したメンバーのレベルまでの子孫メンバーを返します。指定したメンバーが含まれます。|  
|LEAVES|指定されたメンバーと指定されたレベルの間、または指定された距離にあるリーフ子孫メンバーを返します。|  
  
## <a name="examples"></a>例  
 次の例では、指定されたメンバー (United States)、および指定されたメンバー (United States) と指定されたレベル (City) の前のレベルのメンバー間にあるメンバーを返しています。この例では、指定されたメンバー自体 (United States)、および State-Province レベル (City レベルの前のレベル) のメンバーが返されます。 この例には、この関数の他の引数を容易にテストできるように、コメント アウトした引数も含まれています。  
  
```  
SELECT Descendants  
   ([Geography].[Geography].[Country].&[United States]  
      //, [Geography].[Geography].[Country]  
   , [Geography].[Geography].[City]  
      //, [Geography].[Geography].Levels (3)  
      //, SELF   
      //, AFTER  
      , BEFORE  
      // BEFORE_AND_AFTER  
      //, SELF_AND_AFTER  
      //, SELF_AND_BEFORE  
      //,SELF_BEFORE_AFTER  
      //,LEAVES   
   ) ON 0  
FROM [Adventure Works]   
```  
  
 次の例では、 `Measures.[Gross Profit Margin]` **Adventure works** キューブから、2003会計年度の各月の日付に対して計算された、メジャーの日次平均を返します。 **子孫**関数は、階層の現在のメンバーから決定された日数のセットを返し `[Date].[Fiscal]` ます。  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS Avg  
   (  
      Descendants( [Date].[Fiscal].CurrentMember,   
           [Date].[Fiscal].[Date]  
          ),   
        Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
   [Date].[Fiscal].[Month].Members ON ROWS  
FROM [Adventure Works]  
WHERE ([Date].[Fiscal Year].&[2003])  
```  
  
 次の例では、レベル式を使用して、オーストラリアの州ごとの Internet Sales Amount を返し、州ごとのオーストラリアの Internet Sales Amount の合計に対する割合を返します。 この例では、Item 関数を使用して、 **先祖** 関数によって返されるセットから最初の (かつ唯一の) 組を抽出します。  
  
```  
WITH MEMBER Measures.x AS   
   [Measures].[Internet Sales Amount] /   
   ( [Measures].[Internet Sales Amount],  
      Ancestors   
         ( [Customer].[Customer Geography].CurrentMember,   
           [Customer].[Customer Geography].[Country]  
         ).Item (0)  
   ), FORMAT_STRING = '0%'  
SELECT {[Measures].[Internet Sales Amount], Measures.x} ON 0,  
{Descendants   
   ( [Customer].[Customer Geography].[Country].&[Australia],   
     [Customer].[Customer Geography].[State-Province], SELF   
   )    
} ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
