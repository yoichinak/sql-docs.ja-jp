---
description: NonEmptyCrossjoin (MDX)
title: NonEmptyCrossjoin (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6fafaad2f6fa0f46d826bf94b26ceb6fdbe9df55
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471804"
---
# <a name="nonemptycrossjoin-mdx"></a>NonEmptyCrossjoin (MDX)


  1 つ以上のセットのクロス積を含むセットを返します。ただし、空の組と、ファクト テーブル データに関連付けられていない組は含まれません。  
  
## <a name="syntax"></a>構文  
  
```  
  
NonEmptyCrossjoin(Set_Expression1 [ ,Set_Expression2,...] [,Count ] )  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Count*  
 返されるセットの数を指定する有効な数値式です。  
  
## <a name="remarks"></a>解説  
 **NonEmptyCrossjoin**関数は、2つ以上のセットのクロス積をセットとして返します。これは、基になるファクトテーブルによって提供されるデータを含まない空の組または組を除外したものです。 **NonEmptyCrossjoin**関数の動作により、計算されるメンバーはすべて自動的に除外されます。  
  
 *Count*が指定されていない場合、関数は指定されたすべてのセットを結合し、結果セットから空のメンバーを除外します。 複数のセットが指定されている場合、関数は指定されたセットの数を1つ前に指定されたセットから結合します。 **NonEmptyCrossjoin**関数は、後続の指定されたセットに指定されている残りのセットを使用しますが、クロス結合されていない場合は、結果のクロス結合セットで空でないと見なされるメンバーを決定します。 **NonEmptyCrossjoin**関数は、計算されるメジャーの**NON_EMPTY_BEHAVIOR**設定を尊重します。  
  
> [!IMPORTANT]  
>  この関数は旧バージョンとの互換性を維持するために用意されており、非推奨とされます。 代わりに、 [Exists (mdx)](../mdx/exists-mdx.md) 関数をメジャーグループ名引数または空でない [(mdx)](../mdx/nonempty-mdx.md) 関数と共に使用する必要があります。  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
