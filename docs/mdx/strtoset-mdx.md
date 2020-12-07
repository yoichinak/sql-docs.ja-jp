---
description: StrToSet (MDX)
title: StrToSet (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 882ab646af51d4b1edbe0a1240eaaed7cbfa5422
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386778"
---
# <a name="strtoset-mdx"></a>StrToSet (MDX)


  多次元式 (MDX) 形式の文字列によって指定されたセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
StrToSet(Set_Specification [,CONSTRAINED] )   
```  
  
## <a name="arguments"></a>引数  
 *Set_Specification*  
 直接的または間接的にセットを指定する有効な文字列式です。  
  
## <a name="remarks"></a>解説  
 **StrToSet**関数は、文字列式で指定されたセットを返します。 通常、 **StrToSet** 関数はユーザー定義関数と共に使用して、セットの指定を外部関数から mdx ステートメントに返すか、mdx クエリがパラメーター化されたときに使用します。  
  
-   制約付きフラグを使用する場合、セットの指定には、修飾または非修飾メンバー名、または中かっこで囲まれた修飾メンバー名または非修飾メンバー名を含む組のセットを含める必要があり {} ます。 このフラグは、指定された文字列を使用してインジェクション攻撃のリスクを軽減するために使用されます。 修飾されているメンバー名または修飾されていないメンバー名に直接解決できない文字列が指定されると、"STRTOSET 関数の CONSTRAINED フラグによって設定された制限に違反しました。" というエラーが表示されます。  
  
-   CONSTRAINED フラグを使用しない場合、セットを返す有効な多次元式 (MDX) 式に解決されるセットの指定を指定できます。  
  
-   セットとメンバーの違いについて理解を深めるには、「Set 式の使用」および「メンバー式の使用」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、 **StrToSet** 関数を使用して州の属性階層のメンバーのセットを返します。 セットの指定には、有効な MDX セット式が用意されています。  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members')  
ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、制約付きフラグによってエラーが返されます。 セットの指定には有効な MDX セット式が指定されていますが、CONSTRAINED フラグを使用する場合は、セットの指定に修飾されたメンバー名または修飾されていないメンバー名を含める必要があります。  
  
```  
SELECT StrToSet ('[Geography].[State-Province].Members', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
  
```  
  
 次の例では、ドイツおよびカナダの国の再販業者の Sales Amount メジャーを返します。 指定された文字列に指定されたセット指定には、制約付きフラグによって要求される修飾メンバー名が含まれています。  
  
```  
SELECT StrToSet ('{[Geography].[Geography].[Country].[Germany],[Geography].[Geography].[Country].[Canada]}', CONSTRAINED)  
ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
