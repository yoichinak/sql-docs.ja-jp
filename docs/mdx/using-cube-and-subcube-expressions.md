---
description: キューブ式とサブキューブ式の使用
title: Cube 式およびサブキューブ式の使用 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 37f23c75d8a947e52daf47ef9648ccbd1587b9a8
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192302"
---
# <a name="using-cube-and-subcube-expressions"></a>キューブ式とサブキューブ式の使用


  多次元式 (MDX) ステートメントでは、キューブまたはサブキューブのデータを定義、操作、または取得するために、キューブ式やサブキューブ式を使用します。  
  
## <a name="cube-expressions"></a>キューブ式  
 キューブ式には、キューブ識別子または CURRENTCUBE キーワードが含まれているので、単純式のみを指定できます。 多くの MDX ステートメントでは、キューブ識別子を要求する代わりに、CURRENTCUBE キーワードを使用して現在のキューブコンテキストを識別します。  
  
 キューブ識別子は、MDX ステートメントの BNF 表記の説明に *Cube_Name* として表示されます。  
  
 キューブ式は複数の場所に表示される場合があります。 MDX の SELECT ステートメントでは、キューブ式は、データの取得元のキューブを指定します。 次のクエリの例では、[Adventure Works] という式は、その名前のキューブを参照しています。  
  
 `SELECT [Measures].[Internet Sales Amount] ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 CREATE MEMBER ステートメントでは、キューブ式は、作成中の計算されるメンバーが表示されるキューブを指定します。 次の例では、ステートメントは、Adventure Works キューブの Measures ディメンションに対して計算されるメジャーを作成します。  
  
 `CREATE MEMBER [Adventure Works].[Measures].[Test] AS 1`  
  
 MDX スクリプト内で CREATE MEMBER ステートメントを使用すると、キューブの名前を CURRENTCUBE キーワードに置き換えることができます。これは、次の例に示すように、計算されるメンバーが作成されるキューブが、MDX スクリプトが属するキューブと同じキューブである必要があるためです。  
  
 `CREATE MEMBER CURRENTCUBE.[Measures].[Test] AS 1;`  
  
 これにより、キューブの名前がハードコーディングされなくなったため、あるキューブから別のキューブに計算されるメンバーの定義を簡単にコピーして貼り付けることができます。  
  
## <a name="subcube-expressions"></a>サブキューブ式  
 サブキューブ式には、サブキューブ識別子、またはサブキューブを返す MDX ステートメントを含めることができます。 サブキューブ式にサブキューブ識別子が含まれている場合は、単純式になります。 サブキューブを返す MDX ステートメントが含まれている場合は、複雑なステートメントです。 たとえば、次の例に示すように、MDX の SELECT ステートメントは、サブキューブを返すので、サブキューブ式が許可されている場所で使用できます。  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Date].[Calendar Year].MEMBERS ON ROWS`  
  
 `FROM`  
  
 `(SELECT [Measures].[Internet Sales Amount] ON COLUMNS,`  
  
 `[Date].[Calendar Year].&[2004] ON ROWS`  
  
 `FROM [Adventure Works])`  
  
 FROM 句での SELECT ステートメントの使用は、サブセレクトとも呼ばれます。  
  
 サブキューブ式が発生するもう1つの一般的なシナリオは、MDX スクリプトでスコープ付き割り当てを行う場合です。 次の例では、SCOPE ステートメントを使用して、[Measures] で構成されるサブキューブに割り当てを制限しています。[Internet Sales Amount]:  
  
 `SCOPE([Measures].[Internet Sales Amount]);`  
  
 `This=1;`  
  
 `END SCOPE;`  
  
 サブキューブ識別子が *Subcube_Name*として表示されます。 MDX ステートメントの BNF 表記について説明します。  
  
## <a name="see-also"></a>参照  
 [MDX の基本的なクエリ &#40;MDX&#41;](/analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query)   
 [Mdx &#40;mdx&#41;のサブキューブの作成 ](/analysis-services/multidimensional-models/mdx/building-subcubes-in-mdx-mdx)   
 [MDX&#41;&#40;サブキューブステートメントの作成 ](../mdx/mdx-data-definition-create-subcube.md)   
 [MDX &#40;式&#41;](../mdx/expressions-mdx.md)   
 [SCOPE ステートメント (MDX)](../mdx/mdx-scripting-scope.md)  
  
