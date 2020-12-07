---
description: '[モデルから] を選択し &lt; &gt; ます。コンテンツ (DMX)'
title: '[モデルから] を選択し &lt; &gt; ます。コンテンツ (DMX) |Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: df70a8726e9abc56d677c48ba8f3f995814866d4
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727643"
---
# <a name="select-from-ltmodelgtcontent-dmx"></a>[モデルから] を選択し &lt; &gt; ます。コンテンツ (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  指定されたデータマイニングモデルのマイニングモデルスキーマ行セットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.CONTENT   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 省略可能。 返す行数を指定する整数値です。  
  
 *式の一覧*  
 コンテンツスキーマ行セットから派生した列のコンマ区切りのリスト。  
  
 *model*  
 モデル識別子。  
  
 *条件式*  
 省略可能。 列リストから返される値を制限する条件。  
  
 *式 (expression)*  
 省略可能。 スカラー値を返す式。  
  
## <a name="remarks"></a>解説  
 **SELECT FROM** _\<model>_ **です。CONTENT**ステートメントでは、各アルゴリズムに固有のコンテンツが返されます。 たとえば、カスタムアプリケーションでのアソシエーションルールモデルのすべてのルールの説明を使用することができます。 SELECT FROM を使用でき ** \<model> ます。** モデルの NODE_RULE 列の値を返すコンテンツステートメント。  
  
 次の表に、マイニングモデルコンテンツに含まれる列を示します。  
  
> [!NOTE]  
>  アルゴリズムでは、コンテンツを正しく表現するために、列の解釈が異なる場合があります。 各アルゴリズムのマイニングモデルコンテンツの説明、および各種類のモデルのマイニングモデルコンテンツの解釈とクエリの方法に関するヒントについては、「 [マイニングモデルコンテンツ &#40;Analysis Services-データマイニング&#41;](/analysis-services/data-mining/mining-model-content-analysis-services-data-mining)」を参照してください。  
  
|コンテンツ行セット列|説明|  
|---------------------------|-----------------|  
|MODEL_CATALOG|カタログ名です。 プロバイダーがカタログをサポートしない場合は NULL です。|  
|MODEL_SCHEMA|非修飾スキーマ名。 プロバイダーがスキーマをサポートしない場合は NULL です。|  
|MODEL_NAME|モデル名。 この列に NULL を含むことはできません。|  
|ATTRIBUTE_NAME|ノードに対応する属性の名前です。|  
|NODE_NAME|ノード名。|  
|NODE_UNIQUE_NAME|モデル内のノードの一意の名前。|  
|NODE_TYPE|ノードの種類を表す整数です。 .|  
|NODE_GUID|ノードの GUID。 GUID がない場合は NULL です。|  
|NODE_CAPTION|ノードに関連付けられているラベルまはたキャプションです。 主に表示目的で使用されます。 キャプションが存在しない場合は NODE_NAME が返されます。|  
|CHILDREN_CARDINALITY|ノードが持つ子の数です。|  
|PARENT_UNIQUE_NAME|ノードの親の一意な名前です。|  
|NODE_DESCRIPTION|ノードの説明です。|  
|NODE_RULE|ノードに埋め込まれたルールを表す XML フラグメントです。 XML 文字列の形式は、PMML 標準に基づいています。|  
|MARGINAL_RULE|親からノードまでのパスを記述する XML フラグメント。|  
|NODE_PROBABILITY|パスの末尾がノードになる確率です。|  
|MARGINAL_PROBABILITY|親ノードからノードに到達する確率です。|  
|NODE_DISTRIBUTION|ノード内の値の分布を表す統計を含むテーブル。|  
|NODE_SUPPORT|このノードがサポートされているケースの数。|  
  
## <a name="examples"></a>例  
 次のコードは、対象メーリングマイニング構造に追加されたデシジョンツリーモデルの親ノードの ID を返します。  
  
```  
SELECT MODEL_NAME, NODE_NAME FROM [TM Decision Tree].CONTENT  
WHERE NODE_TYPE = 1  
```  
  
 期待される結果:  
  
|MODEL_NAME|NODE_NAME|  
|-----------------|----------------|  
|TM_DecisionTree|0|  
  
 次のクエリでは、 **Isdescendant** 関数を使用して、前のクエリで返されたノードの直下の子を返します。  
  
> [!NOTE]  
>  NODE_NAME の値は文字列であるため、サブ select ステートメントを使用して、 **Isdescendant** 関数の引数として NODE_ID を返すことはできません。  
  
```  
SELECT NODE_NAME, NODETYPE, NODE_CAPTION   
FROM [TM Decision Tree].CONTENT  
WHERE ISDESCENDANT('0')  
```  
  
 期待される結果:  
  
 モデルはデシジョンツリーモデルであるため、モデルの親ノードの子孫には、1つの限界の統計ノード、予測可能な属性を表すノード、入力属性と値を含む複数のノードが含まれます。 詳細については、「 [デシジョン ツリー モデルのマイニング モデル コンテンツ &#40;Analysis Services - データ マイニング&#41;](/analysis-services/data-mining/mining-model-content-for-decision-tree-models-analysis-services-data-mining)」を参照してください。  
  
## <a name="using-the-flattened-keyword"></a>FLATTENED キーワードの使用  
 多くの場合、マイニング モデル コンテンツには、入れ子になったテーブル列のモデルに関する有用な情報が含まれています。 フラット化されたキーワードを使用すると、階層的な行セットをサポートするプロバイダーを使用せずに、入れ子になったテーブルの列からデータを取得できます。  
  
 次のクエリでは、Naive Bayes モデルからマージナル統計ノード (NODE_TYPE = 26) という 1 つのノードが返されます。 ただし、このノードには、入れ子になったテーブルが NODE_DISTRIBUTION 列に含まれています。 その結果、入れ子になったテーブル列がフラット化され、入れ子になったテーブルの行ごとに 1 つの行が返されます。 スカラー列 MODEL_NAME の値は、入れ子になったテーブルの各行に繰り返し表示されます。  
  
 また、入れ子になったテーブル列の名前のみを指定すると、入れ子になったテーブルの各列に対して新しい列が返されることにも注意してください。 既定では、入れ子になったテーブルの名前が、入れ子になったテーブル列それぞれの名前の先頭に含まれます。  
  
```  
SELECT FLATTENED MODEL_NAME, NODE_DISTRIBUTION  
FROM [TM_NaiveBayes].CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 結果の例:  
  
|MODEL_NAME|NODE_DISTRIBUTION.ATTRIBUTE_NAME|NODE_DISTRIBUTION。ATTRIBUTE_VALUE|NODE_DISTRIBUTION.SUPPORT|NODE_DISTRIBUTION。確率|NODE_DISTRIBUTION.VARIANCE|NODE_DISTRIBUTION.VALUETYPE|  
|-----------------|----------------------------------------|-----------------------------------------|--------------------------------|------------------------------------|---------------------------------|----------------------------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|0|0|1|  
|TM_NaiveBayes|Bike Buyer|0|6556|0.506685215240745|0||  
|TM_NaiveBayes|Bike Buyer|1|6383|0.493314784759255|0||  
  
 次の例は、下位選択ステートメントを使用して、入れ子になったテーブルから一部の列のみを返す方法を示しています。 表示を簡略化するには、入れ子になったテーブルのテーブル名を別名で示します。  
  
```  
SELECT MODEL_NAME,   
(SELECT ATTRIBUTE_NAME, ATTRIBUTE_VALUE, [SUPPORT] AS t  
FROM NODE_DISTRIBUTION)   
FROM TM_NaiveBayes.CONTENT  
WHERE NODE_TYPE = 26  
```  
  
 結果の例:  
  
|MODEL_NAME|T.ATTRIBUTE_NAME|t.ATTRIBUTE_VALUE|t.SUPPORT|  
|-----------------|-----------------------|------------------------|---------------|  
|TM_NaiveBayes|Bike Buyer|Missing|0|  
|TM_NaiveBayes|Bike Buyer|0|6556|  
|TM_NaiveBayes|Bike Buyer|1|6383|  
  
## <a name="see-also"></a>参照  
 [DMX&#41;を選択 &#40;](../dmx/select-dmx.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
