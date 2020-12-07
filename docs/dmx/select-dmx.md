---
description: SELECT (DMX)
title: SELECT (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1e44c7d2f4bf872a7629a48c305114f09f98ee66
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462048"
---
# <a name="select-dmx"></a>SELECT (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データマイニング拡張機能 (DMX) の **SELECT** ステートメントは、データマイニングの次のタスクに使用されます。  
  
-   既存のマイニング モデルの内容の参照  
  
-   既存のマイニングモデルからの予測の作成  
  
-   既存のマイニングモデルのコピーの作成  
  
-   マイニング構造の参照  
  
 このステートメントの全構文は複雑なので、モデルとその基になる構造の参照に使用される主な句を次にまとめます。  
  
```  
SELECT [FLATTENED] [TOP <n>] <select list>  
FROM <model/structure>[.aspect]  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
## <a name="flattened"></a>フラット化  
 データ マイニング クライアントによっては、データ マイニング プロバイダーから階層形式の結果セットを受け取ることができない場合があります。 クライアントが階層を処理できない場合や、結果を 1 つの非正規化テーブルに格納しなければならない場合があります。 入れ子になったテーブルからフラット化テーブルにデータを変換するには、クエリの結果をフラット化するように要求する必要があります。  
  
 クエリ結果をフラット化するには、次の例に示すように、**フラット**化されたオプションで**SELECT**構文を使用します。  
  
```  
SELECT FLATTENED <select list> FROM ...  
```  
  
## <a name="top-n-and-order-by"></a>TOP \<n> と ORDER BY  
 式を使用してクエリの結果を並べ替えることができます。その後、 **ORDER by** 句と **TOP** 句の組み合わせを使用して、結果のサブセットを返すことができます。 これは、最も可能性の高い応答者にのみ結果を送信するような配信先指定メーリングなどのシナリオで役に立ちます。 予測確率によってターゲットメーリングの予測クエリの結果を並べ替え、上位の結果のみを返すことができ \<n> ます。  
  
## <a name="select-list"></a>リストの選択  
 には、 *\<select list>* スカラー列参照、予測関数、および式を含めることができます。 使用可能なオプションは、アルゴリズムと、次のコンテキストによって異なります。  
  
-   マイニング構造またはマイニングモデルに対してクエリを実行するかどうか  
  
-   コンテンツまたはケースに対してクエリを実行するかどうか  
  
-   ソース データがリレーショナル テーブルであるかキューブであるか  
  
-   予測を行う場合  
  
 多くの場合、エイリアスを使用することも、選択リストの項目に基づいて単純な式を作成することもできます。 たとえば、次の例は、モデル列の単純な式を示します。  
  
```  
SELECT [CustomerID], [Last Name] + ', ' + [FirstName] AS FullName  
FROM <model>.CASES  
```  
  
 次の例では、予測関数の結果を含む列の別名を作成します。  
  
```  
SELECT Predict([Column1], 'Value') as Column1Prediction  
FROM MyModel  
JOIN <source data query>  
```  
  
## <a name="where"></a>WHERE  
 **WHERE**句を使用すると、クエリによって返されるケースを制限できます。 Where**句は**、 **where**式の列参照が、SELECT ステートメントの内の列参照と同じセマンティクスを持つ必要があり、 *\<select list>* ブール式のみを返すことを指定し**SELECT**ます。 **Where**句の構文は次のとおりです。  
  
```  
WHERE < condition expression >  
```  
  
 **Select ステートメントの**select List および**WHERE**句は、次の規則に従う必要があります。  
  
-   選択リストには、ブール型の結果を返さない式が含まれている必要があります。 式は変更できますが、式はブール型以外の結果を返す必要があります。  
  
-   **WHERE**句には、ブール型の結果を返す式が含まれている必要があります。 この句は変更することができますが、ブール型の結果を返す必要があります。  
  
## <a name="predictions"></a>予測  
 予測の作成に使用できる構文には、次の2種類があります。  
  
-   [&#60;モデルから選択します&#62; 予測結合 &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
-   [DMX&#41;&#62; &#40;&#60;モデルから選択します ](../dmx/select-from-model-dmx.md)  
  
 前者の予測では、複雑な予測をリアルタイムで、またはバッチとして作成することができます。  
  
 2番目の予測の種類では、マイニングモデルの予測可能列に空の予測結合を作成し、列の最も可能性の高い状態を返します。 このクエリの結果は、マイニングモデルの内容に完全に基づいています。  
  
 次の構文を使用して、select FROM 予測結合ステートメントのソースクエリに select ステートメントを挿入できます。  
  
```  
SELECT FROM PREDICTION JOIN (<SELECT statement>) AS t, WHERE <SELECT statement>  
```  
  
 予測クエリの作成の詳細については、「 [構造と DMX 予測クエリの使用方法](../dmx/structure-and-usage-of-dmx-prediction-queries.md)」を参照してください。  
  
## <a name="clause-syntax"></a>句の構文  
 **SELECT**ステートメントを使用した参照は複雑であるため、構文の詳細な要素と引数は句によって記述されています。 各句の詳細については、次の一覧のトピックをクリックしてください。  
  
 [DMX&#41;&#62; &#40;&#60;モデルから [DISTINCT] を選択します。 ](../dmx/select-distinct-from-model-dmx.md)  
  
 [&#60;モデル&#62; から選択します。DMX&#41;のコンテンツ &#40;](../dmx/select-from-model-content-dmx.md)  
  
 [&#60;モデル&#62; から選択します。DMX&#41;&#40;ケース ](../dmx/select-from-model-cases-dmx.md)  
  
 [&#60;モデル&#62; から選択します。DMX&#41;&#40;の SAMPLE_CASES ](../dmx/select-from-model-sample-cases-dmx.md)  
  
 [&#60;モデル&#62; から選択します。DMX&#41;&#40;の DIMENSION_CONTENT ](../dmx/select-from-model-dimension-content-dmx.md)  
  
 [&#60;モデルから選択します&#62; 予測結合 &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md)  
  
 [DMX&#41;&#62; &#40;&#60;モデルから選択します ](../dmx/select-from-model-dmx.md)  
  
 [&#60;構造&#62; から選択します。場合](../dmx/select-from-structure-cases.md)  
  
## <a name="see-also"></a>参照  
 [DMX&#41; データ定義ステートメント &#40;のデータマイニング拡張機能](../dmx/dmx-statements-data-definition.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [DMX&#41; ステートメントリファレンス &#40;データマイニング拡張機能](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)  
  
  
