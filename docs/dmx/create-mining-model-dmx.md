---
description: マイニングモデル (DMX) の作成
title: マイニングモデルの作成 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 35382c7d1d7301d35d8517b62bac352a4ae9fb47
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726322"
---
# <a name="create-mining-model-dmx"></a>マイニングモデル (DMX) の作成
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  新しいマイニング モデルとマイニング構造の両方をデータベースに作成します。 モデルを作成するには、ステートメントで新しいモデルを定義するか、予測モデルマークアップ言語 (PMML) を使用します。 後者については、詳しい知識のあるユーザーのみ使用してください。  
  
 マイニング構造には、モデル名の後に「_structure」を追加した名前を付けます。これにより、構造名がモデル名から一意であることが保証されます。  
  
 既存のマイニング構造のマイニングモデルを作成するには、 [ALTER マイニング構造 &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) ステートメントを使用します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE [SESSION] MINING MODEL <model>  
(  
    [(<column definition list>)]  
)  
USING <algorithm> [(<parameter list>)] [WITH DRILLTHROUGH]  
CREATE MINING MODEL <model> FROM PMML <xml string>  
```  
  
## <a name="arguments"></a>引数  
 *model*  
 モデルの一意の名前です。  
  
 *列定義の一覧*  
 列定義のコンマ区切りのリスト。  
  
 *アルゴリズム*  
 現在のプロバイダーによって定義された、データ マイニング アルゴリズムの名前です。  
  
> [!NOTE]  
>  現在のプロバイダーでサポートされているアルゴリズムの一覧は [DMSCHEMA_MINING_SERVICES 行セット](/previous-versions/sql/sql-server-2012/ms126251(v=sql.110))を使用して取得できます。 の現在のインスタンスでサポートされているアルゴリズムを表示するには [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 、「 [データマイニングのプロパティ](/analysis-services/server-properties/data-mining-properties)」を参照してください。  
  
 *パラメーターリスト*  
 省略可能。 アルゴリズムに対してプロバイダーが定義したパラメーターのコンマ区切りのリスト。  
  
 *XML 文字列*  
 (高度な用途の場合のみ)。XML エンコードモデル (PMML)。 文字列は単一引用符 (') で囲む必要があります。  
  
 **Session**句を使用すると、接続が閉じられたとき、またはセッションがタイムアウトしたときにサーバーから自動的に削除されるマイニングモデルを作成できます。**セッション**マイニングモデルは、ユーザーがデータベース管理者である必要がなく、接続が開いている間のみディスク領域を使用するため、役に立ちます。  
  
 **WITH ドリルスルー**句を使用すると、新しいマイニングモデルでドリルスルーを実行できます。 ドリルスルーは、モデルの作成時にのみ可能です。 モデルの種類によっては、カスタムビューアーでモデルを参照するためにドリルスルーが必要になります。 Microsoft 汎用コンテンツ ツリー ビューアーを使用してモデルを予測または参照する場合は、ドリルスルーは必要ありません。  
  
 **CREATE マイニング model**ステートメントは、列定義の一覧、アルゴリズム、およびアルゴリズムパラメーターの一覧に基づいて、新しいマイニングモデルを作成します。  
  
### <a name="column-definition-list"></a>列定義の一覧  
 列定義の一覧を使用するモデルの構造を定義するには、各列に次の情報を含めます。  
  
-   名前 (必須)  
  
-   データ型 (必須)  
  
-   Distribution  
  
-   モデリングフラグの一覧  
  
-   コンテンツの種類 (必須)  
  
-   予測要求。この列を予測するようにアルゴリズムに指示します。これは、 **predict** 句または **PREDICT_ONLY** 句によって示されます。  
  
-   **関連する to**句によって示される、属性列とのリレーションシップ (適用される場合にのみ必須)  
  
 列定義リストの次の構文を使用して、単一の列を定義します。  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<prediction>]    [<column relationship>]   
```  
  
 入れ子になったテーブル列を定義するには、列定義リストの次の構文を使用します。  
  
```  
<column name>    TABLE    [<prediction>] ( <non-table column definition list> )  
```  
  
 モデリング フラグを除き、特定のグループから句を 1 つだけ使用して列を定義します。 列には複数のモデリング フラグを定義できます。  
  
 列の定義に使用できるデータ型、コンテンツの種類、列の分布、およびモデリングフラグの一覧については、次のトピックを参照してください。  
  
-   [データ型 (データ マイニング)](/analysis-services/data-mining/data-types-data-mining)  
  
-   [コンテンツの種類 (データ マイニング)](/analysis-services/data-mining/content-types-data-mining)  
  
-   [列の分布 (データ マイニング)](/analysis-services/data-mining/column-distributions-data-mining)  
  
-   [モデリング フラグ (データ マイニング)](/analysis-services/data-mining/modeling-flags-data-mining)  
  
 ステートメントに句を追加して、2つの列間のリレーションシップを記述できます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、次の句の使用がサポートされてい \<Column relationship> ます。  
  
 **関連**  
 この形式は値の階層を示します。 関連する列のターゲットには、入れ子になったテーブルのキー列、ケース行の個別値列、または関連する TO 句を持つ別の列 (より深い階層を示す) を指定できます。  
  
 予測列の使用方法を説明するには、予測句を使用します。 次の表では、使用可能な2つの句について説明します。  
  
|\<prediction> clause|説明|  
|---------------------------|-----------------|  
|**PREDICT**|この列は、モデルによって予測できます。また、入力ケースで指定して、その他の予測可能列の値を予測することもできます。|  
|**PREDICT_ONLY**|この列はモデルによって予測できますが、その値を入力ケースで使用して他の予測可能列の値を予測することはできません。|  
  
### <a name="parameter-definition-list"></a>パラメーター定義リスト  
 パラメーターリストを使用して、マイニングモデルのパフォーマンスと機能を調整できます。 パラメーターリストの構文は次のとおりです。  
  
```  
[<parameter> = <value>, <parameter> = <value>,...]  
```  
  
 各アルゴリズムに関連付けられているパラメーターの一覧については、「データマイニング [アルゴリズム &#40;Analysis Services データマイニング&#41;](/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)」を参照してください。  
  
## <a name="remarks"></a>解説  
 組み込みのテストデータセットを含むモデルを作成する場合は、ステートメント CREATE マイニング STRUCTURE の後に ALTER マイニング STRUCTURE を使用する必要があります。 ただし、すべての種類のモデルで予約データセットがサポートされるわけではありません。 詳細については、「[CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md)」を参照してください。  
  
 CREATEMODEL ステートメントを使用してマイニングモデルを作成する方法のチュートリアルについては、「 [タイムシリーズ予測 DMX のチュートリアル](/previous-versions/sql/sql-server-2016/cc879270(v=sql.130))」を参照してください。  
  
## <a name="naive-bayes-example"></a>Naive Bayes の例  
 次の例では、 [!INCLUDE[msCoName](../includes/msconame-md.md)] Naive Bayes アルゴリズムを使用して、新しいマイニングモデルを作成します。 自転車の購入者列は、予測可能な属性として定義されています。  
  
```  
CREATE MINING MODEL [NBSample]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE PREDICT  
)  
USING Microsoft_Naive_Bayes  
```  
  
## <a name="association-model-example"></a>アソシエーションモデルの例  
 次の例では、[!INCLUDE[msCoName](../includes/msconame-md.md)] 結合アルゴリズムを使用して、新しいマイニング モデルを作成しています。 ステートメントでは、テーブル列を使用してモデル定義内にテーブルを入れ子にする機能を利用します。 モデルは、 *MINIMUM_PROBABILITY* パラメーターと *MINIMUM_SUPPORT* パラメーターを使用して変更されます。  
  
```  
CREATE MINING MODEL MyAssociationModel (  
    OrderNumber TEXT KEY,  
    [Products] TABLE PREDICT (  
        [Model] TEXT KEY  
    )  
)  
USING Microsoft_Association_Rules (Minimum_Probability = 0.1, MINIMUM_SUPPORT = 0.01)  
```  
  
## <a name="sequence-clustering-example"></a>シーケンス クラスタリングの例  
 次の例では、[!INCLUDE[msCoName](../includes/msconame-md.md)] シーケンス クラスタリング アルゴリズムを使用して、新しいマイニング モデルを作成しています。 2つのキーを使用してモデルを定義します。 OrderNumber 列は、ケースキーとして使用され、個々の注文を指定します。 LineNumber 列は、入れ子になったテーブルのキーとして使用され、注文が追加されたアイテムのシーケンスを指定します。  
  
```  
CREATE MINING MODEL BuyingSequence (  
    [Order Number] TEXT KEY,  
    [Products] TABLE   
     (  
        [Line Number] LONG KEY SEQUENCE,  
        [Model] TEXT DISCRETE PREDICT  
    )  
)  
USING Microsoft_Sequence_Clustering  
```  
  
## <a name="time-series-example"></a>時系列の例  
 次の例では、 [!INCLUDE[msCoName](../includes/msconame-md.md)] タイムシリーズアルゴリズムを使用して、ARTxp アルゴリズムを使用して新しいマイニングモデルを作成します。 ReportingDate は時系列のキー列で、ModelRegion はデータ系列のキー列です。 この例では、データの周期を 12 か月としています。 したがって、 *PERIODICITY_HINT* パラメーターは12に設定されます。  
  
> [!NOTE]  
>  *PERIODICITY_HINT*パラメーターを指定するには、中かっこ文字を使用する必要があります。 また、値は文字列であるため、単一引用符で囲む必要があります: "{ \<numeric value> }"。  
  
```  
CREATE MINING MODEL SalesForecast (  
        ReportingDate DATE KEY TIME,  
        ModelRegion TEXT KEY,  
        Amount LONG CONTINUOUS PREDICT,  
        Quantity LONG CONTINUOUS PREDICT  
)  
USING Microsoft_Time_Series (PERIODICITY_HINT = '{12}', FORECAST_METHOD = 'ARTXP')  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41; データ定義ステートメント &#40;のデータマイニング拡張機能](../dmx/dmx-statements-data-definition.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
