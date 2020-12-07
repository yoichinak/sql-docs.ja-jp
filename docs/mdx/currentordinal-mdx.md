---
description: CurrentOrdinal (MDX)
title: CurrentOrdinal (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 68119266fd9460a28e036914fce036ec165e553a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413158"
---
# <a name="currentordinal-mdx"></a>CurrentOrdinal (MDX)


  反復処理中に、セット内の現在のイテレーション数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set_Expression.CurrentOrdinal  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 [Filter (mdx)](../mdx/filter-mdx.md)関数や[Generate (mdx)](../mdx/generate-mdx.md)関数などを使用してセットを反復処理する場合、 **currentordinal**関数はイテレーション番号を返します。  
  
## <a name="examples"></a>例  
 次の簡単な例では、 **Currentordinal** を **Generate** と共に使用して、セット内の各項目の名前とセット内の位置を含む文字列を返す方法を示しています。  
  
 `WITH SET MySet AS [Customer].[Customer Geography].[Country].MEMBERS`  
  
 `MEMBER MEASURES.CURRENTORDINALDEMO AS`  
  
 `GENERATE(MySet, CSTR(MySet.CURRENTORDINAL) + ") " + MySet.CURRENT.ITEM(0).NAME, ", ")`  
  
 `SELECT MEASURES.CURRENTORDINALDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
 CurrentOrdinal の実際の使用は、非常に複雑な計算に限定されます。 次の例では、**フィルター**関数を使用する前に、 **order**関数を使用して空でない組を並べ替える、セット内の一意の製品の数を返します。 **Currentordinal**関数は、結合を比較し、削除するために使用されます。  
  
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
    , NOT((OrdPrds.CurrentOrdinal < OrdPrds.Count   
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
          ))  
       )  
SELECT {[Measures].[PrdTies]} ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
