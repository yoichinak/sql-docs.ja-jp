---
description: 分布 (DMX)
title: ディストリビューション (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9deb3afaa6d0a4bc90281c2cc3998365eccb9838
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726223"
---
# <a name="distributions-dmx"></a>分布 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  では、マイニング [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] モデルの作成時にアルゴリズムがこれらの列のデータを処理する方法に影響を与えるように、マイニング構造の列のコンテンツを定義できます。 いくつかのアルゴリズムは、列が値の一般的な分布を含むことが認識された場合、モデルを処理する前にすべての連続列の分布を定義するために使用されます。 分布が定義されない場合、アルゴリズムが持つデータを解釈するための情報が少ないため、分布が定義されたときよりも、マイニング モデルの結果が実際の予測より小さくなる場合があります。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] データマイニングアルゴリズムでは、次の分布の種類がサポートされています。  
  
 **通常**  
 連続列の値は、正規のガウス分布のヒストグラムを形成します。  
  
 **Log Normal**  
 連続列の値は、値の対数が正規分布であるヒストグラムを形成します。  
  
 **単色**  
 連続列の値はフラット曲線を形成し、すべての値が等しくなります。  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)]データマイニングアルゴリズムの詳細については、「データマイニング[アルゴリズム &#40;Analysis Services データマイニング&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)」を参照してください。 サードパーティのアルゴリズム プロバイダーは、追加の分布の種類をサポートしている場合があります。 アルゴリズムでサポートされている分布の種類を確認するには、 **SUPPORTED_DISTRIBUTION_FLAGS** スキーマ行セットを使用します。  
  
 分布の種類の詳細については、「 [列の分布 &#40;データマイニング&#41;](/analysis-services/data-mining/column-distributions-data-mining)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [コンテンツの種類 &#40;データマイニング&#41;](/analysis-services/data-mining/content-types-data-mining)   
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
