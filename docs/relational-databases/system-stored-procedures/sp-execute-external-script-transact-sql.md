---
description: sp_execute_external_script (Transact-SQL)
title: sp_execute_external_script (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning-services
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 7953c9aafda19182395311b7adc648c04d5c1f39
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155078"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**Sp_execute_external_script**ストアドプロシージャは、プロシージャへの入力引数として指定されたスクリプトを実行し、 [Machine Learning Services](../../machine-learning/sql-server-machine-learning-services.md)および[言語拡張](../../language-extensions/language-extensions-overview.md)と共に使用されます。 

Machine Learning Services の場合、 [Python](../../machine-learning/concepts/extension-python.md) と [R](../../machine-learning/concepts/extension-r.md) はサポートされている言語です。 言語拡張の場合、Java はサポートされていますが、 [CREATE EXTERNAL Language](../../t-sql/statements/create-external-language-transact-sql.md)を使用して定義する必要があります。

**Sp_execute_external_script**を実行するには、まず Machine Learning Services または言語拡張機能をインストールする必要があります。 詳細については、Windows および[linux](../../linux/sql-server-linux-setup-machine-learning.md)[に SQL Server Machine Learning Services (Python および R) をインストール](../../machine-learning/install/sql-machine-learning-services-windows-install.md)するか、windows および[Linux](../../linux/sql-server-linux-setup-language-extensions-java.md)[に SQL Server 言語拡張機能をインストール](../../language-extensions/install/windows-java.md)してください。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
**Sp_execute_external_script**ストアドプロシージャは、プロシージャへの入力引数として指定されたスクリプトを実行し、SQL Server 2017 で[Machine Learning Services](../../machine-learning/sql-server-machine-learning-services.md)と共に使用されます。

Machine Learning Services の場合、 [Python](../../machine-learning/concepts/extension-python.md) と [R](../../machine-learning/concepts/extension-r.md) はサポートされている言語です。

**Sp_execute_external_script**を実行するには、まず Machine Learning Services をインストールする必要があります。 詳細については、「 [Install SQL Server Machine Learning Services (Python および R) On Windows](../../machine-learning/install/sql-machine-learning-services-windows-install.md)」を参照してください。
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**Sp_execute_external_script**ストアドプロシージャは、プロシージャへの入力引数として指定されたスクリプトを実行し、SQL Server 2016 の[R Services](../../machine-learning/r/sql-server-r-services.md)と共に使用されます。

R Services の場合、サポートされている言語は  [r](../../machine-learning/concepts/extension-r.md) です。

**Sp_execute_external_script**を実行するには、最初に R Services をインストールする必要があります。 詳細については、「 [Install SQL Server Machine Learning Services (Python および R) On Windows](../../machine-learning/install/sql-r-services-windows-install.md)」を参照してください。
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
**Sp_execute_external_script**ストアドプロシージャは、プロシージャへの入力引数として指定されたスクリプトを実行し、 [Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)と共に使用されます。

Machine Learning Services の場合、 [Python](../../machine-learning/concepts/extension-python.md) と [R](../../machine-learning/concepts/extension-r.md) はサポートされている言語です。

**Sp_execute_external_script**を実行するには、まず Machine Learning Services を有効にする必要があります。 詳細については、 [AZURE SQL Managed Instance ドキュメントの Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)を参照してください。
::: moniker-end

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
## <a name="syntax"></a>構文

```
sp_execute_external_script
    @language = N'language',
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]
    [ , @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2017-and-earlier"></a>SQL Server 2017 以前の構文

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end

## <a name="arguments"></a>引数
 ** \@ language** = N '*language*'  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 スクリプト言語を示します。 *言語* は **sysname**です。 有効な値は、 **R**、 **Python**、および [CREATE EXTERNAL language](../../t-sql/statements/create-external-language-transact-sql.md) (Java など) で定義されている任意の言語です。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 スクリプト言語を示します。 *言語* は **sysname**です。 SQL Server 2017 では、有効な値は **R** および **Python**です。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 スクリプト言語を示します。 *言語* は **sysname**です。 SQL Server 2016 では、有効な値は **R**のみです。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
 スクリプト言語を示します。 *言語* は **sysname**です。 Azure SQL Managed Instance では、有効な値は **R** および **Python**です。
::: moniker-end

 ** \@ スクリプト**= N '*script*' 外部言語スクリプトがリテラルまたは変数入力として指定されています。 *スクリプト* は **nvarchar (max)** です。  

`[ @input_data_1 =  N'input_data_1' ]` 外部スクリプトによって使用される入力データをクエリの形式で指定し [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。 *Input_data_1*のデータ型は**nvarchar (max)** です。

`[ @input_data_1_name = N'input_data_1_name' ]` によって定義されたクエリを表すために使用する変数の名前を指定し @input_data_1 ます。 外部スクリプトの変数のデータ型は、言語によって異なります。 R の場合、入力変数はデータフレームです。 Python の場合、入力は表形式である必要があります。 *input_data_1_name* は **sysname**です。  既定値は *Inputdataset*です。  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` パーティションごとのモデルを構築するために使用されます。 結果セットの順序付けに使用する列の名前を指定します。たとえば、製品名を使用します。 外部スクリプトの変数のデータ型は、言語によって異なります。 R の場合、入力変数はデータフレームです。 Python の場合、入力は表形式である必要があります。

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` パーティションごとのモデルを構築するために使用されます。 地理的領域や日付など、データのセグメント化に使用する列の名前を指定します。 外部スクリプトの変数のデータ型は、言語によって異なります。 R の場合、入力変数はデータフレームです。 Python の場合、入力は表形式である必要があります。 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ストアドプロシージャの呼び出しの完了時に返されるデータを含む外部スクリプト内の変数の名前を指定します。 外部スクリプトの変数のデータ型は、言語によって異なります。 R の場合、出力はデータフレームである必要があります。 Python の場合、出力はパンダのデータフレームである必要があります。 *output_data_1_name* は **sysname**です。  既定値は *Outputdataset*です。  

`[ @parallel = 0 | 1 ]` パラメーターを1に設定して、R スクリプトの並列実行を有効にし `@parallel` ます。 このパラメーターの既定値は 0 (並列処理なし) です。 `@parallel = 1`と出力がクライアントコンピューターに直接ストリーミングされている場合は、 `WITH RESULT SETS` 句が必要であり、出力スキーマを指定する必要があります。  

 + RevoScaleR 関数を使用しない R スクリプトの場合、パラメーターを使用すると、スクリプトを普通に並列化できると仮定して、  `@parallel` 大規模なデータセットを処理するのに役立ちます。 たとえば、R 関数をモデルと共に使用して新しい予測を生成する場合は `predict` 、を `@parallel = 1` クエリエンジンにヒントとして設定します。 クエリを並列化できる場合、行は **MAXDOP** の設定に従って分散されます。  
  
 + RevoScaleR 関数を使用する R スクリプトの場合、並列処理は自動的に処理されるため、 `@parallel = 1` **sp_execute_external_script** の呼び出しにはを指定しないでください。  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` 外部スクリプトで使用される入力パラメーター宣言の一覧。  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` 外部スクリプトによって使用される入力パラメーターの値の一覧です。  

## <a name="remarks"></a>解説

> [!IMPORTANT]
> クエリツリーは SQL machine learning によって制御され、ユーザーはクエリに対して任意の操作を実行できません。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
サポートされている言語で記述されたスクリプトを実行するには、 **sp_execute_external_script** を使用します。 サポートされている言語は、Machine Learning Services で使用される **Python** と **R** 、および言語拡張機能で使用される [CREATE EXTERNAL language](../../t-sql/statements/create-external-language-transact-sql.md) (Java など) で定義されているすべての言語です。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
サポートされている言語で記述されたスクリプトを実行するには、 **sp_execute_external_script** を使用します。 サポートされている言語は SQL Server 2017 Machine Learning Services の **Python** および **R** です。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
サポートされている言語で記述されたスクリプトを実行するには、 **sp_execute_external_script** を使用します。 サポートされている言語は SQL Server 2016 R Services の **r** のみです。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
サポートされている言語で記述されたスクリプトを実行するには、 **sp_execute_external_script** を使用します。 サポートされている言語は、Azure SQL Managed Instance Machine Learning Services の **Python** と **R** です。
::: moniker-end

既定では、このストアドプロシージャによって返される結果セットには、名前のない列が出力されます。 スクリプト内で使用される列名は、スクリプト環境に対してローカルであり、出力される結果セットには反映されません。 結果セットの列に名前を設定するには、の句を使用し `WITH RESULT SET` [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md) ます。

結果セットを返すだけでなく、出力パラメーターを使用してスカラー値を返すこともできます。

::: moniker range=">=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions"
外部リソースプールを構成することによって、外部スクリプトによって使用されるリソースを制御できます。 詳細については、「[CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)」を参照してください。 ワークロードに関する情報は、リソースガバナーのカタログビュー、DMV の、およびカウンターから取得できます。 詳細については、「 [Resource Governor カタログビュー &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)」、 [Resource Governor 関連する動的管理ビュー &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)、および [SQL Server External Scripts オブジェクト](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)」を参照してください。  
::: moniker-end

### <a name="monitor-script-execution"></a>スクリプトの実行の監視

[Sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)と[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)を使用してスクリプトの実行を監視します。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>パーティションモデリングのパラメーター

パーティション分割されたデータでのモデリングを可能にする2つの追加パラメーターを設定できます。この場合、パーティションは、指定した1つ以上の列に基づいて作成され、スクリプトの実行中にのみ使用される論理パーティションにデータセットを分割します。 年齢、性別、地域、日付、または時刻の繰り返し値を含む列は、パーティション分割されたデータセットに適したいくつかの例です。

2つのパラメーター **input_data_1_partition_by_columns** と **input_data_1_order_by_columns**で、2番目のパラメーターを使用して結果セットを並べ替えます。 パラメーターは、 `sp_execute_external_script` すべてのパーティションに対して1回実行される外部スクリプトを使用して、入力として渡されます。 詳細と例については、「 [チュートリアル: パーティションベースのモデルを作成する](../../machine-learning/tutorials/r-tutorial-create-models-per-partition.md)」を参照してください。

を指定することにより、スクリプトを並列で実行でき `@parallel=1` ます。 入力クエリを並列化できる場合は、 `@parallel=1` 引数の一部としてをに設定する必要があり `sp_execute_external_script` ます。 既定では、クエリオプティマイザーは `@parallel=1` 256 行を超えるテーブルで動作しますが、これを明示的に処理する場合、このスクリプトにはパラメーターがデモンストレーションとして含まれます。

> [!Tip]
> トレーニング ワークロードの場合、Microsoft-rx 以外のアルゴリズムを使用している場合でも、任意のトレーニング スクリプトで `@parallel` を使用できます。 通常、SQL Server のトレーニング シナリオで並列処理が提供されるのは、RevoScaleR アルゴリズム (rx プレフィックスが付いたもの) だけです。 ただし、SQL Server 2019 以降の新しいパラメーターを使用すると、その機能を使用して特に設計されていない関数を呼び出すスクリプトを並列化できます。
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Python および R スクリプトのストリーミング実行  

ストリーミングを使用すると、Python または R スクリプトは、メモリに収まりきらないデータを処理できます。 ストリーミング中に渡される行の数を制御するには、コレクション内のパラメーターに整数値を指定し `@r_rowsPerRead` `@params` ます。  たとえば、非常に幅の広いデータを使用するモデルをトレーニングする場合、1つのデータチャンクですべての行を確実に送信できるようにするために、値を小さくして読み取る行を減らすことができます。 また、このパラメーターを使用して、サーバーのパフォーマンスの問題を軽減するために、一度に読み取られて処理される行の数を管理することもできます。 
  
`@r_rowsPerRead`ストリーミングのパラメーターと引数の両方を `@parallel` ヒントと見なす必要があります。 ヒントを適用するには、並列処理を含む SQL クエリプランを生成できる必要があります。 これが不可能な場合は、並列処理を有効にできません。  
  
> [!NOTE]  
> ストリーミングと並列処理は、Enterprise Edition でのみサポートされています。 標準エディションのクエリには、エラーを発生させることなくパラメーターを含めることができますが、パラメーターが無効になり、R スクリプトが1つのプロセスで実行されます。  
  
## <a name="restrictions"></a>制限  

### <a name="data-types"></a>データ型

次のデータ型は、 **sp_execute_external_script** プロシージャの入力クエリまたはパラメーターで使用されている場合はサポートされません。また、サポートされていない型エラーを返します。  

回避策として、列または値をのサポートされている型に **キャスト** してから、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 外部スクリプトに送信します。  
  
+ **cursor**  
  
+ **timestamp**  
  
+ **datetime2**、 **datetimeoffset**、 **time**  
  
+ **sql_variant**  
  
+ **text**、 **image**  
  
+ **xml**  
  
+ **hierarchyid**、 **geometry**、 **geography**  
  
+ CLR ユーザー定義型

一般に、データ型にマップできない結果セット [!INCLUDE[tsql](../../includes/tsql-md.md)] は、NULL として出力されます。  

### <a name="restrictions-specific-to-r"></a>R に固有の制限事項

入力に、R の許容範囲の値に適合しない **datetime** 値が含まれている場合、値は **NA**に変換されます。 SQL machine learning では、R 言語でサポートされているよりも広い範囲の値が許可されるため、この方法が必要になります。

Float 値 (たとえば、、 `+Inf` 、 `-Inf` `NaN` ) は、両方の言語で IEEE 754 が使用されている場合でも、SQL machine learning ではサポートされません。 現在の動作では、値が直接 SQL に送信されます。その結果、SQL クライアントからエラーがスローされます。 そのため、これらの値は **NULL**に変換されます。

## <a name="permissions"></a>アクセス許可

**すべての外部スクリプトデータベースの実行**権限が必要です。  

## <a name="examples"></a>使用例

このセクションでは、を使用して、このストアドプロシージャを使用して R または Python スクリプトを実行する方法の例について説明 [!INCLUDE[tsql](../../includes/tsql-md.md)] します。

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. R データセットを SQL Server に返す  

次の例では、 **sp_execute_external_script** を使用して、R に含まれる虹彩データセットを返すストアドプロシージャを作成します。  

```sql
DROP PROC IF EXISTS get_iris_dataset;  
go  
CREATE PROC get_iris_dataset
AS  
BEGIN  
 EXEC   sp_execute_external_script  
       @language = N'R'  
     , @script = N'iris_data <- iris;'
     , @input_data_1 = N''  
     , @output_data_1_name = N'iris_data'
     WITH RESULT SETS (("Sepal.Length" float not null,
           "Sepal.Width" float not null,  
        "Petal.Length" float not null,
        "Petal.Width" float not null, "Species" varchar(100)));  
END;
GO
```

### <a name="b-create-a-python-model-and-generate-scores-from-it"></a>B. Python モデルを作成し、それからスコアを生成する

この例では、を使用し `sp_execute_external_script` て、単純な Python モデルでスコアを生成する方法を示します。

```sql
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

-- Input query to generate the customer data
DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders'

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

# Get data from input query
customer_data = my_input_data

# Define the model
n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

Python コードで使用される列見出しは SQL Server に出力されません。したがって、SQL で使用する列の名前とデータ型を指定するには、WITH RESULT ステートメントを使用します。

::: moniker range=">=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="c-generate-an-r-model-based-on-data-from-sql-server"></a>C. SQL Server からのデータに基づいて R モデルを生成する  

次の例では、 **sp_execute_external_script** を使用して、虹彩モデルを生成し、モデルを返すストアドプロシージャを作成します。  

> [!NOTE]
> この例では、e1071 パッケージを事前にインストールする必要があります。 詳細については、「 [SQL Server に追加の R パッケージをインストール](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)する」を参照してください。

```sql
DROP PROC IF EXISTS generate_iris_model;
GO
CREATE PROC generate_iris_model
AS
BEGIN
 EXEC sp_execute_external_script  
      @language = N'R'  
     , @script = N'  
          library(e1071);  
          irismodel <-naiveBayes(iris_data[,1:4], iris_data[,5]);  
          trained_model <- data.frame(payload = as.raw(serialize(irismodel, connection=NULL)));  
'  
     , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from iris_data'  
     , @input_data_1_name = N'iris_data'  
     , @output_data_1_name = N'trained_model'  
    WITH RESULT SETS ((model varbinary(max)));  
END;
GO
```

Python を使って似たモデルを生成するには、言語識別子を `@language=N'R'` から `@language = N'Python'` に変更し、`@script` 引数を必要に応じて修正します。 そうしないと、すべてのパラメーターが R と同じように機能します。
::: moniker-end

スコアリングには、ネイティブな [PREDICT](../../t-sql/queries/predict-transact-sql.md) 関数を使うこともできます。通常、これは Python や R のランタイムを呼び出さないので高速です。

## <a name="see-also"></a>関連項目

+ [SQL 機械学習](../../machine-learning/index.yml)
+ [SQL Server 言語拡張機能](../../language-extensions/language-extensions-overview.md)。 
+ [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Transact-sql&#41;&#40;の外部ライブラリの作成 ](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [external scripts enabled サーバー構成オプション](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server のExternal Scripts オブジェクト](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)