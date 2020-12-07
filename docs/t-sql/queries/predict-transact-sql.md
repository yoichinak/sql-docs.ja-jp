---
description: PREDICT (Transact-SQL)
title: PREDICT (Transact-SQL)
titleSuffix: SQL machine learning
ms.custom: ''
ms.date: 06/26/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PREDICT clause
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||>=azure-sqldw-latest||=sqlallproducts-allversions'
ms.openlocfilehash: 6a21506caf12537eb8acab96c97fa53c62b7fadf
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116283"
---
# <a name="predict-transact-sql"></a>PREDICT (Transact-SQL)

[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

格納されているモデルに基づいて予測値やスコアを生成します。 詳細については、「[PREDICT T-SQL 関数を使用したネイティブ スコアリング](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)」をご覧ください。

## <a name="syntax"></a>構文

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

```syntaxsql
PREDICT  
(  
  MODEL = @model | model_literal,  
  DATA = object AS <table_alias>
  [, RUNTIME = ONNX ]
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

MODEL = @model | model_literal  
```

::: moniker-end

::: moniker range=">=azure-sqldw-latest||=sqlallproducts-allversions"

```syntaxsql
PREDICT  
(  
  MODEL = <model_object>,
  DATA = object AS <table_alias>
  [, RUNTIME = ONNX ]
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

<model_object> ::=
  {
    model_literal
    | model_variable
    | ( scalar_subquery )
  }
```

::: moniker-end

### <a name="arguments"></a>引数

**MODEL**

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=sqlallproducts-allversions"
`MODEL` パラメーターは、スコア付けまたは予測に使用するモデルを指定するために使用されます。 モデルは、変数、リテラル、またはスカラー式として指定されます。

`PREDICT` は [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) と [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) パッケージを使用してトレーニングされたモデルをサポートします。
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
`MODEL` パラメーターは、スコア付けまたは予測に使用するモデルを指定するために使用されます。 モデルは、変数、リテラル、またはスカラー式として指定されます。

Azure SQL Managed Instance では、`PREDICT` は [Open Neural Network Exchange (ONNX)](https://onnx.ai/get-started.html) 形式のモデル、または [revoscalepy](../../machine-learning/r/ref-r-revoscaler.md) および [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) パッケージを使用してトレーニングされたモデルをサポートしています。
::: moniker-end

::: moniker range=">=azure-sqldw-latest||=sqlallproducts-allversions"
`MODEL` パラメーターは、スコア付けまたは予測に使用するモデルを指定するために使用されます。 モデルは、変数、リテラル、スカラー式、またはスカラー サブクエリとして指定されます。

Azure Synapse Analytics では、`PREDICT` は [Open Neural Network Exchange (ONNX)](https://onnx.ai/get-started.html) 形式のモデルをサポートしています。
::: moniker-end

**データ**

DATA パラメーターは、スコア付けまたは予測に使用するモデルを指定するために使用されます。 データは、クエリ内でテーブル ソースの形式で指定されます。 テーブル ソースには、テーブル、テーブルの別名、CTE の別名、ビュー、またはテーブル値関数のいずれかを指定できます。

**RUNTIME = ONNX**

> [!IMPORTANT]
> `RUNTIME = ONNX` 引数は [Azure SQL Managed Instance](/azure/azure-sql/managed-instance/machine-learning-services-overview) および [Azure SQL Edge](/azure/sql-database-edge/onnx-overview) でのみ使用できます。

モデルの実行に使用される機械学習エンジンを示します。 `RUNTIME` パラメーターの値は常に `ONNX` です。 Azure SQL Edge にはこのパラメーターが必須です。 Azure SQL Managed Instance では、パラメーターは省略可能で、ONNX モデルを使用する場合にのみ使用されます。

**WITH ( <result_set_definition> )**

WITH 句は、`PREDICT` 関数によって返される出力のスキーマを指定するのに使用されます。

`PREDICT` 関数自体から返される列に加え、データ入力の一部であるすべての列がクエリで使用できます。

### <a name="return-values"></a>戻り値

定義済みのスキーマは使用できません。モデルのコンテンツは検証されず、返された列の値も検証されません。

- `PREDICT` 関数は入力として列を通過します。
- `PREDICT` 関数では、新しい列も生成されますが、列の数とそのデータ型は、予測に使用されたモデルの種類に依存します。

データ、モデル、または列形式に関連するすべてのエラー メッセージは、モデルに関連付けられている基になる予測関数から返されます。

::: moniker range=">=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions"
## <a name="remarks"></a>解説

`PREDICT` 関数は、SQL Server 2017 以降のすべてのエディションで、Windows および Linux 上でサポートされています。 `PREDICT` を使用するために、[Machine Learning Services](../../machine-learning/sql-server-machine-learning-services.md) を有効にする必要はありません。
::: moniker-end

### <a name="supported-algorithms"></a>サポートされているアルゴリズム

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=sqlallproducts-allversions"
使用するモデルは、[RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) または [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) パッケージからサポートされているアルゴリズムのいずれかを使用して作成されている必要があります。 現在サポートされているモデルの一覧については、[PREDICT T-SQL 関数を使用したネイティブ スコアリング](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)に関するページを参照してください。
::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"
[ONNX](https://onnx.ai/) モデル形式に変換できるアルゴリズムがサポートされています。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
[ONNX](https://onnx.ai/) モデル形式、および[RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) または [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) パッケージからサポートされているアルゴリズムのいずれかを使用して作成したモデルに変換できるアルゴリズムがサポートされています。 RevoScaleR および revoscalepy で現在サポートされているアルゴリズムの一覧については、[PREDICT T-SQL 関数を使用したネイティブ スコアリング](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)に関するページを参照してください。
::: moniker-end

### <a name="permissions"></a>アクセス許可

`PREDICT` にはアクセス許可は必要ありませんが、ユーザーは、データベースに対する `EXECUTE` アクセス許可と、入力として使用される任意のデータをクエリするためのアクセス許可が必要です。 モデルがテーブルに格納されている場合、ユーザーはテーブルからモデルを読み込める必要もあります。

## <a name="examples"></a>例

次の例は、`PREDICT` を呼び出す構文を示しています。

### <a name="using-predict-in-a-from-clause"></a>FROM 句で PREDICT を使用する

この例では、`SELECT` ステートメントの `FROM` 句内の `PREDICT` 関数を参照します。

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @model,
    DATA = dbo.mytable AS d) WITH (Score FLOAT) AS p;
```

:::moniker-end

::: moniker range=">=azure-sqldw-latest||=sqlallproducts-allversions"

```sql
DECLARE @model VARBINARY(max) = (SELECT test_model FROM scoring_model WHERE model_id = 1);

SELECT d.*, p.Score
FROM PREDICT(MODEL = @model,
    DATA = dbo.mytable AS d) WITH (Score FLOAT) AS p;
```

::: moniker-end

`DATA` パラメーターでテーブル ソースに指定された別名 **d** は、`dbo.mytable` に属する列を参照するために使用されます。 `PREDICT` 関数に指定された別名 **p** は、`PREDICT` 関数によって返される列を参照するために使用されます。

- モデルは `varbinary(max)` 列として **Models** という名前のテーブルに格納されます。 モードを識別するために、**ID** や**説明**などの追加情報がテーブルに保存されます。
- `DATA` パラメーターでテーブル ソースに指定された別名 **d** は、`dbo.mytable` に属する列を参照するために使用されます。 入力データ列の名前は、モデルの入力名と一致している必要があります。
- `PREDICT` 関数に指定された別名 **p** は、`PREDICT` 関数によって返される予測される列を参照するために使用されます。 列名は、モデルの出力名と同じ名前にする必要があります。
- すべての入力データ列と予測される列は、SELECT ステートメントで表示できるようになります。

::: moniker range=">=azure-sqldw-latest||=sqlallproducts-allversions"

前の例のクエリは、スカラー サブクエリとして `MODEL` を指定することにより、ビューを作成するように書き換えることができます。

```sql
CREATE VIEW predictions
AS
SELECT d.*, p.Score
FROM PREDICT(MODEL = (SELECT test_model FROM scoring_model WHERE model_id = 1),
             DATA = dbo.mytable AS d) WITH (Score FLOAT) AS p;
```

:::moniker-end

### <a name="combining-predict-with-an-insert-statement"></a>PREDICT を INSERT ステートメントと結合する

予測の一般的なユース ケースは、入力データ用のスコアを生成してから、予測した値をテーブルに挿入する方法です。 次の例では、呼び出し元のアプリケーションがストアド プロシージャを使用して予測値を含む行をテーブルに挿入することを前提としています。

```sql
DECLARE @model VARBINARY(max) = (SELECT model FROM scoring_model WHERE model_name = 'ScoringModelV1');

INSERT INTO loan_applications (c1, c2, c3, c4, score)
SELECT d.c1, d.c2, d.c3, d.c4, p.score
FROM PREDICT(MODEL = @model, DATA = dbo.mytable AS d) WITH(score FLOAT) AS p;
```

- `PREDICT` の結果は、PredictionResults という名前のテーブルに格納されます。 
- モデルは `varbinary(max)` 列として **Models** という名前のテーブルに格納されます。 モデルを識別するために、ID や説明などの追加情報がテーブルに保存されます。
- `DATA` パラメーターのテーブル ソースに指定された別名 **d** は、`dbo.mytable` 内の列を参照するために使用されます。入力データ列の名前は、モデルの入力の名前と一致している必要があります。
- `PREDICT` 関数に指定された別名 **p** は、`PREDICT` 関数によって返される予測される列を参照するために使用されます。 列名は、モデルの出力名と同じ名前にする必要があります。
- すべての入力列と予測される列は、SELECT ステートメントで表示できるようになります。

## <a name="next-steps"></a>次のステップ

- [PREDICT T-SQL 関数を使用したネイティブ スコアリング](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)
::: moniker range="=azure-sqldw-latest||=azuresqldb-mi-current||=sqlallproducts-allversions"
-   [ONNX モデルの詳細情報](/azure/machine-learning/concept-onnx#get-onnx-models)
::: moniker-end
