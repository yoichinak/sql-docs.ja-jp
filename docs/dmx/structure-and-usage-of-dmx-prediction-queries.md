---
description: 構造と DMX 予測クエリの使用
title: 構造と DMX 予測クエリの使用方法 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 242e86a0ac74dacd8682825f25adab4a847a82e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500781"
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>構造と DMX 予測クエリの使用
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  で [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] は、データマイニング拡張機能 (DMX) の予測クエリを使用して、マイニングモデルの結果に基づいて、新しいデータセット内の不明な列の値を予測できます。  
  
 使用するクエリの型は、モデルから取得する情報の種類によって異なります。 リアルタイムで簡単な予測を作成する場合、たとえば、Web サイトの潜在顧客が自転車購入者のペルソナに適合するかどうかを知るには、単一クエリを使用します。 データ ソース内に含まれているケースのセットから予測のバッチを作成する場合は、通常の予測クエリを使用します。  
  
## <a name="prediction-types"></a>予測の種類  
 DMX を使用すると、次の種類の予測を作成できます。  
  
 Prediction join  
 マイニング モデル内に存在するパターンに基づいて、入力データに対する予測を作成するのに使用します。 このクエリステートメント **の後に** 、マイニングモデル列と入力列の間の結合条件を指定する ON 句を指定する必要があります。  
  
 自然予測結合  
 クエリを実行するテーブル内の列の名前と正確に一致する、マイニング モデル内の列の名前に基づいた予測を作成するのに使用します。 このクエリステートメントでは、マイニングモデル列と入力列の間で一致する名前に基づいて結合条件が自動的に生成されるため、 **ON** 句は必要ありません。  
  
 Empty prediction join  
 入力データを提供することなく、最も可能性の高い予測を検出するには、を使用します。 これにより、マイニングモデルのコンテンツのみに基づく予測が返されます。  
  
 Singleton query  
 データをクエリに供給することで予測を作成する場合に使用します。 このステートメントは、1 つのケースをクエリに供給することで結果をすばやく得ることができるため便利です。 たとえば、クエリを使用して、女性、年齢35、および既婚者が自転車を購入する可能性があるかどうかを予測できます。 このクエリでは、外部データソースは必要ありません。  
  
## <a name="query-structure"></a>クエリ構造  
 DMX で予測クエリを作成するには、次の要素の組み合わせを使用します。  
  
-   **選択 [フラット化]**  
  
-   **TOP**  
  
-   **FROM** *\<model>***予測結合**      
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDER BY**  
  
 予測クエリの **SELECT** 要素では、結果セットに表示される列と式を定義します。次のデータを含めることができます。  
  
-   マイニングモデルの列を**予測**または**predictonly**します。  
  
-   予測の作成に使用される入力データの任意の列。  
  
-   データ列を返す関数。  
  
 **FROM** *\<model>* **予測結合**要素は、予測の作成に使用するソースデータを定義します。 単一クエリの場合、これは列に割り当てられる一連の値です。 空の予測結合の場合は、空のままとなります。  
  
 **ON**要素は、マイニングモデルで定義されている列を外部データセットの列にマップします。 空の予測結合クエリまたは自然予測結合を作成する場合は、この要素を含める必要はありません。  
  
 **WHERE**句を使用して、予測クエリの結果をフィルター処理できます。 **TOP**句または**order by**句を使用して、最も可能性の高い予測を選択できます。 これらの句の使用方法の詳細については、「 [SELECT &#40;DMX&#41;](../dmx/select-dmx.md)」を参照してください。  
  
 予測ステートメントの構文の詳細については、「 [select FROM &#60;model&#62; の予測結合 &#40;dmx&#41;](../dmx/select-from-model-prediction-join-dmx.md) 」と「 [select from &#60;model&#62; &#40;dmx&#41;](../dmx/select-from-model-dmx.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [DMX&#41; リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; 関数リファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [DMX&#41; オペレーターリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; 構文表記規則を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [DMX&#41; の構文要素を &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [DMX&#41;&#40;一般的な予測関数 ](../dmx/general-prediction-functions-dmx.md)   
 [DMX 選択ステートメントについて](../dmx/understanding-the-dmx-select-statement.md)  
  
  
