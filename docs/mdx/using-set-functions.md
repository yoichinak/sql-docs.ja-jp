---
description: 集合関数の使用
title: Set Functions | を使用するMicrosoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1325055017eeee392cd098d9168dd247a2664aa4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476984"
---
# <a name="using-set-functions"></a>集合関数の使用


  集合関数は、ディメンション、階層、レベルからセットを取得します。あるいは、それらのオブジェクト内でのメンバーの絶対位置および相対位置をトラバースすることにより、さまざまな方法でセットを構築します。  
  
 メンバー関数や組関数などのセット関数は、Analysis Services で見つかった多次元構造をネゴシエートするために不可欠です。 セット式は MDX クエリの軸を定義するため、多次元式 (MDX) クエリから結果を取得するには、set 関数も不可欠です。  
  
 最も一般的なセット関数の1つは、ディメンション、階層、またはレベルのすべてのメンバーを含むセットを取得する [MDX&#41;関数&#41; &#40;設定 &#40;メンバー ](../mdx/members-set-mdx.md) です。 クエリ内でのこの関数の使用例を次に示します。  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns all of the members on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 もう1つの一般的に使用される関数は、 [Crossjoin &#40;MDX&#41;](../mdx/crossjoin-mdx.md) 関数です。 この関数は、パラメーターとして渡されるセットのデカルト積を表す組のセットを返します。 実際には、この関数を使用すると、クエリに ' nested ' または ' crosstabbed ' の軸を作成できます。  
  
 `SELECT`  
  
 `//Returns all of the members on the Measures dimension`  
  
 `[Measures].MEMBERS`  
  
 `ON Columns,`  
  
 `//Returns a set containing every combination of all of the members`  
  
 `//on the Calendar Year level of the Calendar Year Hierarchy`  
  
 `//on the Date dimension and all of the members on the Category level`  
  
 `//of the Category hierarchy on the Product dimension`  
  
 `Crossjoin(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS,`  
  
 `[Product].[Category].[Category].MEMBERS)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 [MDX&#41;関数の子孫 &#40;](../mdx/descendants-mdx.md)は、 **Children**関数と似ていますが、より強力です。 階層内の1つ以上のレベルにあるメンバーの子孫を返します。  
  
 SELECT  
  
 [Measures]。[Internet Sales Amount]  
  
 ON Columns,  
  
 //Returns a set containing all of the Dates beneath Calendar Year  
  
 2004 Date ディメンションの Calendar 階層内の  
  
 派生  
  
 [Date]。[カレンダー]。[Calendar Year] & [2004]  
  
 , [Date].[Calendar].[Date])  
  
 ON Rows  
  
 FROM [Adventure Works]  
  
 [Order &#40;MDX&#41;](../mdx/order-mdx.md)関数を使用すると、特定の数値式に従って、セットの内容を昇順または降順で並べ替えることができます。 次のクエリでは、前のクエリと同じ行のメンバーが返されますが、現在は Internet Sales Amount メジャーによって並べ替えられています。  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//ordered by Internet Sales Amount`  
  
 `ORDER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount], BDESC)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 また、このクエリは、1つの set 関数 (子孫) から返されたセットを別の set 関数にパラメーターとして渡す方法も示しています。  
  
 特定の条件に従ってセットをフィルター処理することは、クエリを記述するときに非常に便利です。このためには、次の例に示すように、 [Filter &#40;MDX&#41;](../mdx/filter-mdx.md) 関数を使用できます。  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//where Internet Sales Amount is greater than $70000`  
  
 `FILTER(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `, [Measures].[Internet Sales Amount]>70000)`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 また、他の方法でセットにフィルターを適用できるようにする、さらに高度な関数もあります。 たとえば、次のクエリは、 [TopCount &#40;MDX&#41;](../mdx/topcount-mdx.md) 関数が set 内の上位 n 個の項目を返すことを示しています。  
  
 `SELECT`  
  
 `[Measures].[Internet Sales Amount]`  
  
 `ON Columns,`  
  
 `//Returns a set containing the top 10 Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension by Internet Sales Amount`  
  
 `TOPCOUNT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,10, [Measures].[Internet Sales Amount])`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
 最後に、複数の論理セット操作を実行することもできます。たとえば、 [Intersect &#40;mdx&#41;](../mdx/intersect-mdx.md)、 [Union &#40;mdx&#41;](../mdx/union-mdx.md) などの関数を使用し、 [mdx &#40;](../mdx/except-mdx-function.md) 関数を除きます。 次のクエリは、後者の2つの関数の例を示しています。  
  
 `SELECT`  
  
 `//Returns a set containing the Measures Internet Sales Amount, Internet Tax Amount and`  
  
 `//Internet Total Product Cost`  
  
 `UNION(`  
  
 `{[Measures].[Internet Sales Amount], [Measures].[Internet Tax Amount]}`  
  
 `, {[Measures].[Internet Total Product Cost]}`  
  
 `)`  
  
 `ON Columns,`  
  
 `//Returns a set containing all of the Dates beneath Calendar Year`  
  
 `//2004 in the Calendar hierarchy of the Date dimension`  
  
 `//except the January 1st 2004`  
  
 `EXCEPT(`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004]`  
  
 `, [Date].[Calendar].[Date])`  
  
 `,{[Date].[Calendar].[Date].&[915]})`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [関数 &#40;MDX 構文&#41;](../mdx/functions-mdx-syntax.md)   
 [メンバー関数の使用](../mdx/using-member-functions.md)   
 [組関数の使用](../mdx/using-tuple-functions.md)  
  
  
