---
title: クイック スタート:Python 関数
titleSuffix: SQL machine learning
description: このクイックスタートでは、SQL 機械学習で Python の数学関数とユーティリティ関数を使用する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/28/2020
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: edd4ec79799cbb62c32c70a9d40236ffd4a76b73
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870014"
---
# <a name="quickstart-python-functions-with-sql-machine-learning"></a>クイック スタート:SQL 機械学習を使用した Python 関数
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

このクイックスタートでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)、[Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)、[SQL Server ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)で Python の数学関数とユーティリティ関数を使用する方法について説明します。 多くの場合、統計関数は T-SQL での実装が複雑ですが、Python では、わずか数行のコードで行うことができます。

## <a name="prerequisites"></a>前提条件

このクイック スタートを実行するには、次の前提条件を用意しておく必要があります。

- 次のいずれかのプラットフォーム上の SQL データベース:
  - [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)。 インストールするには、[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)または [Linux インストール ガイド](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)に関するページを参照してください。
  - SQL Server ビッグ データ クラスター。 [SQL Server ビッグ データ クラスターで Machine Learning Services を有効にする](../../big-data-cluster/machine-learning-services.md)方法に関するページを参照してください。
  - Azure SQL Managed Instance の Machine Learning Services。 詳細については、[Azure SQL Managed Instance の Machine Learning Services の概要](/azure/azure-sql/managed-instance/machine-learning-services-overview)に関するページを参照してください。

- Python スクリプトを含む SQL クエリを実行するためのツールです。 このクイックスタートでは [Azure Data Studio](../../azure-data-studio/what-is.md) を使用します。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>乱数を生成するストアド プロシージャを作成する

わかりやすくするために、既定でインストールされて読み込まれる Python `numpy` パッケージを使用してみましょう。 パッケージには、一般的な統計タスク用の数百の関数が含まれますが、その中の `random.normal` 関数は、指定された標準偏差と平均に対し、正規分布を使用して、指定された個数の乱数を生成します。

たとえば、次の Python コードは、指定された 3 の標準偏差で、平均値が 50 の 100 個の数値を返します。

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

この Python の行を T-SQL から呼び出すには、`sp_execute_external_script` の Python スクリプト パラメーターに Python 関数を追加します。 出力にはデータ フレームが必要であるため、`pandas` を使用して変換します。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=100, loc=50, scale=3));
'
    , @input_data_1 = N'   ;'
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

さまざまな乱数のセットを簡単に生成するにはどうすればよいでしょうか。 ユーザーから引数を取得し、これらの引数を変数として Python スクリプトに渡すストアド プロシージャを定義します。

```sql
CREATE PROCEDURE MyPyNorm (
      @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=mynumbers, loc=mymean, scale=mysd));
'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- 最初の行は、ストアド プロシージャを実行するときに必要になる SQL 入力パラメーターそれぞれを定義します。

- `@params` で始まる行は、Python コードで使用されるすべての変数と、対応する SQL データ型を定義します。

- それに続く行は、SQL パラメーター名を対応する Python 変数名にマップします。

ストアド プロシージャで Python 関数をラップしたので、次のように関数を簡単に呼び出し、別の値を渡すことができます。

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>トラブルシューティングのための Python ユーティリティ関数の使用

Python パッケージは、現在の Python 環境を調査するためのさまざまなユーティリティ関数を提供します。 これらの関数は、SQL Server と外部環境で Python コードが実行する方法に不一致が見つかった場合に役立つ可能性があります。

たとえば、`time` パッケージでシステム タイミング関数を使用して、Python プロセスによって使用される時間を計測し、パフォーマンスの問題を分析することができます。

```sql
EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
import time
start_time = time.time()

# Run Python processes

elapsed_time = time.time() - start_time
'
    , @input_data_1 = N' ;';
```

## <a name="next-steps"></a>次のステップ

SQL 機械学習で Python を使用して機械学習モデルを作成するには、次のクイック スタートに従ってください。

> [!div class="nextstepaction"]
> [クイック スタート: Python で予測モデルを作成してスコア付けする](quickstart-python-train-score-model.md)
