---
title: T-SQL PREDICT によるネイティブ スコアリング
titleSuffix: SQL machine learning
description: PREDICT T-SQL 関数でネイティブ スコアリングを使用して、ほぼリアルタイムで新しいデータ入力の予測値を生成する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/29/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions'
ms.openlocfilehash: 9d8f65baaec3038431455712d64803459a96e45c
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956963"
---
# <a name="native-scoring-using-the-predict-t-sql-function-with-sql-machine-learning"></a>SQL 機械学習で PREDICT T-SQL 関数を使用したネイティブ スコアリング

[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

[PREDICT T-SQL 関数](../../t-sql/queries/predict-transact-sql.md) でネイティブ スコアリングを使用して、ほぼリアルタイムで新しいデータ入力の予測値を生成する方法について説明します。 ネイティブ スコアリングには、既にトレーニング済みのモデルが必要です。

`PREDICT` 関数では [SQL 機械学習](../index.yml)のネイティブ C++ 拡張機能が使われます。 この方法により、可能な限り最速の予測の処理速度と予測ワークロードと [Open Neural Network Exchange (ONNX)](https://onnx.ai/get-started.html) 形式のサポート モデルまたは [RevoScaleR](../r/ref-r-revoscaler.md) および [revoscalepy](../python/ref-py-revoscalepy.md) パッケージを使用してトレーニングされたモデルを実現します。

## <a name="how-native-scoring-works"></a>ネイティブ スコアリングのしくみ

ネイティブ スコアリングでは、ONNX または定義済みのバイナリ形式でモデルを読み取り、指定した新しいデータ入力のスコアを生成するライブラリを使用します。 モデルはトレーニングされ、デプロイされ、保存されるため、R または Python インタープリターを呼び出す必要なくスコアリングに使用できます。 つまり、複数のプロセスの相互作用のオーバーヘッドが軽減されるため、予測パフォーマンスが速くなります。

ネイティブ スコアリングを使用するには、`PREDICT` T-SQL 関数を呼び出し、次の必須の入力を渡します。

+ サポートされているモデルとアルゴリズムに基づく互換性のあるモデル。
+ 入力データ (通常は T-SQL クエリとして定義される)。

この関数は、入力データの予測を、パス スルーしたいソース データの任意の列と一緒に返します。

## <a name="prerequisites"></a>前提条件

`PREDICT` は以下で使用できます。

+ Windows および Linux 上の SQL Server 2017 以降のすべてのエディション
+ Azure SQL Managed Instance
+ Azure SQL データベース
+ Azure SQL Edge
+ Azure Synapse Analytics

関数は、既定で有効にされます。 R や Python をインストールしたり、追加機能を有効にしたりする必要はありません。

## <a name="supported-models"></a>サポートされているモデル

`PREDICT` 関数によってサポートされるモデル形式は、ネイティブ スコアリングを実行する SQL プラットフォームによって異なります。 どのプラットフォームでどのモデル形式がサポートされているかを確認するには、次の表を参照してください。

| プラットフォーム | ONNX モデル形式 | RevoScale モデル形式 |
|-|-|-|
| SQL Server | いいえ | [はい] |
| Azure SQL Managed Instance | ○ | はい |
| Azure SQL データベース | いいえ | [はい] |
| Azure SQL Edge | はい | いいえ |
| Azure Synapse Analytics | はい | いいえ |

::: moniker range="=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions"
### <a name="onnx-models"></a>ONNX モデル

このモデルは、[Open Neural Network Exchange (ONNX)](https://onnx.ai/get-started.html) モデル形式である必要があります。
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions"
### <a name="revoscale-models"></a>RevoScale モデル

モデルは、[RevoScaleR](../r/ref-r-revoscaler.md) または [revoscalepy](../python/ref-py-revoscalepy.md) パッケージを使用し、下に一覧表示されているサポートされる **rx** アルゴリズムのいずれかを使用して、事前にトレーニングされている必要があります。

モデルのシリアル化には、R の場合は [rxSerialize](/machine-learning-server/r-reference/revoscaler/rxserializemodel)、Python の場合は [rx_serialize_model](/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) を使用します。 これらのシリアル化関数は、高速スコアリングをサポートするように最適化されています。

<a name="bkmk_native_supported_algos"></a> 

#### <a name="supported-revoscale-algorithms"></a>サポートされている RevoScale アルゴリズム

次のアルゴリズムが revoscalepy と RevoScaleR でサポートされています。

+ revoscalepy アルゴリズム

  + [rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)
  + [rx_logit](/machine-learning-server/python-reference/revoscalepy/rx-logit) 
  + [rx_btrees](/machine-learning-server/python-reference/revoscalepy/rx-btrees) 
  + [rx_dtree](/machine-learning-server/python-reference/revoscalepy/rx-dtree) 
  + [rx_dforest](/machine-learning-server/python-reference/revoscalepy/rx-dforest) 

+ RevoScaleR アルゴリズム

  + [rxLinMod](/r-server/r-reference/revoscaler/rxlinmod)
  + [rxLogit](/r-server/r-reference/revoscaler/rxlogit)
  + [rxBTrees](/r-server/r-reference/revoscaler/rxbtrees)
  + [rxDtree](/r-server/r-reference/revoscaler/rxdtree)
  + [rxDForest](/r-server/r-reference/revoscaler/rxdforest)

MicrosoftML または microsoftml からのアルゴリズムを使用する必要がある場合は、[sp_rxPredict によるリアルタイムのスコアリング](../predictions/real-time-scoring.md)を使用します。

サポートされていないモデル タイプには、次のタイプが含まれます。

+ 他の変換を含むモデル
+ RevoScaleR または revoscalepy の同等の `rxGlm` または `rxNaiveBayes` アルゴリズムを使用するモデル
+ PMML モデル
+ 他のオープンソース ライブラリまたはサードパーティ ライブラリを使用して作成されたモデル
::: moniker-end

## <a name="examples"></a>例
::: moniker range="=azuresqldb-mi-current||=azure-sqldw-latest||=sqlallproducts-allversions"
### <a name="predict-with-an-onnx-model"></a>ONNX モデルを使用した PREDICT

この例では、ネイティブ スコアリングに `dbo.models` テーブルに格納されている ONNX モデルを使用する方法を示しています。

```sql
DECLARE @model VARBINARY(max) = (
        SELECT DATA
        FROM dbo.models
        WHERE id = 1
        );

WITH predict_input
AS (
    SELECT TOP (1000) [id]
        , CRIM
        , ZN
        , INDUS
        , CHAS
        , NOX
        , RM
        , AGE
        , DIS
        , RAD
        , TAX
        , PTRATIO
        , B
        , LSTAT
    FROM [dbo].[features]
    )
SELECT predict_input.id
    , p.variable1 AS MEDV
FROM PREDICT(MODEL = @model, DATA = predict_input, RUNTIME=ONNX) WITH (variable1 FLOAT) AS p;
```

> [!NOTE]
> **PREDICT** によって返される列と値は、モデルの種類によって異なる場合があるため、**WITH** 句を使用して、返されるデータのスキーマを定義する必要があります。
::: moniker-end

::: moniker range=">=sql-server-2017||=azuresqldb-mi-current||>=sql-server-linux-2017||=sqlallproducts-allversions"
### <a name="predict-with-revoscale-model"></a>RevoScale モデルによる PREDICT

この例では、R で **RevoScaleR** を使用してモデルを作成してから、T-SQL からリアルタイムの予測関数を呼び出しています。

#### <a name="step-1-prepare-and-save-the-model"></a>手順 1. モデルを構築して保存する

次のコードを実行して、サンプル データベースと必要なテーブルを作成します。

```sql
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
    "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

次のステートメントを使用して、データ テーブルに**アヤメ** データセットのデータを設定します。

```sql
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

ここで、モデルを格納するテーブルを作成します。

```sql
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

次のコードでは、**アヤメ** データセットに基づいてモデルを作成し、それを **models** という名前のテーブルに保存します。

```sql
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE]
> RevoScaleR からの [rxSerializeModel](/machine-learning-server/r-reference/revoscaler/rxserializemodel) 関数を使用して、モデルを保存してください。 標準の R `serialize` 関数では、必要な形式を生成できません。

次のようなステートメントを実行すると、格納されているモデルをバイナリ形式で表示できます。

```sql
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

#### <a name="step-2-run-predict-on-the-model"></a>手順 2. モデルで PREDICT を実行する

次の単純な PREDICT ステートメントでは、**ネイティブ スコアリング**関数を使用して、デシジョン ツリー モデルから分類を取得します。 指定した属性に基づいてアヤメの種類、花弁の長さと幅が予測されます。

```sql
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

"PREDICT 関数の実行中にエラーが発生しました。 モデルが破損しているか無効です" というエラーを受け取った場合、通常は、クエリがモデルを返さなかったことを意味します。 モデル名を正しく入力したかどうか、またはモデル テーブルが空であるかどうかを確認します。

> [!NOTE]
> **PREDICT** によって返される列と値は、モデルの種類によって異なる場合があるため、**WITH** 句を使用して、返されるデータのスキーマを定義する必要があります。
::: moniker-end

## <a name="next-steps"></a>次のステップ

+ [PREDICT T-SQL 関数](../../t-sql/queries/predict-transact-sql.md)
+ [SQL の機械学習のドキュメント](../index.yml)
+ [SQL Edge での ONNX を使用した機械学習と AI](/azure/azure-sql-edge/onnx-overview)
+ [Azure SQL Edge での ONNX モデルを使用したデプロイと予測](/azure/azure-sql-edge/deploy-onnx)