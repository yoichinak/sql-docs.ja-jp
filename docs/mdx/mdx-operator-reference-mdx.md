---
description: MDX 演算子リファレンス (MDX)
title: MDX 演算子リファレンス (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c6fe11ee3022c07560435b13a72273962ba6a4b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429774"
---
# <a name="mdx-operator-reference-mdx"></a>MDX 演算子リファレンス (MDX)


  多次元式 (MDX) 言語では、算術演算子、論理演算子、比較演算子、セット、文字列、および単項演算子がサポートされています。 次の表に、サポートされている演算子とその説明を示します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[-- &#40;コメント&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md)|ユーザーによって指定されたコメントテキストを示します。|  
|[-&#41; &#40;MDX&#41;を除く &#40;](../mdx/except-mdx-operator.md)|2 つのセットの重複メンバーを削除して差集合を返すセット演算を実行します。|  
|[-&#40;負の&#41; &#40;MDX&#41;](../mdx/negative-mdx.md)|数値式の負の値を返す単項演算を実行します。|  
|[-&#40;&#41; &#40;MDX&#41;を減算する ](../mdx/subtract-mdx.md)|ある数値を別の数値から減算する算術演算を実行します。|  
|[&#42; &#40;Crossjoin&#41; &#40;MDX&#41;](../mdx/crossjoin-mdx-operator-reference.md)|2つのセットのクロス積を返すセット演算を実行します。|  
|[&#41; &#40;MDX&#41;を乗算&#42; &#40;](../mdx/multiply-mdx.md)|2つの数値を乗算する算術演算を実行します。|  
|[ MDX&#41;&#41; &#40;分割&#40;](../mdx/divide-mdx-operator-reference.md)|1つの数値を別の数値で除算する算術演算を実行します。|  
|[^ &#40;Power&#41; &#40;MDX&#41;](../mdx/power-mdx.md)|1つの数値を別の数値で累乗した算術演算を実行します。|  
|[コメント &#40;MDX&#41;](../mdx/comment-mdx.md)|ユーザーによって指定されたコメントテキストを示します。|  
|[(コメント) (MDX)](../mdx/comment-mdx-double-slash.md)|ユーザーが入力したテキストを示します。|  
|[: &#40;範囲&#41; &#40;MDX&#41;](../mdx/range-mdx.md)|自然な順序で並べたセットを返すセット演算を実行します。指定された 2 つのメンバーが終端になり、その 2 つのメンバーの間にあるすべてのメンバーがセットのメンバーに含まれます。|  
|[+ &#40;&#41; &#40;MDX&#41;を追加する ](../mdx/add-mdx.md)|2つの数値を加算する算術演算を実行します。|  
|[+ &#40;肯定的&#41; &#40;MDX&#41;](../mdx/positive-mdx.md)|数値式の正の値を返す単項演算を実行します。|  
|[+ &#40;文字列連結&#41; &#40;MDX&#41;](../mdx/string-concatenation-mdx.md)|2 つ以上の文字列、組、または文字列と組の組み合わせを連結する文字列演算を実行します。|  
|[+ &#40;Union&#41; &#40;MDX&#41;](../mdx/union-mdx-operator-reference.md)|2つのセットの和集合を返すセット演算を実行し、重複部分を削除します。|  
|[&#60; &#40;未満&#41; &#40;MDX&#41;](../mdx/less-than-mdx.md)|1 つの MDX 式の値が別の MDX 式の値よりも小さいかどうかを判別する比較演算を実行します。|  
|[&#60;= &#40;&#41; &#40;以下の MDX&#41;](../mdx/less-than-or-equal-to-mdx.md)|1つの MDX 式の値が別の MDX 式の値以下かどうかを判断する比較演算を実行します。|  
|[&#60;&#62; &#40;&#41; &#40;MDX&#41;と等しくありません ](../mdx/not-equal-to-mdx.md)|1つの MDX 式の値が別の MDX 式の値と等しくないかどうかを判断する比較演算を実行します。|  
|[=&#41; &#40;MDX&#41;に等しい &#40;](../mdx/equal-to-mdx.md)|1つの MDX 式の値が別の MDX 式の値と等しいかどうかを判断する比較演算を実行します。|  
|[&#62; &#40;より大きい&#41; &#40;MDX&#41;](../mdx/greater-than-mdx.md)|1つの MDX 式の値が別の MDX 式の値より大きいかどうかを判断する比較演算を実行します。|  
|[&#62;= &#40;以上&#41; &#40;MDX&#41;](../mdx/greater-than-or-equal-to-mdx.md)|1 つの MDX 式の値が別の MDX 式の値以上であるかどうかを判別する比較演算を実行します。|  
|[および &#40;MDX&#41;](../mdx/and-mdx.md)|2つの数値式の論理積を実行します。|  
|[MDX&#41;&#40;](../mdx/is-mdx.md)|2つのオブジェクト式の論理比較を実行します。|  
|[MDX&#41;&#40;ません ](../mdx/not-mdx.md)|数値式の論理否定を実行します。|  
|[または &#40;MDX&#41;](../mdx/or-mdx.md)|2つの数値式の論理和を実行します。|  
|[XOR &#40;MDX&#41;](../mdx/xor-mdx.md)|2つの数値式に対して論理的な除外を実行します。|  
  
## <a name="see-also"></a>参照  
 [MDX 言語リファレンス &#40;MDX&#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
