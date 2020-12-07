---
title: クイック スタート:R 関数
titleSuffix: SQL machine learning
description: このクイックスタートでは、SQL 機械学習で R の数学関数とユーティリティ関数を使用する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 2851ab1723e83b675b6659412e7e279700a6f5ac
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870364"
---
# <a name="quickstart-r-functions-with-sql-machine-learning"></a>クイック スタート:SQL 機械学習を使用した R 関数
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) または[ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)で R の数学関数とユーティリティ関数を使用する方法について説明します。 多くの場合、統計関数は T-SQL での実装が複雑ですが、R では、わずか数行のコードで行うことができます。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で R の数学関数とユーティリティ関数を使用する方法について説明します。 多くの場合、統計関数は T-SQL での実装が複雑ですが、R では、わずか数行のコードで行うことができます。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server R Services](../r/sql-server-r-services.md) で R の数学関数とユーティリティ関数を使用する方法について説明します。 多くの場合、統計関数は T-SQL での実装が複雑ですが、R では、わずか数行のコードで行うことができます。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
このクイックスタートでは、[Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) で R を使用する場合に、データ構造体とデータ型を使用する方法について説明します。 R と SQL Managed Instance 間のデータの移動と、発生する可能性のある一般的な問題について説明します。
::: moniker-end

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

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>乱数を生成するストアド プロシージャを作成する

わかりやすくするために、既定でインストールされて読み込まれる R `stats` パッケージを使用してみましょう。 パッケージには、一般的な統計タスク用の数百の関数が含まれますが、その中の `rnorm` 関数は、指定された標準偏差と平均に対し、正規分布を使用して、指定された個数の乱数を生成します。

たとえば、次の R コードは、指定された 3 の標準偏差で、平均値が 50 の 100 個の数値を返します。

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

この R の行を T-SQL から呼び出すには、次のように、`sp_execute_external_script` の R スクリプト パラメーターに R 関数を追加します。

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

さまざまな乱数のセットを簡単に生成するにはどうすればよいでしょうか。

T-SQL と組み合わせれば簡単です。 ユーザーから引数を取得し、これらの引数を変数として R スクリプトに渡すストアド プロシージャを定義します。

```sql
CREATE PROCEDURE MyRNorm (
    @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- 最初の行は、ストアド プロシージャを実行するときに必要になる SQL 入力パラメーターそれぞれを定義します。

- `@params` で始まる行は、R コードで使用されるすべての変数と対応する SQL データ型を定義します。

- すぐ後に続く行では、SQL パラメーター名と対応する R 変数名をマップします。

これでストアド プロシージャに R 関数がラップされたため、次のように関数を簡単に呼び出してさまざまな値を渡すことができます。

```sql
EXECUTE MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>トラブルシューティングのために R ユーティリティ関数を使用する

既定では、**utils** パッケージが含まれます。このパッケージは、現在の R 環境を調査するためのさまざまなユーティリティ関数を提供します。 これらの関数は、SQL Server と外部環境で R コードが実行する方法に不一致が見つかった場合に役立つ可能性があります。

たとえば、`system.time` や `proc.time` など、R のシステム タイミング関数を使用して、R プロセスによって使用される時間をキャプチャし、パフォーマンスの問題を分析することがあります。 例については、「[データ機能の作成](../tutorials/walkthrough-create-data-features.md)」チュートリアルを参照してください。R タイミング関数がソリューションに埋め込まれています。

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        start.time <- proc.time();
        
        # Run R processes
        
        elapsed_time <- proc.time() - start.time;'
```

その他の有用な関数については、「[R コード プロファイル関数を使用してパフォーマンスを向上させる](../r/using-r-code-profiling-functions.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

SQL 機械学習で R を使用して機械学習モデルを作成するには、次のクイック スタートに従ってください。

> [!div class="nextstepaction"]
> [SQL 機械学習を使用して R で予測モデルを作成してスコア付けする](quickstart-r-train-score-model.md)
