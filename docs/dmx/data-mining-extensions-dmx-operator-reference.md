---
description: データマイニング拡張機能 (DMX) 演算子リファレンス
title: データマイニング拡張機能 (DMX) 演算子リファレンス |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ba8f03b86a93122b2dcd9b825adc656feae80cd2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414298"
---
# <a name="data-mining-extensions-dmx-operator-reference"></a>データマイニング拡張機能 (DMX) 演算子リファレンス
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  のデータマイニング拡張機能 (DMX) 言語では [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、算術演算子、代入演算子、比較演算子、論理演算子、および単項演算子がサポートされています。 次の表に、DMX でサポートされる演算子を示します。  
  
|演算子|説明|  
|--------------|-----------------|  
|[+ &#40;&#41; &#40;DMX&#41;を追加する ](../dmx/add-dmx.md)|2つの数値を加算する算術演算子。|  
|[-&#40;&#41; &#40;DMX&#41;を減算する ](../dmx/subtract-dmx.md)|ある数値を別の数値から減算する算術演算子。|  
|[&#41; &#40;DMX&#41;を乗算&#42; &#40;](../dmx/multiply-dmx.md)|ある数値を別の数値によって乗算する算術演算子です。|  
|[ DMX&#41;&#41; &#40;分割&#40;](../dmx/divide-dmx.md)|1つの数値を別の数値で除算する算術演算子。|  
|[&#60; &#40;&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|比較演算子。 Null 以外の値に評価される引数の場合、左の引数の値が右の引数の値より小さい場合は TRUE を返します。それ以外の場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[&#41; &#40;DMX&#41;より大きい&#62; &#40;](../dmx/greater-than-dmx.md)|比較演算子。 Null 以外の値に評価される引数の場合、左の引数の値が右の引数の値より大きい場合は TRUE を返します。それ以外の場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[= &#40;&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|比較演算子。 Null 以外の値に評価される引数では、左の引数の値が右側の引数の値と等しい場合に TRUE を返します。それ以外の場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[&#60;&#62; &#40;&#41; &#40;DMX&#41;と等しくありません ](../dmx/not-equal-to-dmx.md)|比較演算子。 Null 以外の値に評価される引数の場合、左の引数の値が右の引数の値と等しくない場合は TRUE を返します。それ以外の場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[&#60;= &#40;以下&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|比較演算子。 Null 以外の値に評価される引数の場合、左の引数の値が右の引数の値以下である場合は TRUE を返します。それ以外の場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[&#62;=&#41;DMX&#41; &#40;以上 &#40;。 ](../dmx/greater-than-or-equal-to-dmx.md)|比較演算子。 NULL 以外の値として評価される引数では、左の引数の値が右の引数の値以上の場合に TRUE を返します。そうでない場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[および &#40;DMX&#41;](../dmx/and-dmx.md)|2つの数値式の組み合わせを実行する論理演算子です。|  
|[DMX&#41;&#40;ません ](../dmx/not-dmx.md)|数値式で否定を実行する論理演算子です。|  
|[または &#40;DMX&#41;](../dmx/or-dmx.md)|2つの数値式の和を実行する論理演算子。|  
|[+ &#40;正の&#41; &#40;DMX&#41;](../dmx/positive-dmx.md)|数値式の正の値を返す単項演算子です。|  
|[-&#40;負の&#41; &#40;DMX&#41;](../dmx/negative-dmx.md)|数値式の負の値を返す単項演算子。|  
|[DMX&#41;&#41; &#40;スラッシュ &#40;コメント ](../dmx/double-slash-comment-dmx.md)|実行しないテキスト文字列を示し [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ます。 コメントは、DMX ステートメント内で入れ子にしたり、コード行の末尾に含めたり、別の行に挿入したりすることができます。|  
|[--&#40;コメント&#41; &#40;DMX&#41; の概要](../dmx/comment-dmx-summary.md)|実行しないテキスト文字列を示し [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ます。 コメントは、DMX ステートメント内で入れ子にしたり、コード行の末尾に含めたり、別の行に挿入したりすることができます。|  
|[DMX&#41;&#41; &#40;スラッシュの星 &#40;コメント ](../dmx/slash-star-comment-dmx.md)|実行しないテキスト文字列を示し [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ます。 コメントは、DMX ステートメント内で入れ子にしたり、コード行の末尾に含めたり、別の行に挿入したりすることができます。|  
  
## <a name="see-also"></a>参照  
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;&#40;オペレーター ](../dmx/operators-dmx.md)  
  
  
