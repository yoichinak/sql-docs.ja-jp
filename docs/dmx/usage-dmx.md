---
description: 使用法 (DMX)
title: 使用状況 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4e9108fc9bc53361a15d144f1f11afa62f9d5a97
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726049"
---
# <a name="usage-dmx"></a>使用法 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データマイニング拡張機能 (DMX) を使用しての新しいデータマイニングモデルを定義する場合は [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、モデルを構築するデータマイニングアルゴリズムで各列を使用する方法を指定する必要があります。 列は次の型のうちのいずれかとして指定することができます。  
  
-   **キー**  
  
-   **Key Sequence**  
  
-   **[キー時刻]**  
  
-   **将来**  
  
-   **[予測のみ]**  
  
 DMX では指定されていない列は入力列として扱われます。  
  
 モデルを正しく処理するには、各行を一意に識別するキー列はどれなのか、予測可能モデルを作成する場合に予測を作成するための対象列はどれなのか、および対象列を予測するリレーションシップを作成するために入力列として使用する列はどれなのかをアルゴリズムに理解させる必要があります。  
  
 **Predict**型として指定された列は、入力列と出力列の両方として使用されます。 **Predictonly**として指定された列は、出力列としてのみ使用されます。 特定のアルゴリズムでは、列の予測を異なる方法で扱うことができます。  
  
 でサポートされる列の使用法の種類の詳細につい [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ては、「 [マイニングモデル列](/analysis-services/data-mining/mining-model-columns)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データマイニングアルゴリズム &#40;Analysis Services-データマイニング&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [構造と DMX 予測クエリの使用](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
