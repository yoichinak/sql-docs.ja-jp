---
title: クイック スタート:R データ構造体、データ型、およびオブジェクト
titleSuffix: SQL machine learning
description: このクイックスタートでは、SQL 機械学習で R を使用するときに、データ構造体、データ型、およびオブジェクトを使用する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 58eb68b94d5e969ef4a62d5de057d2936a628bda
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870371"
---
# <a name="quickstart-data-structures-data-types-and-objects-using-r-with-sql-machine-learning"></a>クイック スタート:SQL 機械学習での R を使用したデータ構造体、データ型、およびオブジェクト
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) または[ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)で R を使用するときに、データ構造体とデータ型を使用する方法について説明します。 R と SQL Server 間のデータの移動と、発生する可能性のある一般的な問題について説明します。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で R を使用するときに、データ構造体とデータ型を使用する方法について説明します。 R と SQL Server 間のデータの移動と、発生する可能性のある一般的な問題について説明します。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server R Services](../r/sql-server-r-services.md) で R を使用するときに、データ構造体とデータ型を使用する方法について説明します。 R と SQL Server 間のデータの移動と、発生する可能性のある一般的な問題について説明します。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
このクイックスタートでは、[Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) で R を使用する場合に、データ構造体とデータ型を使用する方法について説明します。 R と SQL Managed Instance 間のデータの移動と、発生する可能性のある一般的な問題について説明します。
::: moniker-end

前もって知っておくべき一般的な問題は、次のとおりです。

- データ型が一致しないときがある
- 暗黙的な変換が発生することがある
- cast および convert 操作が必要な場合がある
- R と SQL で異なるデータ オブジェクトが使用される

## <a name="prerequisites"></a>前提条件

このクイック スタートを実行するには、次の前提条件を用意しておく必要があります。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
- SQL Server Machine Learning Services。 Machine Learning Services をインストールするには、[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)または [Linux インストール ガイド](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)に関するページを参照してください。 [SQL Server ビッグ データ クラスターで Machine Learning Services を有効にする](../../big-data-cluster/machine-learning-services.md)こともできます。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
- SQL Server Machine Learning Services。 Machine Learning Services をインストールするには、[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)に関するページを参照してください。 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
- SQL Server 2016 R Services。 R Services をインストールするには、[Windows インストール ガイド](../install/sql-r-services-windows-install.md)に関するページを参照してください。 
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
- Azure SQL Managed Instance の Machine Learning Services。 詳細については、[Azure SQL Managed Instance の Machine Learning Services の概要](/azure/azure-sql/managed-instance/machine-learning-services-overview)に関するページを参照してください。
::: moniker-end

- R スクリプトを含む SQL クエリを実行するためのツール。 このクイックスタートでは [Azure Data Studio](../../azure-data-studio/what-is.md) を使用します。

## <a name="always-return-a-data-frame"></a>常にデータ フレームを返す

スクリプトが R から SQL Server に結果を返す場合は、データを **data.frame** として返す必要があります。 リスト、ファクター、ベクター、バイナリ データなど、スクリプトで生成するその他の種類のオブジェクトは、ストアド プロシージャ結果の一部として出力する場合はデータ フレームに変換する必要があります。 幸い、その他のオブジェクトのデータ フレームへの変更をサポートする複数の R 関数が存在します。 バイナリ モデルをシリアル化して、データ フレームに返すこともできます。この処理については、このクイックスタートで後述します。

最初に、R の基本的なオブジェクト (ベクトル、行列、リスト) を使用して、データ フレームへの変換によって SQL Server に渡す出力がどのように変わるかを見てみましょう。

次の 2 つの R で書かれた "Hello World" スクリプトを比較します。これらのスクリプトはほぼ同じものに見えますが、1 つ目は 3 つの値が含まれる 1 つの列を返し、2 つ目は 1 つの値が含まれる列を 3 つ返します。

**例 1**

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
     , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
     , @input_data_1 = N' ';
```

**例 2**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'
      , @input_data_1 = N'  ';
```

## <a name="identify-schema-and-data-types"></a>スキーマとデータ型の識別

なぜ結果がこれほど異なるのでしょうか。

答えは通常、R の `str()` コマンドを使用すればわかります。 指定の R オブジェクトのデータ スキーマが情報メッセージとして返されるよう、R スクリプトの任意の場所に関数 `str(object_name)` を追加します。

なぜ例 1 と例 2 の結果がこれほど異なるのかを理解するため、各ステートメントの `@script` 変数定義の最後に、行 `str(OutputDataSet)` を次のように挿入します。

**str 関数が追加された例 1**

```sql
EXECUTE sp_execute_external_script
        @language = N'R'
      , @script = N' mytextvariable <- c("hello", " ", "world");
      OutputDataSet <- as.data.frame(mytextvariable);
      str(OutputDataSet);'
      , @input_data_1 = N'  '
;
```

**str 関数を追加した例 2**

```sql
EXECUTE sp_execute_external_script
  @language = N'R', 
  @script = N' OutputDataSet <- data.frame(c("hello"), " ", c("world"));
    str(OutputDataSet);' , 
  @input_data_1 = N'  ';
```

次に、 **[メッセージ]** 内のテキストを確認して、なぜ出力が異なるのかを調べます。

**結果 - 例 1**

```sql
STDOUT message(s) from external script:
'data.frame':   3 obs. of  1 variable:
$ mytextvariable: Factor w/ 3 levels " ","hello","world": 2 1 3
```

**結果 - 例 2**

```sql
STDOUT message(s) from external script:
'data.frame':   1 obs. of  3 variables:
$ c..hello..: Factor w/ 1 level "hello": 1
$ X...      : Factor w/ 1 level " ": 1
$ c..world..: Factor w/ 1 level "world": 1
```

ご覧のように、R 構文をわずかに変更するだけで結果のスキーマに大きな影響がありました。 ここではその理由については説明しませんが、R データ型の違いについては、「[Hadley Wickham 氏による "Advanced R"](http://adv-r.had.co.nz)」の「*データ構造*」のセクションで詳しく説明されています。

現時点では、R オブジェクトをデータ フレームに強制変換するときは予想される結果を確認する必要がある、という点のみ注意してください。

> [!TIP]
> また、`is.matrix`、`is.vector` などの R の ID 関数を使用して、内部データ構造に関する情報を返すこともできます。

## <a name="implicit-conversion-of-data-objects"></a>データ オブジェクトの暗黙的な変換

各 R オブジェクトには、他のデータ オブジェクトと結合されたときに、その 2 つのデータ オブジェクトのディメンションの数が同じ場合、またはいずれかのデータ オブジェクトに異種データ型が含まれている場合、値がどのように扱われるのかについて独自のルールがあります。

まず、テスト データの小さなテーブルを作成します。

```sql
CREATE TABLE RTestData (col1 INT NOT NULL)

INSERT INTO RTestData
VALUES (1);

INSERT INTO RTestData
VALUES (10);

INSERT INTO RTestData
VALUES (100);
GO
```

たとえば、次のステートメントを実行し、R を使用して行列の乗算を行うとします。3 つの値を持つ 1 列の行列に 4 つの値を持つ配列を掛けると、結果として 4x3 行列が予想されます。

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:15);
    OutputDataSet <- as.data.frame(x %*% y);'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));
```

これにより、3 つの値の列が 1 列の行列に変換されます。 行列は単に R における配列の特殊なケースであるため、配列 `y` は暗黙的に、2 つの引数を一致させるために 1 列の行列に強制変換されます。

**結果**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|

ただし、配列 `y` のサイズを変更した場合に起こることについて注意してください。

```sql
execute sp_execute_external_script
   @language = N'R'
   , @script = N'
        x <- as.matrix(InputDataSet);
        y <- array(12:14);
   OutputDataSet <- as.data.frame(y %*% x);'
   , @input_data_1 = N' SELECT [Col1]  from RTestData;'
   WITH RESULT SETS (([Col1] int ));
```

この場合、結果として単一の値が R から返されます。

**結果**

|Col1|
|---|
|1542|

なぜですか? この場合、2 つの引数を同じ長さのベクターとして扱うことができるため、内積が 1 つの行列として R から返されます。  これは、線形代数のルールに従った想定どおりの動作です。ただし、ダウンストリーム アプリケーションで出力スキーマが変更されないと想定されている場合に問題が発生する可能性があります。

> [!TIP]
>
> エラーが発生しましたか？ **master** や別のデータベースではなく、テーブルが格納されているデータベースのコンテキストで、ストアド プロシージャを実行していることを確認してください。
>
> また、これらの例では一時テーブルを使用しないことをお勧めします。 一部の R クライアントは、バッチ間の接続を終了するときに、一時テーブルを削除します。

## <a name="merge-or-multiply-columns-of-different-length"></a>異なる長さの列のマージまたは乗算

R は、異なるサイズのベクトルを使用するため、およびそれらの列のような構造をデータ フレームに結合するために、優れた柔軟性を提供します。 ベクターのリストはテーブルのように見えますが、データベース テーブルに適用されるどのルールにも従いません。

たとえば、次のスクリプトでは、長さが 6 の数値の配列を定義し、R 変数 `df1` に格納します。 数値配列は、3 つの値を含む RTestData テーブルの整数と組み合わされ、新しいデータ フレーム `df2` が作成されます。

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
    , @script = N'
               df1 <- as.data.frame( array(1:6) );
               df2 <- as.data.frame( c( InputDataSet , df1 ));
               OutputDataSet <- df2'
    , @input_data_1 = N' SELECT [Col1]  from RTestData;'
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));
```

データ フレームを埋めるために、R は RTestData から取得した要素を、配列 `df1` 内の要素数と一致するために必要な数だけ繰り返します。

**結果**

|*Col2*|*Col3*|
|----|----|
|1|1|
|10|2|
|100|3|
|1|4|
|10|5|
|100|6|

データ フレームはテーブルのような外見ですが、実際はベクトルのリストであることを思い出してください。

## <a name="cast-or-convert-data"></a>データのキャストまたは変換

R と SQL Server は同じデータ型を使用しないため、データを取得して R ランタイムに渡すためのクエリを SQL Server で実行する際は、通常何らかの暗黙的な変換を行います。 R から SQL Server にデータを返す場合は、別の変換を行います。

- SQL Server は、Launchpad サービスで管理される R プロセスにクエリのデータをプッシュし、効率を向上させるために内部表現に変換します。
- R ランタイムでデータが data.frame 変数に読み込まれ、データに対して独自の操作が実行されます。
- データベース エンジンは、セキュリティで保護された内部接続を使用する SQL Server にデータを返し、SQL Server のデータ型の観点からデータを提供します。
- データを取得するには、SQL クエリを発行して表形式データ セットを処理できるクライアントまたはネットワーク ライブラリを使用して SQL Server に接続します。 このクライアント アプリケーションは、他の方法でデータに影響する可能性があります。

この動作を確認するには、このようなクエリを [AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks) データ ウェアハウス上で実行します。 このビューは、予測の作成に使用する売上データを返します。

```sql
USE AdventureWorksDW
GO

SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = 'M200 Europe'
           ORDER BY ReportingDate ASC
```

> [!NOTE]
>
> 任意のバージョンの AdventureWorks を使用することも、ご使用のデータベースを使用して別のクエリを作成することもできます。 ポイントとなるのは、テキスト、日時、および数値を含むデータを処理してみることです。

それでは、ストアド プロシージャへの入力として、このクエリを貼り付けてみてください。

```sql
EXECUTE sp_execute_external_script
       @language = N'R'
      , @script = N' str(InputDataSet);
      OutputDataSet <- InputDataSet;'
      , @input_data_1 = N'
           SELECT ReportingDate
         , CAST(ModelRegion as varchar(50)) as ProductSeries
         , Amount
           FROM [AdventureWorksDW].[dbo].[vTimeSeries]
           WHERE [ModelRegion] = ''M200 Europe''
           ORDER BY ReportingDate ASC ;'
WITH RESULT SETS undefined;
```

エラーが発生した場合、クエリ テキストの編集が必要になることがあります。 たとえば、WHERE 句内の文字列熟語は、2 つの一重引用符のセットで囲む必要があります。

クエリが動作したら、R で入力データがどのように扱われているかについて、`str` 関数の結果で確認します。

**結果**

```text
STDOUT message(s) from external script: 'data.frame':    37 obs. of  3 variables:
STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"
STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1
STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950
```

- 日時列は、R データ型 **POSIXct** を使用して処理されています。
- テキスト列 "ProductSeries" は、**factor**、つまりカテゴリ変数として識別されています。 文字列値は、既定ではファクターとして処理されます。 文字列を R に渡すと、内部使用のために整数に変換され、出力では文字列にマップし直されます。

### <a name="summary"></a>まとめ

このような短い例であっても、SQL クエリを入力として渡す場合はデータ変換の影響を確認する必要があることがわかります。 一部の SQL Server データ型は R でサポートされていないため、エラーを回避するために次の方法を検討してください。

- データを事前にテストし、R コードに渡したときに問題となる可能性がある、スキーマ内の列または値を確認します。
- 入力データ ソース内の列を指定する場合、`SELECT *` を使用するよりは、個別に指定して、各列がどのように処理されるかを理解します。
- 予想外の問題を回避するために、入力データを準備するときに、必要に応じて明示的なキャストを実行します。
- エラー発生の原因となりモデリングの役に立たない (GUID や rowguid などの) データの列を渡すことを回避します。

サポート対象およびサポート対象外のデータ型について詳しくは、「[R ライブラリとデータ型](../r/r-libraries-and-data-types.md)」に関するページを参照してください。

## <a name="next-steps"></a>次のステップ

SQL 機械学習で高度な R 関数を作成する方法については、次のクイックスタートを参照してください。

> [!div class="nextstepaction"]
> [SQL 機械学習を使用した高度な R 関数の作成](quickstart-r-functions.md)
