---
description: '&lt;モデル &gt; 予測結合 (DMX) からの選択'
title: '&lt;モデル &gt; 予測結合 (DMX) から選択します。Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 033b610da29267cd07076c01157744441c4450d9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413298"
---
# <a name="select-from-ltmodelgt-prediction-join-dmx"></a>&lt;モデル &gt; 予測結合 (DMX) からの選択
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  では、マイニングモデルを使用して、外部データソースの列の状態を予測します。 **予測結合**ステートメントは、各ケースをソースクエリからモデルに一致させます。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <select expression list>   
FROM <model> | <sub select> [NATURAL] PREDICTION JOIN   
<source data query> [ON <join mapping list>]   
[WHERE <condition expression>]  
[ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>引数  
 *n*  
 任意。 返す行数を指定する整数値です。  
  
 *式リストの選択*  
 マイニング モデルから派生する、列の識別子と式のコンマ区切りのリストです。  
  
 *model*  
 モデル識別子。  
  
 *サブ選択*  
 埋め込みの select ステートメントです。  
  
 *source data query*  
 ソース クエリです。  
  
 *結合マッピングの一覧*  
 任意。 モデルの列をソースクエリの列と比較する論理式。  
  
 *条件式*  
 任意。 列リストから返される値を制限する条件。  
  
 *式 (expression)*  
 任意。 スカラー値を返す式。  
  
## <a name="remarks"></a>解説  
 ON 句は、ソースクエリの列とマイニングモデルの列との間のマッピングを定義します。 このマッピングは、列を入力として使用して予測を作成できるように、ソースクエリの列をマイニングモデルの列に転送するために使用されます。 内の列 \<*join mapping list*> は、次の例に示すように等号 (=) を使用して関連付けられています。  
  
```  
[MiningModel].ColumnA = [source data query].Column1 AND   
[MiningModel].ColumnB = [source data query].Column2 AND  
...  
```  
  
 入れ子になったテーブルを ON 句にバインドする場合、入れ子になった列のレコードが所属するケースをアルゴリズムが正しく識別できるように、キー列をすべての非キー列とバインドします。  
  
 予測結合のソース クエリは、テーブルまたは単一クエリのどちらかにできます。  
  
 およびでは、テーブル式を返さない予測関数を指定でき \<*select expression list*> \<*condition expression*> ます。  
  
 **自然予測結合** では、モデル内の列名に一致するソースクエリの列名が自動的にマップされます。 **自然予測**を使用する場合は、ON 句を省略できます。  
  
 WHERE 条件は、予測可能列または関連する列にのみ適用できます。  
  
 ORDER by 句では、引数として1つの列のみを使用できます。つまり、複数の列で並べ替えることはできません。  
  
## <a name="example-1-singleton-query"></a>例 1: 単一クエリ  
 次の例では、特定のユーザーがリアルタイムで自転車を購入するかどうかを予測するクエリを作成する方法を示します。 このクエリでは、データはテーブルまたはその他のデータ ソースに格納されませんが、クエリに直接入力されます。 クエリ内の人物は、次の特徴を持ちます。  
  
-   35 才  
  
-   持ち家所有  
  
-   2 台の自家用車を所有  
  
-   自宅に2人の子供がいます  
  
 このクエリでは、TM デシジョンツリーマイニングモデルと、サブジェクトに関する既知の特性を使用して、自転車を購入した人と、その予測がどのように行われたかを示す [&#40;DMX&#41;](../dmx/predicthistogram-dmx.md) 関数によって返された一連の表形式の値を示すブール値を返します。  
  
```  
SELECT  
  [TM Decision Tree].[Bike Buyer],  
  PredictHistogram([Bike Buyer])  
FROM  
  [TM Decision Tree]  
NATURAL PREDICTION JOIN  
(SELECT 35 AS [Age],  
  '5-10 Miles' AS [Commute Distance],  
  '1' AS [House Owner Flag],  
  2 AS [Number Cars Owned],  
  2 AS [Total Children]) AS t  
```  
  
## <a name="example-2-using-openquery"></a>例 2: OPENQUERY の使用  
 次の例では、外部データセットに格納されている潜在顧客の一覧を使用して、バッチ予測クエリを作成する方法を示します。 テーブルはのインスタンスで定義されているデータソースビューの一部であるため、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] クエリは [OPENQUERY](../dmx/source-data-query-openquery.md) を使用してデータを取得できます。 テーブル内の列の名前がマイニングモデルの列の名前と異なるため、テーブルの列をモデルの列にマップするには **ON** 句を使用する必要があります。  
  
 このクエリでは、テーブル内の各ユーザーの姓と名が返されます。これは、各ユーザーが自転車を購入する可能性があるかどうかを示すブール型の列と共に返されます。0は "自転車を購入しない" ことを表し、1は "自転車を購入する可能性がある" ことを意味します。 最後の列には、予測結果の確率が含まれます。  
  
```  
SELECT  
  t.[LastName],  
  t.[FirstName],  
  [TM Decision Tree].[Bike Buyer],  
  PredictProbability([Bike Buyer])  
From  
  [TM Decision Tree]  
PREDICTION JOIN  
  OPENQUERY([Adventure Works DW Multidimensional 2012],  
    'SELECT  
      [LastName],  
      [FirstName],  
      [MaritalStatus],  
      [Gender],  
      [YearlyIncome],  
      [TotalChildren],  
      [NumberChildrenAtHome],  
      [Education],  
      [Occupation],  
      [HouseOwnerFlag],  
      [NumberCarsOwned]  
    FROM  
      [dbo].[ProspectiveBuyer]  
    ') AS t  
ON  
  [TM Decision Tree].[Marital Status] = t.[MaritalStatus] AND  
  [TM Decision Tree].[Gender] = t.[Gender] AND  
  [TM Decision Tree].[Yearly Income] = t.[YearlyIncome] AND  
  [TM Decision Tree].[Total Children] = t.[TotalChildren] AND  
  [TM Decision Tree].[Number Children At Home] = t.[NumberChildrenAtHome] AND  
  [TM Decision Tree].[Education] = t.[Education] AND  
  [TM Decision Tree].[Occupation] = t.[Occupation] AND  
  [TM Decision Tree].[House Owner Flag] = t.[HouseOwnerFlag] AND  
  [TM Decision Tree].[Number Cars Owned] = t.[NumberCarsOwned]  
```  
  
 データセットを、自転車の購入を予測している顧客のみに制限し、顧客名で一覧を並べ替えるには、前の例に WHERE 句と ORDER BY 句を追加します。  
  
```  
WHERE [BIKE Buyer]  
ORDER BY [LastName] ASC  
```  
  
## <a name="example-3-predicting-associations"></a>例 3: アソシエーションの予測  
 次の例は、[!INCLUDE[msCoName](../includes/msconame-md.md)] アソシエーション アルゴリズムから作成したモデルを使用して予測を作成する方法を示します。 アソシエーションモデルの予測は、関連する製品を推奨するために使用できます。 たとえば、次のクエリでは、一緒に購入される可能性が最も高い3つの製品が返されます。  
  
-   Mountain Bottle Cage  
  
-   Mountain Tire Tube  
  
-   Mountain-200  
  
 [Predict &#40;DMX&#41;](../dmx/predict-dmx.md)関数はポリモーフィックであり、すべての種類のモデルで使用できます。 関数の引数として value3 を使用して、クエリによって返される項目の数を制限します。 自然予測結合句に続く **選択** リストでは、予測の入力として使用する値を指定します。  
  
```  
SELECT FLATTENED  
  PREDICT([Association].[v Assoc Seq Line Items], 3)  
FROM  
  [Association]  
NATURAL PREDICTION JOIN  
(SELECT (SELECT 'Mountain Bottle Cage' AS [Model]  
  UNION SELECT 'Mountain Tire Tube' AS [Model]  
  UNION SELECT 'Mountain-200' AS [Model]) AS [v Assoc Seq Line Items ]) AS t  
```  
  
 結果の例:  
  
|Expression.Model|  
|----------------------|  
|HL Mountain Tire|  
|Water Bottle|  
|Fender Set - Mountain|  
  
 予測可能な属性を含む列はテーブル列であるため、 `[v Assoc Seq Line Items]` クエリは入れ子になったテーブルを含む単一の列を返します。 既定では、入れ子になったテーブル列にはという名前が付けられ `Expression` ます。 プロバイダーが階層的な行セットをサポートしていない場合は、次の例に示すように **フラット** 化されたキーワードを使用して、結果を見やすくすることができます。  
  
## <a name="see-also"></a>参照  
 [DMX&#41;を選択 &#40;](../dmx/select-dmx.md)   
 [DMX&#41; データ定義ステートメント &#40;のデータマイニング拡張機能](../dmx/dmx-statements-data-definition.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
