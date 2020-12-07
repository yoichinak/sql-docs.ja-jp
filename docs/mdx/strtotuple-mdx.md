---
description: StrToTuple (MDX)
title: StrToTuple (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6df003fcbac42c791cc6939dfc96d316c89f4612
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386768"
---
# <a name="strtotuple-mdx"></a>StrToTuple (MDX)


  多次元式 (MDX) 形式の文字列によって指定された組を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
StrToTuple(Tuple_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>引数  
 *Tuple_Specification*  
 直接的または間接的に組を指定する有効な文字列式です。  
  
## <a name="remarks"></a>解説  
 **Strtotuple**関数は、指定されたセットを返します。 **Strtotuple**関数は、通常、外部関数から MDX ステートメントに組の指定を返すために、ユーザー定義関数と共に使用されます。  
  
-   CONSTRAINED フラグを使用するときは、組指定に修飾されているメンバー名または修飾されていないメンバー名を含める必要があります。 このフラグは、指定された文字列を使用してインジェクション攻撃のリスクを軽減するために使用されます。 修飾されたメンバー名または修飾されていないメンバー名に直接解決できない文字列が指定されると、"STRTOTUPLE 関数の制約付きフラグによって設定された制限に違反しました。" というエラーが表示されます。  
  
-   CONSTRAINED フラグを使用しない場合、組を返す有効な MDX 式に解決される組を指定できます。  
  
## <a name="examples"></a>例  
 次の例では、2004年の Bayern メンバーの再販業者 Sales Amount メジャーを返します。 組の指定には、有効な MDX 組式が含まれています。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、2004年の Bayern メンバーの再販業者 Sales Amount メジャーを返します。 指定された組の指定には、制約付きフラグによる要求に従って、修飾されたメンバー名が含まれます。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].[CY 2004], [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、2004年の Bayern メンバーの再販業者 Sales Amount メジャーを返します。 組の指定には、有効な MDX 組式が含まれています。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、制約付きフラグによってエラーが返されます。 指定された組の指定に有効な MDX 組式が含まれていますが、制約付きフラグには組の指定に修飾されたメンバー名または非修飾メンバー名が必要です。  
  
```  
SELECT StrToTuple ('([Geography].[State-Province].[Bayern],[Date].[Calendar Year].&[2003].NEXTMEMBER, [Measures].[Reseller Sales Amount])', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>関連項目  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
