---
title: クイック スタート:R スクリプトの実行
titleSuffix: SQL machine learning
description: SQL 機械学習を使用して、一連の単純な R スクリプトを実行します。 ストアド プロシージャ sp_execute_external_script を使用して、スクリプトを実行する方法について説明します。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: a924bca8acf50846f8b14053cc01a6a1a35f1617
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870380"
---
# <a name="quickstart-run-simple-r-scripts-with-sql-machine-learning"></a>クイック スタート:SQL 機械学習を使用して単純な R スクリプトを実行する
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) または[ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)を使用して、一連の単純な R スクリプトを実行します。 ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して、SQL Server インスタンスでスクリプトを実行する方法について説明します。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) を使用して、一連の単純な R スクリプトを実行します。 ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して、SQL Server インスタンスでスクリプトを実行する方法について説明します。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
このクイックスタートでは、[SQL Server R Services](../r/sql-server-r-services.md) を使用して、一連の単純な R スクリプトを実行します。 ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して、SQL Server インスタンスでスクリプトを実行する方法について説明します。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
このクイックスタートでは、[Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) を使用して、一連の単純な R スクリプトを実行します。 ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) を使用して、データベースでスクリプトを実行する方法について説明します。
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

## <a name="run-a-simple-script"></a>単純なスクリプトを実行する

R スクリプトを実行するには、それをシステム ストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) に引数として渡します。 このシステム ストアド プロシージャは、R ランタイムを起動し、R にデータを渡し、R ユーザー セッションを安全に管理し、結果をクライアントに返します。

以降の手順では、次のサンプル R スクリプトを実行します。

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. **Azure Data Studio** を開き、ご自身のサーバーに接続します。

1. 完全な R スクリプトを `sp_execute_external_script` ストアド プロシージャに渡します。

   このスクリプトは、`@script` 引数を通して渡されます。 `@script`引数内のすべては、有効な R コードである必要があります。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

1. 適切な結果が計算され、R の `print` 関数から **[メッセージ]** ウィンドウに結果が返されます。

   次のように表示されます。

    **結果**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Hello World スクリプトを実行する

一般的なスクリプトの例では、文字列 "Hello World" が出力されるだけです。 次のコマンドを実行します。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

`sp_execute_external_script`ストアド プロシージャへの入力は次のとおりです。

| 入力 | 説明 |
|-|-|
| @language | 呼び出す言語拡張機能 (この例では R) を定義します |
| @script | R ランタイムに渡されるコマンドを定義します この引数には R スクリプト全体を Unicode テキストとして含める必要があります。 **nvarchar** 型の変数にテキストを追加して、その変数を呼び出すこともできます |
| @input_data_1 | クエリによって返されるデータ。R ランタイムに渡され、そこからデータがデータ フレームとして返されます |
|結果セットを含む | 句では、返されるデータ テーブルのスキーマを定義し、列名として "Hello World" を追加し、データ型に **int** を追加します |

このコマンドは、次のテキストを出力します。

| Hello World |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>入力と出力を使用する

既定では、`sp_execute_external_script` は 1 つのデータセットを入力として受け入れます。通常は、有効な SQL クエリの形式で指定します。 次に、1 つの R データ フレームを出力として返します。

ここでは、`sp_execute_external_script` の既定の入力変数と出力変数を使用します。**InputDataSet** および **OutputDataSet**。

1. テスト データの小さなテーブルを作成します。

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

1. テーブルのクエリを実行するには、`SELECT` ステートメントを使用します。
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **結果**

    ![RTestData テーブルの内容](./media/select-rtestdata.png)

1. 次の R スクリプトを実行します。 `SELECT` ステートメントを使用してテーブルからデータを取得し、それを R ランタイムを介して渡し、データをデータ フレームとして返します。 `WITH RESULT SETS` 句では、SQL に対して返されたデータ テーブルのスキーマを定義して、列名 *NewColName* を追加します。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **結果**

    ![テーブルからデータを返す R スクリプトからの出力](./media/r-output-rtestdata.png)

1. 次に、入力変数と出力変数の名前を変更します。 既定の入力変数名と出力変数名は **InputDataSet** と **OutputDataSet** で、このスクリプトによって名前が **SQL_in** および **SQL_out** に変更されます。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    R では大文字と小文字が区別されることに注意してください。 R スクリプトで使用される入力変数と出力変数は (**SQL_out**、**SQL_in**)、大文字と小文字を区別して、`@input_data_1_name` と `@output_data_1_name` で定義されている名前と一致する必要があります。

   > [!TIP]
   > パラメーターとして渡すことができる入力データセットは 1 つだけです。また、返すことのできるデータセットも 1 つだけです。 ただし、R コード内から他のデータセットを呼び出し、そのデータセットに加えて、他の種類の出力を返すことができます。 任意のパラメーターに OUTPUT キーワードを追加することもでき、その場合は、パラメーターに結果が返されます。

1. 入力データを含まない R スクリプトを使用して値を生成することもできます (`@input_data_1` は空白に設定されます)。

   次のスクリプトは、 "hello" と "world" というテキストを出力します。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    mytextvariable <- c("hello", " ", "world");
    OutputDataSet <- as.data.frame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **結果**

    ![入力として @script を使用したクエリ結果](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>R バージョンの確認

インストールされている R のバージョンを確認する場合は、次のスクリプトを実行します。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

R `print` 関数は、**メッセージ** ウィンドウにバージョンを返します。 次の出力例では、R バージョン 3.4.4 がインストールされていることがわかります。

**結果**

```text
STDOUT message(s) from external script:
                   _
platform       x86_64-w64-mingw32
arch           x86_64
os             mingw32
system         x86_64, mingw32
status
major          3
minor          4.4
year           2018
month          03
day            15
svn rev        74408
language       R
version.string R version 3.4.4 (2018-03-15)
nickname       Someone to Lean On
```

## <a name="list-r-packages"></a>R パッケージの一覧表示
::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Microsoft では、Machine Learning Services と共にプレインストールされる R パッケージを多数提供しています。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Microsoft では、R Servicesと共にプレインストールされる R パッケージを多数提供しています。
::: moniker-end

バージョン、依存関係、ライセンス、ライブラリパスの情報など、インストールされている R パッケージの一覧を表示するには、次のスクリプトを実行します。

```SQL
EXEC sp_execute_external_script @language = N'R'
    , @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((
            Package NVARCHAR(255)
            , Version NVARCHAR(100)
            , Depends NVARCHAR(4000)
            , License NVARCHAR(1000)
            , LibPath NVARCHAR(2000)
            ));
```

出力は R の `installed.packages()` からのものであり、結果セットとして返されます。

**結果**

![R のインストール済みパッケージ](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>次のステップ

SQL 機械学習で R を使用する場合のデータ構造の使用方法については、次のクイックスタートを参照してください。

> [!div class="nextstepaction"]
> [SQL 機械学習での R を使用したデータ型とオブジェクトの処理](quickstart-r-data-types-and-objects.md)
