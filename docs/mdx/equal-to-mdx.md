---
description: = (等しい) (MDX)
title: = (等しい) (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5ec3cbcb928926d02dd6597116f8ce9af00bf8e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494935"
---
# <a name="-equal-to-mdx"></a>= (等しい) (MDX)


  1 つの多次元式 (MDX) 式の値が、別の MDX 式の値と等しいかどうかを判別する比較演算を実行します。  
  
> [!NOTE]  
>  オブジェクトを比較するに [は、is &#40;MDX&#41;](../mdx/is-mdx.md) 演算子を使用します。 たとえば、クエリ軸の現在のメンバーが特定のメンバーであるかどうかを確認する場合は、IS 演算子を使用します。  
  
## <a name="syntax"></a>構文  
  
```  
  
MDX_Expression = MDX_Expression   
```  
  
#### <a name="parameters"></a>パラメーター  
 *MDX_Expression*  
 有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 次の条件に基づくブール値。  
  
-   最初のパラメーターの値が2番目のパラメーターの値と等しい場合は**true** 。  
  
-   最初のパラメーターの値が2番目のパラメーターの値と等しくない場合は**false** 。  
  
-   両方のパラメーターが null の場合、または1つのパラメーターが null で、もう一方のパラメーターが0の場合は**true** 。  
  
## <a name="examples"></a>例  
 次のクエリは、これらの条件の例を示しています。  
  
 `With`  
  
 `--Returns true`  
  
 `Member [Measures].bool1 as 1=1`  
  
 `--Returns false`  
  
 `Member [Measures].bool2 as 1=0`  
  
 `--Returns true`  
  
 `Member [Measures].bool3 as null=null`  
  
 `--Returns true`  
  
 `Member [Measures].bool4 as 0=null`  
  
 `--Returns false`  
  
 `Member [Measures].bool5 as 1=null`  
  
 `Select {[Measures].bool1,[Measures].bool2,[Measures].bool3,[Measures].bool4,[Measures].bool5}`  
  
 `On 0`  
  
 `From [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [Mdx 演算子リファレンス &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
