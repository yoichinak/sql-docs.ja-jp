---
description: Order (MDX)
title: Order (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4db745ea01a56d68fe259ebb2fffb5aae250abd4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471744"
---
# <a name="order-mdx"></a>Order (MDX)


  指定されたセットのメンバーを整列します。必要に応じて、階層を維持または分割します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Numeric expression syntax  
Order(Set_Expression, Numeric_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
String expression syntax  
Order(Set_Expression, String_Expression   
[ , { ASC | DESC | BASC | BDESC } ] )  
  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *String_Expression*  
 有効な文字列式です。通常は、文字列として表現された数値を返すセル座標の有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **Order**関数は、( **ASC**または**desc**フラグを使用して指定されたように)、または非階層型 ( **basc**または**bdesc**フラグを使用して指定された) のいずれかにすることができます。 **B**は "break hierarchy" を表します。 **ASC**または**DESC**が指定されている場合、 **Order**関数は、まず階層内の位置に基づいてメンバーを配置し、次に各レベルを順序付けます。 **Basc**または**bdesc**が指定されている場合、 **Order**関数は、階層に関係なく、セット内のメンバーを整列します。 フラグを指定しない場合、 **ASC** が既定値になります。  
  
 2つ以上の階層がクロス結合されているセットで **Order** 関数が使用されていて、 **DESC** フラグが使用されている場合、セット内の最後の階層のメンバーのみが並べ替えられます。 この点が Analysis Services 2000 とは異なります。Analysis Services 2000 では、セットのすべての階層が並べ替えられます。  
  
## <a name="examples"></a>例  
 次の例では、 **Adventure works** キューブから、Date ディメンションの calendar 階層のすべての四半期の再販業者の注文数を返します。 **Order** 関数は、ROWS 軸のセットを並べ替えます。 **Order**関数は、階層によって決定される階層の降順でセットを並べ替え `[Reseller Order Count]` `[Calendar]` ます。  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,DESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 この例では、 **DESC** フラグが **bdesc**に変更されると、階層が破損し、階層に関係なく、カレンダー四半期の一覧が返されます。  
  
 `SELECT`  
  
 `Measures.[Reseller Order Count] ON COLUMNS,`  
  
 `Order(`  
  
 `[Date].[Calendar].[Calendar Quarter].MEMBERS`  
  
 `,Measures.[Reseller Order Count]`  
  
 `,BDESC`  
  
 `) ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 次の例では、階層とは無関係に、Reseller Gross Profit に基づいて、売上が上位 5 番目までの製品のサブカテゴリに対応する Reseller Sales メジャーを返しています。 **サブセット**関数は、 **Order**関数を使用して結果が並べ替えられた後に、セット内の最初の5組のみを返すために使用されます。  
  
 `SELECT Subset`  
  
 `(Order`  
  
 `([Product].[Product Categories].[SubCategory].members`  
  
 `,[Measures].[Reseller Gross Profit]`  
  
 `,BDESC`  
  
 `)`  
  
 `,0`  
  
 `,5`  
  
 `) ON 0`  
  
 `FROM [Adventure Works]`  
  
 次の例では、 **rank** 関数を使用して、再販業者の Sales Amount メジャーに基づいて City 階層のメンバーにランクを付け、順位の順に表示します。 **Order**関数を使用して City 階層のメンバーのセットを最初に並べ替えると、並べ替えは一度だけ実行された後、線形スキャンが行われてから、並べ替えられた順序で表示されます。  
  
```  
WITH   
SET OrderedCities AS Order  
   ([Geography].[City].[City].members  
   , [Measures].[Reseller Sales Amount], BDESC  
   )  
MEMBER [Measures].[City Rank] AS Rank  
   ([Geography].[City].CurrentMember, OrderedCities)  
SELECT {[Measures].[City Rank],[Measures].[Reseller Sales Amount]}  ON 0   
,Order  
   ([Geography].[City].[City].MEMBERS  
   ,[City Rank], ASC)  
    ON 1  
FROM [Adventure Works]  
```  
  
 次の例では、**フィルター**関数を使用する前に、 **order**関数を使用して空でない組を並べ替える、セット内の一意の製品の数を返します。 **Currentordinal**関数は、結合を比較し、削除するために使用されます。  
  
```  
WITH MEMBER [Measures].[PrdTies] AS Count  
   (Filter  
      (Order  
        (NonEmpty  
          ([Product].[Product].[Product].Members  
          , {[Measures].[Reseller Order Quantity]}  
          )  
       , [Measures].[Reseller Order Quantity]  
       , BDESC  
       ) AS OrdPrds  
    , (OrdPrds.CurrentOrdinal < OrdPrds.Count   
       AND [Measures].[Reseller Order Quantity] =   
          ( [Measures].[Reseller Order Quantity]  
            , OrdPrds.Item  
               (OrdPrds.CurrentOrdinal  
               )  
            )  
         )  
         OR (OrdPrds.CurrentOrdinal > 1   
            AND [Measures].[Reseller Order Quantity] =   
               ([Measures].[Reseller Order Quantity]  
               , OrdPrds.Item  
                  (OrdPrds.CurrentOrdinal-2)  
                )  
             )  
          )  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
 組のセットで **DESC** フラグがどのように機能するかを理解するには、まず次のクエリの結果を検討します。  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 Rows 軸では、販売区域グループは、北米、ヨーロッパ、太平洋、NA のように、課税額の降順に並べ替えられていることがわかります。 次のように、一連の製品サブカテゴリを使用して販売区域グループのセットを crossjoin し、同じ方法で **Order** 関数を適用するとどうなるかを見てみましょう。  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC)  
ON 1  
FROM [Adventure Works]  
  
```  
  
 製品サブカテゴリのセットは階層順に降順に並べ替えられていますが、販売区域グループは、ヨーロッパ、NA、北米および太平洋の階層に表示される順序で並べ替えられずに表示されるようになりました。 これは、組のセット (製品サブカテゴリ) の最後の階層のみが並べ替えられるためです。 Analysis Services 2000 の動作を再現するには、次の例のように、入れ子になった一連の **生成** 関数を使用して、各セットをクロス結合する前に並べ替えます。  
  
```  
  
SELECT  
{[Measures].[Tax Amount]} ON 0,  
GENERATE(  
ORDER(  
[Sales Territory].[Sales Territory].[Group].MEMBERS  
,[Measures].[Tax Amount], DESC)  
,  
ORDER(  
[Sales Territory].[Sales Territory].CURRENTMEMBER  
*  
{[Product].[Product Categories].[subCategory].Members}  
,[Measures].[Tax Amount], DESC))  
ON 1  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
