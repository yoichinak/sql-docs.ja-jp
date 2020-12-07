---
description: 生成 (MDX)
title: Generate (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9746d83589464f75bbc951c20dc15d04b7b2037d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429954"
---
# <a name="generate-mdx"></a>生成 (MDX)


  あるセットを別のセットの各メンバーに適用し、その結果セットを和集合で結合します。 または、この関数は、セットに対して文字列式を評価することによって作成された連結文字列を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set expression syntax  
Generate( Set_Expression1 ,  Set_Expression2 [ , ALL ]  )  
  
String expression syntax  
Generate( Set_Expression1 ,  String_Expression [ ,Delimiter ]  )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *String_Expression*  
 有効な文字列式です。通常は、指定されたセット内の各組の現在のメンバーの名前 (CurrentMember.Name) です。  
  
 *区切り記号*  
 文字列式として表された有効な区切り記号です。  
  
## <a name="remarks"></a>解説  
 2番目のセットを指定した場合、 **Generate** 関数は、2番目のセット内の組を1つ目のセット内の各組に適用して生成されたセットを返し、和集合によって結果セットを結合します。 **ALL**を指定した場合、関数は結果セット内の重複部分を保持します。  
  
 文字列式が指定されている場合、 **Generate** 関数は、最初のセット内の各組に対して指定された文字列式を評価し、結果を連結することによって生成される文字列を返します。 必要に応じて、文字列を区切り、結果として連結された文字列内の各結果を区切ることができます。  
  
## <a name="examples"></a>例  
  
### <a name="set"></a>オン  
 次の例では、set [Date] に4つのメンバーがあるため、Internet Sales amount メジャーを含むセットが返されます。[Calendar Year]。[Calendar Year]。属する  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]}, ALL)  
ON 0  
FROM [Adventure Works]  
```  
  
 ALL を削除すると、クエリが変更され、Internet Sales Amount が 1 回だけ返されるようになります。  
  
```  
SELECT   
GENERATE( [Date].[Calendar Year].[Calendar Year].MEMBERS  
, {[Measures].[Internet Sales Amount]})  
ON 0  
FROM [Adventure Works]  
```  
  
 **Generate**の最も一般的な用途は、メンバーのセットに対して TopCount などの複雑なセット式を評価することです。 次のクエリの例では、行に各暦年の上位10個の製品が表示されます。  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS  
, TOPCOUNT(  
[Date].[Calendar Year].CURRENTMEMBER  
*  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount]))  
ON 1  
FROM [Adventure Works]  
```  
  
 年ごとに異なる上位10件が表示され、この結果を取得する唯一の方法は [ **生成** の使用] であることに注意してください。 次の例に示すように、Calendar year と上位10製品のセットをクロス結合するだけで、すべての時間について上位10製品が表示されます。  
  
```  
SELECT   
{[Measures].[Internet Sales Amount]}  
ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS  
*   
TOPCOUNT(  
[Product].[Product].[Product].MEMBERS  
,10, [Measures].[Internet Sales Amount])  
ON 1  
FROM [Adventure Works]  
```  
  
### <a name="string"></a>文字列型  
 次の例は、 **Generate** を使用して文字列を返す方法を示しています。  
  
```  
WITH   
MEMBER MEASURES.GENERATESTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME)  
MEMBER MEASURES.GENERATEDELIMITEDSTRINGDEMO AS  
GENERATE(   
[Date].[Calendar Year].[Calendar Year].MEMBERS,  
[Date].[Calendar Year].CURRENTMEMBER.NAME, " AND ")  
SELECT   
{MEASURES.GENERATESTRINGDEMO, MEASURES.GENERATEDELIMITEDSTRINGDEMO}  
ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  この形式の **Generate** 関数は、計算をデバッグするときに便利です。これにより、セット内のすべてのメンバーの名前を表示する文字列を返すことができます。 これは、 [Settostr &#40;MDX&#41;](../mdx/settostr-mdx.md) 関数が返すセットの厳密な MDX 表現よりも読みやすくなる可能性があります。  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
