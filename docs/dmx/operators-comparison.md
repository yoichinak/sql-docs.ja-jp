---
description: 比較演算子 (DMX)
title: 比較演算子 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0be897f827740a2a27ce3376df36ec0e296951b8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395808"
---
# <a name="operators---comparison"></a>演算子 - 比較
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  のデータマイニング拡張機能 (DMX) 式では、比較演算子をスカラーデータと共に使用でき [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ます。 比較演算子は、ブールデータ型に評価される。テストされた条件の結果に基づいて、TRUE または FALSE を返します。  
  
 次の表は、DMX がサポートしている比較演算子について示しています。  
  
|演算子|説明|  
|--------------|-----------------|  
|[&#60; &#40;&#41; &#40;DMX&#41;](../dmx/less-than-dmx.md)|NULL 以外の値として評価される引数では、左の引数の値が右の引数の値より小さい場合に TRUE を返します。そうでない場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[&#41; &#40;DMX&#41;より大きい&#62; &#40;](../dmx/greater-than-dmx.md)|Null 以外の値に評価される引数の場合、左の引数の値が右の引数の値より大きい場合は TRUE を返します。それ以外の場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[= &#40;&#41; &#40;DMX&#41;](../dmx/equal-to-dmx.md)|Null 以外の値に評価される引数の場合、左の引数の値が右の引数の値と等しい場合に TRUE を返します。それ以外の場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[&#60;&#62; &#40;&#41; &#40;DMX&#41;と等しくありません ](../dmx/not-equal-to-dmx.md)|Null 以外の値に評価される引数の場合、左の引数の値が右の引数の値と等しくない場合は TRUE を返します。それ以外の場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[&#60;= &#40;以下&#41; &#40;DMX&#41;](../dmx/less-than-or-equal-to-dmx.md)|NULL 以外の値として評価される引数では、左の引数の値が右の引数の値以下の場合に TRUE を返します。そうでない場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[&#62;=&#41;DMX&#41; &#40;以上 &#40;。 ](../dmx/greater-than-or-equal-to-dmx.md)|Null 以外の値に評価される引数の場合、左の引数の値が右の引数の値以上の場合は TRUE を返します。それ以外の場合は FALSE を返します。 いずれかの引数または両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
  
 また、DMX ステートメントや関数で比較演算子を使用して、条件を検索することもできます。  
  
## <a name="see-also"></a>参照  
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;&#40;式 ](../dmx/expressions-dmx.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [DMX&#41;&#40;オペレーター ](../dmx/operators-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
