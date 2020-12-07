---
description: IS (MDX)
title: IS (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eab5fc86d89fccbe6ae56c4dba78ccde60e26d50
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387348"
---
# <a name="is-mdx"></a>IS (MDX)


  2つのオブジェクト式の論理比較を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Expression1 IS ( Expression2 | NULL )  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Expression1*  
 MDX オブジェクト参照を返す有効な多次元式 (MDX) 式です。  
  
 *Expression2*  
 MDX オブジェクト参照を返す有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 両方の引数が同じオブジェクトを参照する場合に **true** を返すブール値です。それ以外の場合は **false**。 **Null**キーワードが指定されている場合、演算子は、 *Expression1*が**null**の場合に**true**を返します。それ以外の場合は**false**。  
  
## <a name="remarks"></a>解説  
 **Is**演算子は、組とメンバーが等しいかどうかを判断するためによく使用されます。これは、厳密に等価であることを意味します。  
  
## <a name="examples"></a>例  
 次の例で **は、is** 演算子を使用して、軸上の現在のメンバーが特定のメンバーであるかどうかを確認する方法を示します。  
  
 `With`  
  
 `//Returns TRUE if the currentmember is Bikes`  
  
 `Member [Measures].[IsBikes?] AS`  
  
 `[Product].[Category].CurrentMember IS [Product].[Category].&[1]`  
  
 `SELECT`  
  
 `{[Measures].[IsBikes?]} ON 0,`  
  
 `[Product].[Category].[Category].Members ON 1`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [Mdx 演算子リファレンス &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
