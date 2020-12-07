---
title: クイック スタート:Python スクリプトを実行する
titleSuffix: SQL machine learning
description: SQL Server、ビッグ データ クラスター、Azure SQL Managed Instances 上の SQL Server Machine Learning Services を使用して、一連の単純な Python スクリプトを実行します。 ストアド プロシージャ sp_execute_external_script を使用して、スクリプトを実行する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/28/2020
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.custom: contperfq1
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 9f2b729273362afd7a14cb60434416996b186557
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870169"
---
# <a name="quickstart-run-simple-python-scripts-with-sql-machine-learning"></a>クイック スタート:SQL 機械学習を使用して単純な Python スクリプトを実行する
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

このクイックスタートでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)、[Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)、[SQL Server ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)を使用して、一連の単純な Python スクリプトを実行します。 ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して、SQL Server インスタンスでスクリプトを実行する方法について説明します。

## <a name="prerequisites"></a>前提条件

このクイック スタートを実行するには、次の前提条件を用意しておく必要があります。

- 次のいずれかのプラットフォーム上の SQL データベース:
  - [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)。 インストールするには、[Windows インストール ガイド](../install/sql-machine-learning-services-windows-install.md)または [Linux インストール ガイド](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)に関するページを参照してください。
  - SQL Server ビッグ データ クラスター。 [SQL Server ビッグ データ クラスターで Machine Learning Services を有効にする](../../big-data-cluster/machine-learning-services.md)方法に関するページを参照してください。
  - Azure SQL Managed Instance の Machine Learning Services。 詳細については、[Azure SQL Managed Instance の Machine Learning Services の概要](/azure/azure-sql/managed-instance/machine-learning-services-overview)に関するページを参照してください。

- Python スクリプトを含む SQL クエリを実行するためのツールです。 このクイックスタートでは [Azure Data Studio](../../azure-data-studio/what-is.md) を使用します。

## <a name="run-a-simple-script"></a>単純なスクリプトを実行する

Python スクリプトを実行するには、これを引数としてシステム ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) に渡します。 このシステム ストアド プロシージャを使用して、SQL 機械学習のコンテキストで Python ランタイムを起動し、データを Python に渡し、Python ユーザー セッションを安全に管理し、何らかの結果をクライアントに返します。

以降の手順では、次に例示する Python スクリプトをデータベースで実行します。

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. SQL インスタンスに接続された **Azure Data Studio** で新しいクエリ ウィンドウを開きます。

1. 完全な Python スクリプトを `sp_execute_external_script` ストアド プロシージャに渡します。

   このスクリプトは、`@script` 引数を通して渡されます。 `@script` 引数内のすべては、有効な Python コードである必要があります。

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

1. 正しい結果が計算され、Python `print` 関数によって **Messages** ウィンドウに結果が返されます。

   次のように表示されます。

    **結果**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Hello World スクリプトを実行する

一般的なスクリプトの例では、文字列 "Hello World" が出力されるだけです。 次のコマンドを実行します。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'OutputDataSet = InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

`sp_execute_external_script`ストアド プロシージャへの入力は次のとおりです。

| 入力 | 説明 |
|-|-|
| @language | 呼び出す言語拡張機能 (この例では Python) を定義します |
| @script | Python ランタイムに渡されるコマンドを定義します Python 全体は、Unicode テキストとして、この引数で囲まれている必要があります。 **nvarchar** 型の変数にテキストを追加して、その変数を呼び出すこともできます |
| @input_data_1 | クエリによって返されるデータ。Python ランタイムに渡され、そこからデータがデータ フレームとして返されます |
| 結果セットを含む | 句では、SQL 機械学習に対して返されるデータ テーブルのスキーマを定義し、列名として "Hello World" を追加し、データ型に **int** を追加します |

このコマンドは、次のテキストを出力します。

| Hello World |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>入力と出力を使用する

既定では、`sp_execute_external_script` は 1 つのデータセットを入力として受け入れます。通常は、有効な SQL クエリの形式で指定します。 次に、1 つの Python データ フレームを出力として返します。

ここでは、`sp_execute_external_script` の既定の入力変数と出力変数を使用します。**InputDataSet** および **OutputDataSet**。

1. テスト データの小さなテーブルを作成します。

    ```sql
    CREATE TABLE PythonTestData (col1 INT NOT NULL)
    
    INSERT INTO PythonTestData
    VALUES (1);
    
    INSERT INTO PythonTestData
    VALUES (10);
    
    INSERT INTO PythonTestData
    VALUES (100);
    GO
    ```

1. テーブルのクエリを実行するには、`SELECT` ステートメントを使用します。
  
    ```sql
    SELECT *
    FROM PythonTestData
    ```

    **結果**

    ![PythonTestData テーブルの内容](./media/select-pythontestdata.png)

1. 次の Python スクリプトを実行します。 `SELECT` ステートメントを使用してテーブルからデータを取得し、それを Python ランタイムを介して渡し、データをデータ フレームとして返します。 `WITH RESULT SETS` 句では、SQL に対して返されたデータ テーブルのスキーマを定義して、列名 *NewColName* を追加します。

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **結果**

    ![テーブルからデータを返す Python スクリプトからの出力](./media/python-output-pythontestdata.png)

1. 次に、入力変数と出力変数の名前を変更します。 既定の入力変数名と出力変数名は **InputDataSet** と **OutputDataSet** で、次のスクリプトによって名前が **SQL_in** および **SQL_out** に変更されます。

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'SQL_out = SQL_in;'
        , @input_data_1 = N'SELECT 12 as Col;'
        , @input_data_1_name  = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Python では大文字と小文字が区別されることに注意してください。 Python スクリプトで使用される入力変数と出力変数は (**SQL_out**、**SQL_in**)、大文字と小文字を区別して、`@input_data_1_name` と `@output_data_1_name`で定義されている名前と一致する必要があります。

    > [!TIP]
    > パラメーターとして渡すことができる入力データセットは 1 つだけです。また、返すことのできるデータセットも 1 つだけです。 ただし、Python コード内から他のデータセットを呼び出し、データセットに加えて他の型の出力を返すことができます。 任意のパラメーターに OUTPUT キーワードを追加することもでき、その場合は、パラメーターに結果が返されます。

1. 入力データを含まない Python スクリプトを使用して値を生成することもできます (`@input_data_1` は空白に設定されます)。

    次のスクリプトは、 "hello" と "world" というテキストを出力します。

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    import pandas as pd
    mytextvariable = pandas.Series(["hello", " ", "world"]);
    OutputDataSet = pd.DataFrame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **結果**

    ![入力として @script を使用したクエリ結果](./media/python-data-generated-output.png)

> [!NOTE]
> Python では、先頭のスペースを使用してステートメントをグループ化します。 そのため、前述のスクリプトのように、埋め込まれた Python スクリプトが複数の行にまたがる場合は、SQL コマンドに合わせるために Python コマンドにインデントを設定しようとしないでください。 たとえば、次のスクリプトでは次のエラーが生成されます。
>
> ```sql
> EXECUTE sp_execute_external_script @language = N'Python'
>       , @script = N'
>       import pandas as pd
>       mytextvariable = pandas.Series(["hello", " ", "world"]);
>       OutputDataSet = pd.DataFrame(mytextvariable);
>       '
>       , @input_data_1 = N''
> WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
> ```

## <a name="check-python-version"></a>Python バージョンの確認

サーバーにインストールされている Python のバージョンを確認するには、次のスクリプトを実行します。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

Python `print` 関数は、**Messages** ウィンドウにバージョンを返します。 次の出力例では、この場合、Python バージョン 3.5.2 がインストールされていることが分かります。

**結果**

```text
STDOUT message(s) from external script:
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>Python パッケージを一覧表示します

Microsoft では、Machine Learning Services と共にプレインストールされる Python パッケージを多数提供しています。

バージョンなど、インストールされている Python パッケージの一覧を表示するには、次のスクリプトを実行します。

```SQL
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import pkg_resources
import pandas
dists = [str(d) for d in pkg_resources.working_set]
OutputDataSet = pandas.DataFrame(dists)
'
WITH RESULT SETS(([Package] NVARCHAR(max)))
GO
```

この一覧は Python の `pkg_resources.working_set` からのものであり、データ フレームとして SQL に返されます。

**結果**

:::image type="content" source="media/python-package-list.png" alt-text="インストールされている Python パッケージの一覧":::

## <a name="next-steps"></a>次のステップ

SQL 機械学習で Python を使用する場合のデータ構造の使用方法については、次のクイックスタートを参照してください。

> [!div class="nextstepaction"]
> [クイック スタート: Python を使用したデータ構造とオブジェクト](quickstart-python-data-structures.md)
