---
title: sp_rxPredict を使用したリアルタイム スコアリング
description: 予測ワークロードの予測またはスコアのパフォーマンスを高めるために、SQL Server で sp_rxPredict システム ストアド プロシージャを使用したリアルタイム スコアリングを実行する方法について説明します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/31/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e6809a66ce7f5fd425ce9bfeb2b1fea919c4dfaa
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956933"
---
# <a name="real-time-scoring-with-sp_rxpredict-in-sql-server"></a>SQL Server での sp_rxPredict を使用したリアルタイム スコアリング
[!INCLUDE[sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

予測ワークロードの予測またはスコアのパフォーマンスを高めるために、SQL Server で [sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md) システム ストアド プロシージャを使用したリアルタイム スコアリングを実行する方法について説明します。

`sp_rxPredict` を使用したリアルタイム スコアリングは言語に依存せず、[Machine Learning Services](../sql-server-machine-learning-services.md) または [R Services](../r/sql-server-r-services.md) の R または Python ランタイムに依存することなく実行されます。 モデルが Microsoft 関数を使用して作成およびトレーニングされてから、SQL Server でバイナリ形式にシリアル化されていれば、リアルタイム スコアリングを使用して、R または Python アドオンがインストールされていない SQL Server インスタンスでの新しいデータ入力に対する予測される結果を生成できます。

## <a name="how-real-time-scoring-works"></a>リアルタイム スコアリングのしくみ

リアルタイム スコアリングは、R では [RevoScaleR](../r/ref-r-revoscaler.md) または [MicrosoftML](../r/ref-r-microsoftml.md) の、Python では [revoscalepy](../python/ref-py-revoscalepy.md) または [microsoftml](../python/ref-py-microsoftml.md) の関数に基づく特定の種類のモデルでサポートされています。 これは、ネイティブ C++ ライブラリを使用して、特別なバイナリ形式で格納された機械学習モデルに提供されるユーザー入力に基づいてスコアを生成します。

トレーニング済みのモデルは、 [Machine Learning Services](../sql-server-machine-learning-services.md) または [R Services](../r/sql-server-r-services.md) で外部言語ランタイムを呼び出すことなくスコアリングに使用できるため、複数のプロセスのオーバーヘッドが削減されます。 

リアルタイム スコアリングは、複数の手順で構成されるプロセスです。

1. スコアリングを行うストアド プロシージャは、データベースごとに有効にする必要があります。
2. 事前トレーニング済みのモデルをバイナリ形式で読み込みます。
3. モデルへの入力として、スコア付けされる新しい入力データ (表形式または単一行) を指定します。
4. スコアを生成するには、[sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md) ストアド プロシージャを呼び出します。

## <a name="prerequisites"></a>前提条件

+ [SQL Server CLR 統合を有効にします](../../relational-databases/clr-integration/clr-integration-enabling.md)。

+ [リアルタイム スコアリングを有効にします](#bkmk_enableRtScoring)。

+ このモデルは、サポートされる **rx** アルゴリズムのいずれかを使用して、事前にトレーニングされている必要があります。 R の場合、`sp_rxPredict` によるリアルタイムのスコアリングは、[RevoScaleR および Microsoft Ml でサポートされているアルゴリズム](#bkmk_rt_supported_algos)で動作します。 Python については、[revoscalepy および microsoftml でサポートされているアルゴリズム](#bkmk_py_supported_algos)を参照してください。

+ モデルのシリアル化には、R の場合は [rxSerialize](/machine-learning-server/r-reference/revoscaler/rxserializemodel)、Python の場合は [rx_serialize_model](/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) を使用します。 これらのシリアル化関数は、高速スコアリングをサポートするように最適化されています。

+ 呼び出し元のデータベース エンジン インスタンスにモデルを保存します。 このインスタンスには、R または Python のランタイム拡張機能を含める必要はありません。

> [!Note]
> 現在、リアルタイム スコアリングは、数行から数百行までの範囲の、より小さなデータセットに対する高速予測向けに最適化されています。 大きなデータセットでは、[rxPredict](/machine-learning-server/r-reference/revoscaler/rxpredict) を使用する方が高速になる場合があります。

<a name ="bkmk_enableRtScoring"></a> 

## <a name="enable-real-time-scoring"></a>リアルタイム スコアリングを有効にする

スコアリングに使用するデータベースごとに、この機能を有効にする必要があります。 サーバー管理者は、RevoScaleR パッケージに含まれているコマンドライン ユーティリティ (RegisterRExt.exe) を実行する必要があります。

> [!NOTE]
> リアルタイム スコアリングを機能させるには、インスタンスで SQL CLR 機能を有効にする必要があります。さらに、データベースは信頼できるものとしてマークされている必要があります。 スクリプトを実行するとき、これらのアクションが実行されます。 ただし、これを行う前に、セキュリティへの付加的な影響について検討してください。

1. 管理者特権でコマンド プロンプトを開き、RegisterRExt.exe が格納されているフォルダーに移動します。 既定のインストールでは、次のパスを使用できます。

    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. 次のコマンドを実行します。このとき、拡張ストアド プロシージャを有効にするインスタンスの名前とターゲット データベースに置き換えます。

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    たとえば、拡張ストアド プロシージャを既定のインスタンスの CLRPredict データベースに追加するには、次のように入力します。

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    データベースが既定のインスタンス上にある場合、インスタンス名は省略可能です。 名前付きインスタンスを使用している場合は、インスタンス名を指定する必要があります。

3. RegisterRExt.exe は、次のオブジェクトを作成します。

    + 信頼されたアセンブリ
    + ストアド プロシージャ `sp_rxPredict`
    + 新しいデータベース ロール、`rxpredict_users`。 データベース管理者は、このロールを使用して、リアルタイム スコアリング機能を使用するユーザーに権限を付与できます。

4. `sp_rxPredict` を実行する必要があるユーザーを新しいロールに追加します。

> [!NOTE]
>
> SQL Server 2017 以降では、CLR 統合に関する問題を回避するために、追加のセキュリティ対策が実施されています。 これらの対策では、このストアド プロシージャの使用に対して追加の制限を課します。

## <a name="disable-real-time-scoring"></a>リアルタイム スコアリングを無効にする

リアルタイム スコアリング機能を無効にするには、管理者特権でコマンド プロンプトを開き、次のコマンドを実行します。`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

<a name="bkmk_py_supported_algos"></a>

## <a name="supported-algorithms"></a>サポートされているアルゴリズム

### <a name="python-algorithms-using-real-time-scoring"></a>リアルタイム スコアリングを使用する Python アルゴリズム

+ revoscalepy モデル

  + [rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) \*
  + [rx_logit](/machine-learning-server/python-reference/revoscalepy/rx-logit) \*
  + [rx_btrees](/machine-learning-server/python-reference/revoscalepy/rx-btrees) \*
  + [rx_dtree](/machine-learning-server/python-reference/revoscalepy/rx-dtree) \*
  + [rx_dforest](/machine-learning-server/python-reference/revoscalepy/rx-dforest) \*
  
  \* でマークされたモデルは、PREDICT 関数を使用したネイティブ スコアリングもサポートします。

+ microsoftml モデル

  + [rx_fast_trees](/machine-learning-server/python-reference/microsoftml/rx-fast-trees)
  + [rx_fast_forest](/machine-learning-server/python-reference/microsoftml/rx-fast-forest)
  + [rx_logistic_regression](/machine-learning-server/python-reference/microsoftml/rx-logistic-regression)
  + [rx_oneclass_svm](/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm)
  + [rx_neural_net](/machine-learning-server/python-reference/microsoftml/rx-neural-network)
  + [rx_fast_linear](/machine-learning-server/python-reference/microsoftml/rx-fast-linear)

+ Microsoftml によって提供される変換

  + [featurize_text](/machine-learning-server/python-reference/microsoftml/featurize-text)
  + [concat](/machine-learning-server/python-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/python-reference/microsoftml/categorical)
  + [categorical_hash](/machine-learning-server/python-reference/microsoftml/categorical-hash)

<a name="bkmk_rt_supported_algos"></a>

### <a name="r-algorithms-using-real-time-scoring"></a>リアルタイム スコアリングを使用する R アルゴリズム

+ RevoScaleR モデル

  + [rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod) \*
  + [rxLogit](/machine-learning-server/r-reference/revoscaler/rxlogit) \*
  + [rxBTrees](/machine-learning-server/r-reference/revoscaler/rxbtrees) \*
  + [rxDtree](/machine-learning-server/r-reference/revoscaler/rxdtree) \*
  + [rxdForest](/machine-learning-server/r-reference/revoscaler/rxdforest) \*
  
  \* でマークされたモデルは、PREDICT 関数を使用したネイティブ スコアリングもサポートします。

+ MicrosoftML モデル

  + [rxFastTrees](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [rxFastForest](/machine-learning-server/r-reference/microsoftml/rxfastforest)
  + [rxLogisticRegression](/machine-learning-server/r-reference/microsoftml/rxlogisticregression)
  + [rxOneClassSvm](/machine-learning-server/r-reference/microsoftml/rxoneclasssvm)
  + [rxNeuralNet](/machine-learning-server/r-reference/microsoftml/rxneuralnet)
  + [rxFastLinear](/machine-learning-server/r-reference/microsoftml/rxfastlinear)

+ MicrosoftML によって提供される変換

  + [featurizeText](/machine-learning-server/r-reference/microsoftml/rxfasttrees)
  + [concat](/machine-learning-server/r-reference/microsoftml/concat)
  + [categorical](/machine-learning-server/r-reference/microsoftml/categorical)
  + [categoricalHash](/machine-learning-server/r-reference/microsoftml/categoricalHash)
  + [selectFeatures](/machine-learning-server/r-reference/microsoftml/selectFeatures)

### <a name="unsupported-model-types"></a>サポートされていないモデルの種類

リアルタイム スコアリングはインタープリターを使用しません。そのため、インタープリターを必要とする可能性がある関数は、スコアリングの手順ではサポートされていません。  たとえば、次のようなものがあります。

+ `rxGlm` アルゴリズムまたは `rxNaiveBayes` アルゴリズムを使用するモデルはサポートされていません。

+ 変換関数または変換を含む数式を使用するモデル (`A ~ log(B` など) は、リアルタイム スコアリングではサポートされていません。 この種類のモデルを使用するには、データをリアルタイム スコアリングに渡す前に、入力データに対して変換を実行することをお勧めします。

## <a name="example"></a>例

このセクションでは、**リアルタイム**予測のモデルを準備し保存するために必要な手順について説明し、R で T-SQL から関数を呼び出す方法の例を示します。

### <a name="step-1-prepare-and-save-the-model"></a>手順 1. モデルを構築して保存する

sp\_rxPredict に必要なバイナリ形式は、PREDICT 関数を使用するために必要な形式と同じです。 そのため、R コードで、[rxSerializeModel](/machine-learning-server/r-reference/revoscaler/rxserializemodel) への呼び出しを含め、この例のように `realtimeScoringOnly = TRUE` を指定してください。

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-2-call-sp_rxpredict"></a>手順 2. sp_rxPredict を呼び出す

他のストアド プロシージャと同様に、`sp_rxPredict` を呼び出します。 現在のリリースでは、ストアド プロシージャは 2 つのパラメーターのみを取ります。バイナリ形式のモデルでは _\@model_、スコアリングで使用するデータには _\@inputData_ が有効な SQL クエリとして定義されています。

バイナリ形式は PREDICT 関数で使用されるものと同じであるため、前の例からのモデルおよびデータ テーブルを使用できます。

```sql
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> スコアリングの入力データにモデルの要件に合致する列が含まれていない場合、`sp_rxPredict` への呼び出しは失敗します。 現在、次の .NET データ型のみがサポートされています: double、float、short、ushort、long、ulong、および string。
>
> そのため、リアルタイム スコアリングに使用する前に、入力データでサポートされていない型をフィルターで除外することが必要になる場合があります。
>
> 対応する SQL 型の詳細については、「[SQL と CLR 型のマッピング](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)」または「[CLR パラメーター データのマッピング](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

+ [SQL 機械学習で PREDICT T-SQL 関数を使用したネイティブ スコアリング](native-scoring-predict-transact-sql.md)
+ [sp_rxPredict](../../relational-databases/system-stored-procedures/sp-rxpredict-transact-sql.md)
+ [SQL 機械学習](../index.yml)