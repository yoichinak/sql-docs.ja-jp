---
description: 文字列関数の使用
title: 文字列関数の使用 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2160662a5e8fe9e89e133e053cca820fc60a66e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500485"
---
# <a name="using-string-functions"></a>文字列関数の使用


  文字列関数は、多次元式 (MDX) 内のほとんどすべてのオブジェクトに対して使用できます。 ストアド プロシージャでは、主にオブジェクトを文字列表記に変換するために文字列関数を使用します。 文字列関数を使用して、値を返すためにオブジェクトに対して文字列式を評価することもできます。  
  
 最も広く使用されている文字列関数は、 **Name** と **Uniquename**です。 これらの関数はそれぞれ、オブジェクトの名前と一意の名前を返します。 ほとんどの場合、これらは、計算をデバッグする際に、関数によって返されるメンバーを検出するために使用されます。  
  
## <a name="examples"></a>例  
 次のクエリ例では、これらの関数の使用方法を示しています。  
  
 `WITH`  
  
 `//Returns the name of the current Product on rows`  
  
 `MEMBER [Measures].[ProductName] AS [Product].[Product].CurrentMember.Name`  
  
 `//Returns the uniquename of the current Product on rows`  
  
 `MEMBER [Measures].[ProductUniqueName] AS [Product].[Product].CurrentMember.Uniquename`  
  
 `//Returns the name of the Product dimension`  
  
 `MEMBER [Measures].[ProductDimensionName] AS [Product].Name`  
  
 `SELECT  {[Measures].[ProductName],[Measures].[ProductUniqueName],[Measures].[ProductDimensionName]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 **Generate**関数を使用すると、セットのすべてのメンバーに対して文字列関数を実行し、結果を連結できます。 これは、セットの内容を視覚化できるように計算をデバッグする場合にも役立ちます。 次の例では、この用途で関数を使用する方法を示します。  
  
 `WITH`  
  
 `//Returns the names of the current Product and its ancestors up to the All Member`  
  
 `MEMBER [Measures].[AncestorNames] AS`  
  
 `GENERATE(`  
  
 `ASCENDANTS([Product].[Product Categories].CurrentMember)`  
  
 `, [Product].[Product Categories].CurrentMember.Name, ", ")`  
  
 `SELECT`  
  
 `{[Measures].[AncestorNames]}`  
  
 `ON COLUMNS,`  
  
 `[Product].[Product Categories].MEMBERS  ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 広く使用されている文字列関数のグループとして、オブジェクトの uniquename を含む文字列、またはオブジェクトに解決される式をオブジェクト自体にキャストできるものがあります。 次のクエリの例では、 **Strtomember** 関数と **StrToSet** 関数がこの処理を実行する方法を示しています。  
  
 `SELECT`  
  
 `{StrToMember("[Measures].[Inter" + "net Sales Amount]")}`  
  
 `ON COLUMNS,`  
  
 `StrToSet("{`  
  
 `[Product].[Product Categories].[Category].&[3],`  
  
 `[Product].[Product Categories].[Product].&[477],`  
  
 `[Product].[Product Categories].[Product].&[788],`  
  
 `[Product].[Product Categories].[Product].&[708],`  
  
 `[Product].[Product Categories].[Product].&[711]`  
  
 `}")`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
> [!NOTE]  
>  **Strtomember**関数と**StrToSet**関数は、注意して使用する必要があります。 計算定義内で使用されている場合、クエリのパフォーマンスが低下する可能性があります。  
  
## <a name="see-also"></a>参照  
 [MDX&#41;を生成 &#40;](../mdx/generate-mdx.md)   
 [MDX&#41;&#40;名前 ](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [関数 &#40;MDX 構文&#41;](../mdx/functions-mdx-syntax.md)   
 [MDX&#41;&#40;のストアドプロシージャの使用 ](../mdx/using-stored-procedures-mdx.md)   
 [StrToMember &#40;MDX&#41;](../mdx/strtomember-mdx.md)   
 [StrToSet &#40;MDX&#41;](../mdx/strtoset-mdx.md)  
  
  
