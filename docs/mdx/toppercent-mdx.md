---
description: TopPercent (MDX)
title: TopPercent (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f275628747d0b17ede6c76f67961fe5233e788c4
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243541"
---
# <a name="toppercent-mdx"></a>TopPercent (MDX)


  セットを降順で並べ替え、累積合計が指定した割合以上になる最大値を持つ組のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
TopPercent(Set_Expression, Percentage, Numeric_Expression)   
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Percentage*  
 返される組の割合を指定する有効な数値式です。  
  
> [!IMPORTANT]  
>  *パーセント*  は正の値である必要があります。負の値を指定すると、エラーが発生します。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **TopPercent** 関数は、指定されたセットに対して評価される指定された数値式の合計を計算し、セットを降順に並べ替えます。 次に、合計値の累積割合が指定されている割合以上になるように、最も値の大きい方から要素を返します。 この関数は、累積合計が指定した割合以上になるセットの最小サブセットを返します。 要素は大きい方から順に返されます。  
  
> [!WARNING]  
>  *Numeric_Expression* が負の値を返す場合、 **TopPercent** は1行だけを返します。  
>   
>  この動作の詳細については、2番目の例を参照してください。  
  
> [!IMPORTANT]  
>  下位 [パーセント](../mdx/bottompercent-mdx.md) 関数と同様に、 **TopPercent** 関数は常に階層を解除します。  
  
## <a name="examples"></a>例  

### <a name="a-return-toppercent"></a>A. TopPercent を返す

 次の例では、自転車カテゴリについて、再販業者の売上の上位10% を作成するのに役立つ、最適な都市が返されます。 結果は降順に並べ替えられ、sales の最高値を持つ都市から順に並べ替えられます。  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopPercent  
   ({[Geography].[Geography].[City].Members}  
   , 10  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
```  
  
 上記の式では、次の結果が生成されます。  
  
|City|Reseller Sales Amount|  
|-|---------------------------|  
|Toronto|$3508904.84|  
|London|$1521530.09|  
|Seattle|$1209418.16|  
|Paris|$1170425.18|  
  
 元のデータセットは、次のクエリを使用して取得し、588行を返すことができます。  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
Order  
   ({[Geography].[Geography].[City].Members}  
   , [Measures].[Reseller Sales Amount]  
   , BDESC  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].[Bikes])  
  
```  
  
### <a name="b-understand-the-effect-of-negative-values"></a>B. 負の値の影響を理解する

 次のチュートリアルは、 *Numeric_Expression* での負の値の効果を理解するのに役立ちます。 まず、この動作を実行できる、いくつかのコンテキストを構築します。  
  
 次のクエリでは、販売店の "Sales Amount"、"Total Product Cost"、および "粗利益" のテーブルを、利益の降順で並べ替えて返します。 利益には負の値しかないので、損失の少ないものが上位に表示されます。  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  ORDER( [Product].[Product Categories].[Bikes].[Touring Bikes].children, [Measures].[Reseller Gross Profit], BDESC )   ON rows  
FROM [Adventure Works]  
  
```  
  
 上記のクエリは、次の結果を返します。見やすくするために、中間部の行は削除してあります。  
  
|ツーリング バイク|Reseller Sales Amount|再販業者の製品コストの合計|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|ツーリング-2000 Blue、50|$157444.56|$163112.57|($5668.01)|  
|ツーリング-2000 Blue、46|$321027.03|$333021.50|($11994.47)|  
|Touring-3000 Blue, 62|$87773.61|$100133.52|($12359.91)|  
|...|...|...|...|  
|ツーリング-1000 黄、46|$1016312.83|$1234454.27|($218141.44)|  
|Touring-1000 Yellow, 60|$1184363.30|$1443407.51|($259044.21)|  
  
 このとき、利益で上位 100% の自転車を提示するように求められた場合、クエリは次のように記述されます。  
  
```  
SELECT { [Measures].[Reseller Sales Amount], [Measures].[Reseller Total Product Cost], [Measures].[Reseller Gross Profit] } ON columns  
     ,  TOPPERCENT( [Product].[Product Categories].[Bikes].[Touring Bikes].children, 100,[Measures].[Reseller Gross Profit] )   ON rows  
FROM [Adventure Works]  
  
```  
  
 クエリでは 100% (100%) が要求されることに注意してください。これは、すべての行が返されることを意味します。 ただし、 *Numeric_Expression* には負の値があるため、1行だけが返されます。  
  
|ツーリング バイク|Reseller Sales Amount|再販業者の製品コストの合計|Reseller Gross Profit|  
|-|---------------------------|---------------------------------|---------------------------|  
|ツーリング-2000 Blue、50|$157444.56|$163112.57|($5668.01)|  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
