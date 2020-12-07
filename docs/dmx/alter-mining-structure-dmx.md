---
description: ALTER MINING STRUCTURE (DMX)
title: ALTER マイニング構造 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6169d898479637d8f8c0a74aececd56cf1f62eb7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727813"
---
# <a name="alter-mining-structure-dmx"></a>ALTER MINING STRUCTURE (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  既存のマイニング構造に基づく新しいマイニングモデルを作成します。  **ALTER マイニング structure**ステートメントを使用して新しいマイニングモデルを作成する場合は、構造が既に存在している必要があります。 これに対して、ステートメントを使用して、 [DMX&#41;&#40;のマイニングモデルを作成 ](../dmx/create-mining-model-dmx.md)すると、モデルが作成され、基になるマイニング構造が同時に自動的に生成されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER MINING STRUCTURE <structure>  
ADD MINING MODEL <model>  
(  
    <column definition list>  
  [(<nested column definition list>) [WITH FILTER (<nested filter criteria>)]]  
)  
USING <algorithm> [(<parameter list>)]   
[WITH DRILLTHROUGH]  
[,FILTER(<filter criteria>)]  
```  
  
## <a name="arguments"></a>引数  
 *データ*  
 マイニング モデルが追加されるマイニング構造の名前です。  
  
 *model*  
 マイニングモデルの一意の名前。  
  
 *列定義の一覧*  
 列定義のコンマ区切りのリスト。  
  
 *入れ子になった列の定義リスト*  
 入れ子になったテーブルの列のコンマ区切りのリストです (該当する場合)。  
  
 *入れ子になったフィルター条件*  
 入れ子になったテーブルの列に適用されるフィルター式です。  
  
 *アルゴリズム*  
 プロバイダーによって定義されたデータマイニングアルゴリズムの名前。  
  
> [!NOTE]  
>  現在のプロバイダーでサポートされているアルゴリズムの一覧は [DMSCHEMA_MINING_SERVICES 行セット](/previous-versions/sql/sql-server-2012/ms126251(v=sql.110))を使用して取得できます。 の現在のインスタンスでサポートされているアルゴリズムを表示するには [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、「 [データマイニングのプロパティ](/analysis-services/server-properties/data-mining-properties)」を参照してください。  
  
 *パラメーターリスト*  
 省略可能。 アルゴリズムに対してプロバイダーが定義したパラメーターのコンマ区切りのリスト。  
  
 *フィルター条件*  
 ケーステーブルの列に適用されるフィルター式。  
  
## <a name="remarks"></a>解説  
 マイニング構造に複合キーが含まれている場合、マイニングモデルには、構造体で定義されているすべてのキー列が含まれている必要があります。  
  
 クラスタリングアルゴリズムとシーケンスクラスターアルゴリズムを使用して作成されたモデルなど、予測可能な列がモデルに必要ない場合は、 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[msCoName](../includes/msconame-md.md)] ステートメントに列定義を含める必要はありません。 結果として得られるモデルのすべての属性が入力として扱われます。  
  
 ケーステーブルに適用される **WITH** 句では、フィルター処理とドリルスルーの両方のオプションを指定できます。  
  
-   **フィルター**キーワードとフィルター条件を追加します。 このフィルターは、マイニングモデル内のケースに適用されます。  
  
-   **ドリルスルー**キーワードを追加して、マイニングモデルのユーザーがモデルの結果からケースデータにドリルダウンできるようにします。 データマイニング拡張機能 (DMX) では、ドリルスルーはモデルの作成時にのみ有効にすることができます。  
  
 ケースフィルターとドリルスルーの両方を使用するには、次の例に示す構文を使用して、単一 **の WITH** 句でキーワードを結合します。  
  
 `WITH DRILLTHROUGH, FILTER(Gender = 'Male')`  
  
## <a name="column-definition-list"></a>列定義の一覧  
 モデルの構造を定義するには、各列について次の情報を含む列定義リストを指定します。  
  
-   名前 (必須)  
  
-   エイリアス (省略可能)  
  
-   モデリングフラグ  
  
-   予測要求。予測可能な値が列に含まれているかどうかをアルゴリズムに示します。予測可能な値は、 **PREDICT** 句または **PREDICT_ONLY** 句で示されます。  
  
 列定義リストの次の構文を使用して、単一の列を定義します。  
  
```  
<structure column name>  [AS <model column name>]  [<modeling flags>]    [<prediction>]  
```  
  
### <a name="column-name-and-alias"></a>列名と別名  
 列定義リストで使用する列名は、マイニング構造で使用されている列の名前にする必要があります。 ただし、必要に応じて、マイニングモデルの構造列を表す別名を定義することもできます。 同じ構造列に複数の列定義を作成し、列の各コピーに異なる別名と予測の使用方法を割り当てることもできます。 既定では、別名を定義しない場合、構造列の名前が使用されます。 詳細については、「 [モデル列の別名を作成](/analysis-services/data-mining/create-an-alias-for-a-model-column)する」を参照してください。  
  
 入れ子になったテーブルの列の場合は、入れ子になったテーブルの名前を指定し、データ型を **テーブル**として指定します。次に、モデルに含める入れ子になった列の一覧をかっこで囲んで指定します。  
  
 入れ子になったテーブル列の定義の後にフィルター条件式を付加ことによって、入れ子になったテーブルに適用されるフィルター式を定義できます。  
  
### <a name="modeling-flags"></a>ModelingFlags  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、マイニングモデル列で使用する次のモデリングフラグがサポートされています。  
  
> [!NOTE]  
>  NOT_NULL モデリングフラグは、マイニング構造列に適用されます。 詳細については、「[CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md)」を参照してください。  
  
|期間|定義|  
|-|-|  
|**リグレッサー**|アルゴリズムが、指定した列を回帰アルゴリズムの回帰式に使用できることを示します。|  
|**MODEL_EXISTENCE_ONLY**|属性列の値が属性の有無ほど重要ではないことを示します。|  
  
 列には複数のモデリング フラグを定義できます。 モデリングフラグの使用方法の詳細については、「 [モデル化フラグ &#40;DMX&#41;](../dmx/modeling-flags-dmx.md)」を参照してください。  
  
### <a name="prediction-clause"></a>予測句  
 予測句では、予測列の使用方法を記述します。 次の表は、使用可能な句を示しています。  
  
|句|説明|  
|-|-|  
|**PREDICT**|この列はモデルによって予測できます。また、その値を入力として使用して、その他の予測可能列の値を予測することもできます。|  
|**PREDICT_ONLY**|この列はモデルによって予測できますが、その値を入力ケースで使用して他の予測可能列の値を予測することはできません。|  
  
## <a name="filter-criteria-expressions"></a>フィルター条件式  
 マイニングモデルで使用するケースを制限するフィルターを定義できます。 フィルターは、ケース テーブルの列、入れ子になったテーブルの行、またはその両方に適用できます。  
  
 フィルター条件式は、WHERE 句に似た単純な DMX 述語です。 フィルター式は、基本的な算術演算子、スカラー、および列名を使用する式に制限されます。 ただし、EXISTS 演算子は例外です。これは、サブクエリに対して少なくとも 1 行が返される場合は true に評価されます。 述語は、一般的な論理演算子 (AND、OR、および NOT) を使用して組み合わせることができます。  
  
 マイニングモデルで使用されるフィルターの詳細については、「 [Analysis Services データマイニング&#41;&#40;マイニングモデルのフィルター ](/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining)」を参照してください。  
  
> [!NOTE]  
>  フィルター内の列は、マイニング構造列である必要があります。 モデル列または別名列に対してフィルターを作成することはできません。  
  
 DMX の演算子と構文の詳細については、「 [マイニングモデル列](/analysis-services/data-mining/mining-model-columns)」を参照してください。  
  
## <a name="parameter-definition-list"></a>パラメーター定義リスト  
 アルゴリズム パラメーターをパラメーター リストに追加して、モデルのパフォーマンスと機能を調整できます。 使用できるパラメーターは、USING 句で指定するアルゴリズムによって異なります。 各アルゴリズムに関連付けられているパラメーターの一覧については、「データマイニング [アルゴリズム &#40;Analysis Services データマイニング&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)」を参照してください。  
  
 パラメーターリストの構文は次のとおりです。  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
## <a name="example-1-add-a-model-to-a-structure"></a>例 1: 構造へのモデルの追加  
 次の例では、Naive Bayes マイニングモデルを **新しいメーリング** マイニング構造に追加し、属性状態の最大数を50に制限しています。  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes (MAXIMUM_STATES = 50)  
```  
  
## <a name="example-2-add-a-filtered-model-to-a-structure"></a>例 2: 構造へのフィルター選択されたモデルの追加  
 次の例では、マイニングモデルを `Naive Bayes Women` **新しいメーリング** マイニング構造に追加します。 新しいモデルには、例1で追加したマイニングモデルと同じ基本的な構造があります。ただし、このモデルでは、50年の年齢を超えて、マイニング構造のケースを女性の顧客に限定しています。  
  
```  
ALTER MINING STRUCTURE [New Mailing]  
ADD MINING MODEL [Naive Bayes Women]  
(  
    CustomerKey,   
    Gender,  
    [Number Cars Owned],  
    [Bike Buyer] PREDICT  
)  
USING Microsoft_Naive_Bayes  
WITH FILTER([Gender] = 'F' AND [Age] >50)  
```  
  
## <a name="example-3-add-a-filtered-model-to-a-structure-with-a-nested-table"></a>例 3: 入れ子になったテーブルを含む構造へのフィルター選択されたモデルの追加  
 次の例では、変更後のバージョンのマーケットバスケットマイニング構造にマイニングモデルを追加します。 この例で使用されているマイニング構造は、customer region の属性を含む**region**列を追加するように変更されています。また、[**高**]、[中 **]、また**は [**低**] の値を使用して顧客の収入を分類する [**収益グループ**] 列を追加しました。  
  
 また、マイニング構造には、顧客が購入したアイテムを一覧表示する入れ子になったテーブルも含まれます。  
  
 入れ子になったテーブルがマイニング構造に含まれているため、ケーステーブル、入れ子になったテーブル、またはその両方に対してフィルターを定義できます。 この例では、ケース フィルターと入れ子になった行フィルターを組み合わせて、Road Tire モデルのいずれかの品目を購入した富裕なヨーロッパの顧客だけにケースを制限します。  
  
```  
ALTER MINING STRUCTURE [Market Basket with Region and Income]  
ADD MINING MODEL [Decision Trees]  
(  
    CustomerKey,   
    Region,  
    [Income Group],  
    [Product] PREDICT (Model)   
WITH FILTER (EXISTS (SELECT * FROM [v Assoc Seq Line Items] WHERE   
 [Model] = 'HL Road Tire' OR  
 [Model] = 'LL Road Tire' OR  
 [Model] = 'ML Road Tire' )  
)  
) WITH FILTER ([Income Group] = 'High' AND [Region] = 'Europe')  
USING Microsoft_Decision Trees  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41; データ定義ステートメント &#40;のデータマイニング拡張機能](../dmx/dmx-statements-data-definition.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
