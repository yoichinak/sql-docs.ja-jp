---
title: SQL テーブルから Python Pandas データフレームにデータを挿入する
titleSuffix: SQL machine learning
description: Python を使用して SQL テーブルからデータを読み取り、Pandas データフレームに挿入する方法について説明します。
author: dphansen
ms.author: davidph
ms.date: 07/23/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: 041291804f6fbefe4832398b7c56b2ab97940008
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870246"
---
# <a name="insert-data-from-a-sql-table-into-a-python-pandas-dataframe"></a>SQL テーブルから Python Pandas データフレームにデータを挿入する
[!INCLUDE[SQL Server SQL DB SQL MI](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

この記事では、Python で [pyodbc](../../connect/python/pyodbc/python-sql-driver-pyodbc.md) パッケージを使用して、SQL データを [pandas](https://pandas.pydata.org/) データフレームに挿入する方法について説明します。 データフレーム内に含まれるデータの行と列は、さらなるデータの探索に使用できます。

## <a name="prerequisites"></a>前提条件

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

* この記事で使用されているサンプル データを取得するために、[サンプル データベースを復元](../../samples/adventureworks-install-configure.md)します。

## <a name="verify-restored-database"></a>復元されたデータベースの確認

**Person.CountryRegion** テーブルに対してクエリを実行して、復元されたデータベースが存在することを確認できます。

```sql
USE AdventureWorks;
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

## <a name="insert-data"></a>データの挿入

次のスクリプトを使用して、Person.CountryRegion テーブルからデータを選択し、データフレームに挿入します。 接続文字列変数 'server'、'database'、'username'、および 'password' を編集して、SQL に接続します。

新しいノートブックを作成するには:

1. Azure Data Studio で **[ファイル]** を選択し、 **[新しいノートブック]** を選択します。
2. ノートブックで、カーネル **[Python3]** を選択し、 **[+ コード]** を選択します。
3. ノートブックにコードを貼り付け、 **[すべて実行]** を選択します。

```python
import pyodbc
import pandas as pd
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'servername' 
database = 'AdventureWorks' 
username = 'yourusername' 
password = 'databasename'  
cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
# select 26 rows from SQL table to insert in dataframe.
query = "SELECT [CountryRegionCode], [Name] FROM Person.CountryRegion;"
df = pd.read_sql(query, cnxn)
print(df.head(26))
```

**出力**

前のスクリプトの `print` コマンドによって、`pandas` データフレーム `df` のデータ行が表示されます。

```text
CountryRegionCode                 Name
0                 AF          Afghanistan
1                 AL              Albania
2                 DZ              Algeria
3                 AS       American Samoa
4                 AD              Andorra
5                 AO               Angola
6                 AI             Anguilla
7                 AQ           Antarctica
8                 AG  Antigua and Barbuda
9                 AR            Argentina
10                AM              Armenia
11                AW                Aruba
12                AU            Australia
13                AT              Austria
14                AZ           Azerbaijan
15                BS         Bahamas, The
16                BH              Bahrain
17                BD           Bangladesh
18                BB             Barbados
19                BY              Belarus
20                BE              Belgium
21                BZ               Belize
22                BJ                Benin
23                BM              Bermuda
24                BT               Bhutan
25                BO              Bolivia
```

## <a name="next-steps"></a>次のステップ

+ [Python データフレームを SQL に挿入する](../data-exploration/python-dataframe-sql-server.md)