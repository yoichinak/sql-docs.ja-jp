---
description: マイニング構造の作成 (DMX)
title: マイニング構造の作成 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ab738433380302e0f3d8bc70113aa2a8d13f7ac8
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726283"
---
# <a name="create-mining-structure-dmx"></a>マイニング構造の作成 (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  データベースに新しいマイニング構造を作成し、必要に応じてトレーニングパーティションとテストパーティションを定義します。 マイニング構造を作成した後は、 [ALTER マイニング構造 &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) ステートメントを使用して、マイニング構造にモデルを追加できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE [SESSION] MINING STRUCTURE <structure>  
(  
    [(<column definition list>)]  
)  
[WITH HOLDOUT (<holdout-specifier> [OR <holdout-specifier>])]  
[REPEATABLE(<holdout seed>)]  
<holdout-specifier>::=  <holdout-maxpercent> PERCENT | <holdout-maxcases> CASES  
```  
  
## <a name="arguments"></a>引数  
 *データ*  
 構造の一意の名前です。  
  
 *列定義の一覧*  
 列定義のコンマ区切りのリスト。  
  
 *予約-maxpercent*  
 テスト用に確保するデータの割合を示す 1 ~ 100 の整数。  
  
 *予約-maxcases*  
 テストに使用するケースの最大数を示す整数です。  
  
 ケースの最大数に対して指定された値が入力ケース数よりも大きい場合は、すべての入力ケースがテストに使用され、警告が発生します。  
  
> [!NOTE]  
>  ケースの割合と最大数の両方を指定した場合は、2つの制限のうち小さい方が使用されます。  
  
 *提示したシード*  
 データのパーティション分割を開始するためのシードとして使用される整数。  
  
 0 に設定すると、マイニング構造 ID のハッシュがシードとして使用されます。  
  
> [!NOTE]  
>  パーティションを再現できるようにする必要がある場合は、シードを指定する必要があります。  
  
 既定値 : REPEATABLE(0)  
  
## <a name="remarks"></a>解説  
 マイニング構造を定義するには、列リストを指定し、必要に応じて列間の階層リレーションシップを指定して、さらに必要に応じてマイニング構造をトレーニング データセットとテスト データセットにパーティション分割します。  
  
 オプションの SESSION キーワードは、その構造が、現在のセッションの間しか使用できない一時的な構造であることを示します。 セッションが終了すると、構造と、その構造に基づくすべてのモデルが削除されます。 一時的なマイニング構造およびモデルを作成するには、まずデータベースプロパティ AllowSessionMiningModels を設定する必要があります。 詳細については、「 [データ マイニング プロパティ](/analysis-services/server-properties/data-mining-properties)」を参照してください。  
  
## <a name="column-definition-list"></a>列定義の一覧  
 列定義リストに各列の次の情報を含めることによって、マイニング構造を定義します。  
  
-   名前 (必須)  
  
-   データ型 (必須)  
  
-   Distribution  
  
-   モデリングフラグの一覧  
  
-   コンテンツの種類 (必須)  
  
-   RELATED TO 句によって示される、属性列とのリレーションシップです (適用される場合にのみ必須)。  
  
 列定義リストの次の構文を使用して、単一の列を定義します。  
  
```  
<column name>    <data type>    [<Distribution>]    [<Modeling Flags>]    <Content Type>    [<column relationship>]  
```  
  
 列定義リストの次の構文を使用して、入れ子になったテーブル列を定義します。  
  
```  
<column name>    TABLE    ( <column definition list> )  
```  
  
 構造列の定義に使用できるデータ型、コンテンツの種類、列の分布、およびモデリングフラグの一覧については、次のトピックを参照してください。  
  
-   [データ型 (データ マイニング)](/analysis-services/data-mining/data-types-data-mining)  
  
-   [コンテンツの種類 (データ マイニング)](/analysis-services/data-mining/content-types-data-mining)  
  
-   [列の分布 (データ マイニング)](/analysis-services/data-mining/column-distributions-data-mining)  
  
-   [モデリング フラグ (データ マイニング)](/analysis-services/data-mining/modeling-flags-data-mining)  
  
 列には複数のモデリング フラグ値を定義できます。 ただし、1つの列に対して使用できるコンテンツの種類は1つとデータ型は1つだけです。  
  
### <a name="column-relationships"></a>列のリレーションシップ  
 任意の列定義ステートメントに句を追加して、2つの列間のリレーションシップを記述できます。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、次の句の使用がサポートされてい \<column relationship> ます。  
  
 **関連**  
 値の階層を示します。 関連する列のターゲットには、入れ子になったテーブルのキー列、ケース行の個別値列、または関連する TO 句を持つ別の列 (より深い階層を示す) を指定できます。  
  
## <a name="holdout-parameters"></a>提示パラメーター  
 提示されたパラメーターを指定する場合は、構造データのパーティションを作成します。 予約に指定した量はテスト用に予約されており、残りのデータはトレーニングに使用されます。 既定では、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] を使用してマイニング構造を作成する場合、30% のテスト データと 70% のトレーニング データを含む、提示されたパーティションが作成されます。 詳しくは、「 [Training and Testing Data Sets](/analysis-services/data-mining/training-and-testing-data-sets)」をご覧ください。  
  
 データマイニング拡張機能 (DMX) を使用してマイニング構造を作成する場合は、提示されたパーティションを作成するように手動で指定する必要があります。  
  
> [!NOTE]  
>  **ALTER マイニング STRUCTURE**ステートメントでは、予約はサポートされていません。  
  
 提示されたパラメーターは 3 つまで指定できます。 提示されたケースの最大数と提示されたケースの割合の両方を指定すると、ケースの最大数に達するまでケースの割合が予約されます。 予約のパーセンテージを整数として指定し、その後に **パーセント** キーワードを付けて、ケースの最大数を整数として指定し、その後に **ケース** キーワードを指定します。 次の例に示すように、条件を任意の順序で組み合わせることができます。  
  
```  
WITH HOLDOUT (20 PERCENT)   
WITH HOLDOUT (2000 CASES)   
WITH HOLDOUT (20 PERCENT OR 2000 CASES)   
WITH HOLDOUT (2000 CASES OR 20 PERCENT)  
```  
  
 提示されたシードは、トレーニングデータセットまたはテストデータセットにケースをランダムに割り当てるプロセスの開始点を制御します。 提示されたシードを設定すると、パーティションを反復可能にすることができます。 提示されたシードを指定しない場合、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] では、マイニング構造の名前を使用してシードが作成されます。 構造の名前を変更すると、シード値が変わります。 提示されたシードパラメーターは、他の提示されたパラメーターのいずれかまたは両方で使用できます。  
  
> [!NOTE]  
>  パーティション情報はトレーニングデータと共にキャッシュされるため、提示を使用するには、マイニング構造の **Cachemode** プロパティが **KeepTrainingData**に設定されていることを確認する必要があります。 これは、の [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 新しいマイニング構造の既定の設定です。 提示されたパーティションを含む既存のマイニング構造で **Cachemode** プロパティを **ClearTrainingCases** に変更しても、処理されたマイニングモデルには影響しません。 ただし、 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> が **KeepTrainingData**に設定されていない場合、提示されたパラメーターは無効になります。 これは、すべてのソースデータがトレーニングに使用され、テストセットは使用できなくなることを意味します。 パーティションの定義は、構造体を使用してキャッシュされます。トレーニングケースのキャッシュをクリアすると、テストデータのキャッシュと提示されたセットの定義もクリアされます。  
  
## <a name="examples"></a>例  
 次の例では、DMX を使用して、提示されたマイニング構造を作成する方法を示します。  
  
### <a name="example-1-adding-a-structure-with-no-training-set"></a>例 1 : トレーニング セットを含まない構造を追加する  
 次の例では、 `New Mailing` 関連するマイニングモデルを作成せず、予約を使用せずに、という名前の新しいマイニング構造を作成します。 マイニングモデルを構造に追加する方法については、「 [ALTER マイニング structure &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md)」を参照してください。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)  
```  
  
### <a name="example-2-specifying-holdout-percentage-and-seed"></a>例 2: 提示された割合とシードを指定する  
 次の句を列定義リストの後に追加すると、マイニング構造に関連付けられているすべてのマイニングモデルのテストに使用できるデータセットを定義できます。 ステートメントでは、ケースの最大数を制限せずに、合計入力ケースの25% であるテストセットが作成されます。 5000は、パーティションを作成するためのシードとして使用されます。 シードを指定すると、基になるデータが変更されない限り、マイニング構造を処理するたびに、同じケースがテストセットに対して選択されます。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT) REPEATABLE(5000)  
```  
  
### <a name="example-3-specifying-holdout-percentage-and-max-cases"></a>例 3: 提示された割合と最大ケースを指定する  
 次の句は、合計入力ケースの25% または2000ケースのいずれか少ない方を含むテストセットを作成します。 シードとして0が指定されているので、入力したケースのサンプリングを開始するために使用されるシードの作成には、マイニング構造の名前が使用されます。  
  
```  
CREATE MINING STRUCTURE [New Mailing]  
(  
    CustomerKey LONG KEY,   
    Gender TEXT DISCRETE,  
    [Number Cars Owned] LONG DISCRETE,  
    [Bike Buyer] LONG DISCRETE   
)   
WITH HOLDOUT(25 PERCENT OR 2000 CASES) REPEATABLE(0)  
```  
  
## <a name="see-also"></a>参照  
 [DMX&#41; データ定義ステートメント &#40;のデータマイニング拡張機能](../dmx/dmx-statements-data-definition.md)   
 [DMX&#41; データ操作ステートメントを &#40;データマイニング拡張機能](../dmx/dmx-statements-data-manipulation.md)   
 [データ マイニング拡張機能 &#40;DMX&#41; ステートメント リファレンス](../dmx/data-mining-extensions-dmx-statements.md)  
  
