---
description: Ascendants (MDX)
title: 先祖 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb485e2785facba4a47647f8a51548e0140b3efb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491468"
---
# <a name="ascendants-mdx"></a>Ascendants (MDX)


  指定されたメンバー自体も含めたメンバーの先祖のセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Ascendants(Member_Expression)  
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **先祖**関数は、メンバーの階層の最上位にあるメンバーの先祖をすべて返します。具体的には、指定されたメンバーの階層のポスト順序走査を実行し、そのメンバーに関連するすべての先祖メンバー (それ自体を含む) を set で返します。 これは、特定のレベルで特定の先祖メンバー (先祖) を返す [先祖](../mdx/ancestor-mdx.md) 関数とは対照的です。  
  
## <a name="examples"></a>例  
 次の例では、Adventure Works キューブから、メンバーの再販業者の注文数 `[Sales Territory].[Northwest]` と、その**Adventure Works**メンバーのすべての先祖を返します。 **先祖**関数は、 `[Sales Territory].[Northwest]` ROWS 軸のメンバーとその先祖を含むセットを構築します。  
  
```  
SELECT  
   Measures.[Reseller Order Count] ON COLUMNS,  
   Order(  
      Ascendants(  
         [Sales Territory].[Northwest]  
      ),  
      DESC  
   ) ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
