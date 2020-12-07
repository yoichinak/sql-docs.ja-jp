---
description: IIf (MDX)
title: IIf (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8a9a8da3ec20a34ba1dea30b1285d6a9c147e55d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387468"
---
# <a name="iif-mdx"></a>IIf (MDX)


  ブール条件が true か false かに応じて、異なる分岐の式を評価します。  
  
## <a name="syntax"></a>構文  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>引数  
 IIf 関数は、iif ( \<condition> ,,) という3つの引数を受け取ります \<then branch> \<else branch> 。  
  
 *Logical_Expression*  
 **True** (1) または**false** (0) に評価される条件。 有効な多次元式 (MDX) の論理式を指定する必要があります。  
  
 *Expression1 ヒント [一括 |Strict |Lazy]]*  
 論理式が **true**と評価されるときに使用されます。 Expression1 有効な多次元式 (MDX) 式を指定する必要があります。  
  
 *Expression2 ヒント [一括 |Strict |Lazy]]*  
 論理式が **false**に評価されるときに使用されます。 Expression2 には、有効な多次元式 (MDX) を指定する必要があります。  
  
## <a name="remarks"></a>解説  
 論理式で指定された条件は、この式の値が0の場合は **false** に評価されます。 その他の値は **true**に評価されます。  
  
 条件が **true**の場合、 **IIf** 関数は最初の式を返します。 それ以外の場合、関数は2番目の式を返します。  
  
 指定された式は、値または MDX オブジェクトを返すことができます。 また、1 番目と 2 番目の式の型は一致しなくてもかまいません。  
  
 **IIf**関数は、検索条件に基づいてメンバーのセットを作成する場合は推奨されません。 代わりに、 [Filter](../mdx/filter-mdx.md) 関数を使用して、指定されたセット内の各メンバーを論理式に対して評価し、メンバーのサブセットを返します。  
  
> [!NOTE]  
>  いずれかの式が NULL に評価された場合、その条件が満たされると結果セットは NULL になります。  
  
 ヒントは、式を評価する方法とタイミングを決定するオプションの修飾子です。 これにより、式の評価方法を指定することによって、既定のクエリプランをオーバーライドできます。  
  
-   一括では、元の IIF サブ空間に対して式が評価されます。  
  
-   STRICT を指定すると、論理条件式によって作成された制限付きのサブ空間のみで式が評価されます。  
  
-   レイジーは、セルごとのモードで式を評価します。  
  
 "一括" と "厳密" は IIF の then 分岐にのみ適用されますが、LAZY はすべての MDX 式に適用されます。 任意の MDX 式の後にヒントレイジーを指定すると、その式がセル単位のモードで評価されます。  
  
 集中と厳密はヒントで相互に排他的です。これらは、異なる式で同じ IIF (,,) で使用できます。  
  
 詳細については、「 [SQL Server Analysis Services 2008 の IIF 関数のクエリヒント](http://www.ssas-info.com/analysis-services-articles/50-mdx/1103-iif-function-query-hints-in-sql-server-analysis-services-2008) 」および「 [MDX の IIF 関数と CASE ステートメントの実行プランとプランヒント](https://go.microsoft.com/fwlink/?LinkId=269565)」を参照してください。  
  
## <a name="examples"></a>例  
 次のクエリは、計算されるメジャー内の **IIF** を使用して、Internet Sales Amount メジャーが $1万より大きいか、または未満の場合に、2つの異なる文字列値のいずれかを返す簡単な方法を示しています。  
  
 `WITH MEMBER MEASURES.IIFDEMO AS`  
  
 `IIF([Measures].[Internet Sales Amount]>10000`  
  
 `, "Sales Are High", "Sales Are Low")`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.IIFDEMO} ON 0,`  
  
 `[Date].[Date].[Date].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 IIF の非常に一般的な用途は、次の例に示すように、計算されるメジャー内で "ゼロによる除算" エラーを処理することです。  
  
 `WITH`  
  
 `//Returns 1.#INF when the previous period contains no value`  
  
 `//but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth With Errors] AS`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `,FORMAT_STRING='PERCENT'`  
  
 `//Traps division by zero and returns null when the previous period contains`  
  
 `//no value but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth] AS`  
  
 `IIF(([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)=0,`  
  
 `NULL,`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `),FORMAT_STRING='PERCENT'`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.[Previous Period Growth With Errors], MEASURES.[Previous Period Growth]} ON 0,`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004],`  
  
 `[Date].[Calendar].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 次の例では、Generate 関数内の2つのセットのいずれか **を返して** 、行に組の複雑なセットを作成しています。  
  
 `SELECT {[Measures].[Internet Sales Amount]} ON 0,`  
  
 `//If Internet Sales Amount is zero or null`  
  
 `//returns the current year and the All Customers member`  
  
 `//else returns the current year broken down by Country`  
  
 `GENERATE(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `, IIF([Measures].[Internet Sales Amount]=0,`  
  
 `{([Date].[Calendar Year].CURRENTMEMBER, [Customer].[Country].[All Customers])}`  
  
 `, {{[Date].[Calendar Year].CURRENTMEMBER} * [Customer].[Country].[Country].MEMBERS}`  
  
 `))`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 最後に、この例では、プランヒントの使用方法を示します。  
  
 `WITH MEMBER MEASURES.X AS`  
  
 `IIF(`  
  
 `[Measures].[Internet Sales Amount]=0`  
  
 `, NULL`  
  
 `, (1/[Measures].[Internet Sales Amount]) HINT EAGER)`  
  
 `SELECT {[Measures].x} ON 0,`  
  
 `[Customer].[Customer Geography].[Country].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
