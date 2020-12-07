---
description: モデリング フラグ (DMX)
title: モデリングフラグ (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 968b1c10f8eb054f6527253bd358e97eaa396637
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727723"
---
# <a name="modeling-flags-dmx"></a>モデリング フラグ (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のモデリング フラグを使用すると、ケース テーブルで定義されているデータに関する追加情報をデータ マイニング アルゴリズムに提供できます。 アルゴリズムは、この情報を使用して、より正確なデータ マイニング モデルを作成することができます。 モデリングフラグは、マイニング構造列とマイニングモデル列の両方に定義できます。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、次のモデリングフラグがサポートされています。  
  
 **NOT NULL**  
 属性列の値に null 値を含めることはできません。 モデルの学習プロセス中に、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] がこの属性列に NULL 値を検出した場合、エラーが発生します。 このフラグは、マイニング構造列に対して定義されています。  
  
 **リグレッサー**  
 アルゴリズムが、指定した列を回帰アルゴリズムの回帰式に使用できることを示します。 このフラグは、[!INCLUDE[msCoName](../includes/msconame-md.md)] Linear Regression および [!INCLUDE[msCoName](../includes/msconame-md.md)] Decision Trees アルゴリズムによってサポートされており、マイニング モデル列で定義されます。  
  
 **MODEL_EXISTENCE_ONLY**  
 この属性列の値は、属性の有無ほど重要ではありません。 このフラグはマイニング モデル列で定義されます。  
  
 サード パーティのアルゴリズムによっては、別のモデリング フラグもサポートしている場合があります。 アルゴリズムでサポートされているモデリングフラグを確認するには、 **SUPPORTED_MODELING_FLAGS** スキーマ行セットを使用します。 また、サーバーのマイニング サービスに対してクエリを実行し、特定のアルゴリズムでサポートされているモデリング フラグを判別することもできます。 たとえば、次のクエリでは、現在のサーバー上の Microsoft 線形回帰アルゴリズムでサポートされているモデリング フラグが返されます。  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 期待される結果:  
  
 NOT NULL、REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>マイニングモデルでのモデリングフラグの指定  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]マイニング構造列にフラグを指定するためにがサポートする構文の例については、「 [DMX&#41;&#40;マイニング構造を作成](../dmx/create-mining-structure-dmx.md)する」を参照してください。  
  
 マイニングモデル列でのモデリングフラグを指定する構文の例については、「 [ALTER マイニング STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md)」を参照してください。  
  
 マイニングモデル列の操作の詳細については、「 [マイニングモデル列](/analysis-services/data-mining/mining-model-columns)」を参照してください。  
  
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
  
