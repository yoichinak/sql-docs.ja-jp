---
title: Python によるデータ探索のためのヒストグラムのプロット
titleSuffix: SQL machine learning
description: Python を使用してデータを視覚化するために、ヒストグラムを作成する方法について説明します。
author: dphansen
ms.author: davidph
ms.date: 07/14/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: ee708d473e29cd36fe02e18e95eb71c0505dfdd7
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870160"
---
# <a name="plot-histograms-in-python"></a>Python でのヒストグラムのプロット 
[!INCLUDE[SQL Server SQL DB SQL MI](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

この記事では、Python パッケージ [pandas'.hist()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.hist.html) を使用してデータをプロットする方法について説明します。 SQL データベースは、連続した重複しない値を持つヒストグラム データ間隔を視覚化するために使用されるソースです。

## <a name="prerequisites"></a>前提条件:

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
* [Windows 用](../../database-engine/install-windows/install-sql-server.md)または [Linux 用の SQL Server](../../linux/sql-server-linux-overview.md)
::: moniker-end

::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"
* [Azure SQL Database](/azure/sql-database/sql-database-get-started-portal)
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
* [Azure SQL Managed Instance](/azure/azure-sql/managed-instance/instance-create-quickstart)

* サンプル データベースを Azure SQL Managed Instance に復元するための [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)。
::: moniker-end

* Azure Data Studio。 インストールするには、[Azure Data Studio](../../azure-data-studio/what-is.md) に関するページを参照してください。

* この記事で使用されているサンプル データを取得するために、[サンプル DW データベースを復元](../../samples/adventureworks-install-configure.md)します。

## <a name="verify-restored-database"></a>復元されたデータベースの確認

**Person.CountryRegion** テーブルに対してクエリを実行して、復元されたデータベースが存在することを確認できます。
```sql
USE AdventureWorksDW;
SELECT * FROM Person.CountryRegion;
```
  
## <a name="install-python-packages"></a>Python パッケージのインストール

[Azure Data Studio をダウンロードしてインストール](../../azure-data-studio/download-azure-data-studio.md)します。

次の Python パッケージをインストールします。
  * pyodbc
  * pandas

  これらのパッケージをインストールするには:

  1. Azure Data Studio ノートブックで、 **[パッケージの管理]** を選択します。
  2. **[パッケージの管理]** ペインで **[新規追加]** タブを選択します。
  3. 次の各パッケージについてパッケージ名を入力し、 **[検索]** をクリックし、 **[インストール]** をクリックします。

## <a name="plot-histogram"></a>ヒストグラムのプロット

ヒストグラムに表示される分散データは、AdventureWorksDW からの SQL クエリに基づいています。 ヒストグラムは、データとデータ値の頻度を視覚化します。 接続文字列変数 'server'、'database'、'username'、および 'password' を編集して、SQL データベースに接続します。

新しいノートブックを作成するには:

1. Azure Data Studio で **[ファイル]** を選択し、 **[新しいノートブック]** を選択します。
2. ノートブックで、カーネル **[Python3]** を選択し、 **[+ コード]** を選択します。
3. ノートブックにコードを貼り付け、 **[すべて実行]** を選択します。

```python
import pyodbc 
import pandas as plt
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'servername' 
database = 'AdventureWorksDW' 
username = 'yourusername' 
password = 'databasename'  
cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
sql = "SELECT DATEDIFF(year, c.BirthDate, GETDATE()) AS Age FROM [dbo].[FactInternetSales] s INNER JOIN dbo.DimCustomer c ON s.CustomerKey = c.CustomerKey"
df = pd.read_sql(sql, cnxn)
df.hist(bins=10)
```

表示には、FactInternetSales テーブル内の顧客の年齢分布が表示されます。

![pandas ヒストグラム](./media/python-histogram.png)