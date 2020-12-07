---
description: StrToMember (MDX)
title: StrToMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68d2d99bb51412a98919d1ab1626c7a86bd86245
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386808"
---
# <a name="strtomember-mdx"></a>StrToMember (MDX)


  多次元式 (MDX) 形式の文字列によって指定されたメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
StrToMember(Member_Name [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>引数  
 *Member_Name*  
 メンバーを直接または間接的に指定する有効な文字列式です。  
  
## <a name="remarks"></a>解説  
 **Strtomember**関数は、文字列式で指定されたメンバーを返します。 **Strtomember**関数は、通常、メンバーの指定を外部関数から mdx ステートメントに返す場合、または mdx クエリがパラメーター化される場合に、ユーザー定義関数と共に使用されます。  
  
-   CONSTRAINED フラグを使用するときは、メンバー名には修飾されているメンバー名または修飾されていないメンバー名に直接解決できる文字列を指定する必要があります。 このフラグは、指定された文字列を使用してインジェクション攻撃のリスクを軽減するために使用されます。 修飾されているメンバー名または修飾されていないメンバー名に直接解決できない文字列を指定すると、"STRTOMEMBER 関数の CONSTRAINED フラグによって設定された制限に違反しました。" というエラーが表示されます。  
  
-   CONSTRAINED フラグを使用しない場合、メンバー名に直接解決されるメンバーも、名前に解決される MDX 式に解決されるメンバーも指定できます。  
  
-   セットとメンバーの違いについて理解を深めるには、「Set 式の使用」および「メンバー式の使用」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、 **Strtomember** 関数を使用して州州属性階層の Bayern メンバーの再販業者 Sales Amount メジャーを返します。 文字列の指定により、修飾されているメンバー名が指定されています。  
  
```  
SELECT {StrToMember ('[Geography].[State-Province].[Bayern]')}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 次の例では、 **Strtomember** 関数を使用して、Bayern メンバーの再販業者 Sales Amount メジャーを返します。 メンバー名文字列には修飾されていないメンバー名のみを指定したので、クエリは指定メンバーの最初のインスタンスを返します。この最初のインスタンスは、Reseller Sales と交差しない Customer ディメンションの Customer Geography 階層にあります。 ベストプラクティスでは、想定される結果を得るために、修飾名を指定します。  
  
```  
SELECT {StrToMember ('[Bayern]').Parent}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 次の例では、 **Strtomember** 関数を使用して州州属性階層の Bayern メンバーの再販業者 Sales Amount メジャーを返します。 指定されたメンバー名文字列は、修飾メンバー名に解決されます。  
  
```  
SELECT {StrToMember('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)}  
ON 0,  
{[Measures].[Reseller Sales Amount]} ON 1  
FROM [Adventure Works]  
  
```  
  
 次の例では、制約付きフラグによってエラーが返されます。 指定されたメンバー名文字列には、修飾メンバー名に解決される有効な MDX メンバー式が含まれていますが、制約フラグでは、メンバー名文字列に修飾されたメンバー名または修飾されていないメンバー名が必要です。  
  
```  
SELECT StrToMember ('[Geography].[Geography].[Country].[Germany].FirstChild', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
