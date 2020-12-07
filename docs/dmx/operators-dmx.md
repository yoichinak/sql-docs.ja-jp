---
description: 演算子 (DMX)
title: 演算子 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4c523ea9150f7d3361f93582e01b703be35d2366
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395738"
---
# <a name="operators-dmx"></a>演算子 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データマイニング拡張機能 (DMX) 演算子を使用すると、のクエリで算術、比較、連結、および論理演算を実行でき [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ます。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、次の操作を実行するために演算子が使用されます。  
  
-   特定の条件を満たす値またはオブジェクトを検索します。  
  
-   値または式の間に決定を実装します。  
  
 DMX は、次のセクションで説明するいくつかのカテゴリの演算子を使用します。 個々の演算子の詳細については、「 [データマイニング拡張機能 &#40;DMX&#41; 演算子リファレンス](../dmx/data-mining-extensions-dmx-operator-reference.md)」を参照してください。  
  
|演算子のカテゴリ|操作の種類|  
|-----------------------|-----------------------|  
|[DMX&#41;&#40;算術演算子 ](../dmx/operators-arithmetic.md)|加算、減算、乗算、除算を実行します。|  
|[DMX&#41;&#40;比較演算子 ](../dmx/operators-comparison.md)|1つの値を別の値または式と比較します。|  
|[DMX&#41;&#40;論理演算子 ](../dmx/operators-logical.md)|AND、OR、NOT などの条件の真偽をテストします。|  
|[単項演算子 &#40;DMX&#41;](../dmx/operators-unary.md)|1つのオペランドに対して操作を実行します。|  
  
 演算子を使用すると、DMX 内の小さな式を結合して、より複雑な式にすることができます。 複合式では、演算子は [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 演算子の優先順位の定義に基づいて順番に評価されます。 優先順位の高い演算子は、優先順位の低い演算子より先に実行されます。 式の詳細については、「 [DMX&#41;&#40;式 ](../dmx/expressions-dmx.md)」を参照してください。  
  
 単純な式を結合して複雑な式を作成する場合、結果として得られる式のデータ型は、演算子のルールとデータ型の優先順位のルールを組み合わせることによって決定されます。 結果が文字または Unicode 値の場合、は、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 演算子のルールと照合順序の優先順位のルールを組み合わせることによって、結果の照合順序を決定します。 また、単純式の有効桁数、小数点以下桁数、および長さに基づいて、結果の有効桁数、小数点以下桁数、および長さを決定するルールもあります。  
  
## <a name="see-also"></a>参照  
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
