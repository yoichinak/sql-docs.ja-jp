---
title: Python データフレームを SQL テーブルに挿入する
titleSuffix: SQL machine learning
description: データフレームから SQL テーブルにデータを挿入する方法。
author: dphansen
ms.author: davidph
ms.date: 07/23/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=azuresqldb-current||=sqlallproducts-allversions'
ms.openlocfilehash: 85980bf7bc69190a0e7ae75ee74336a62afd12c6
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870247"
---
# <a name="insert-python-dataframe-into-sql-table"></a>Python データフレームを SQL テーブルに挿入する
[!INCLUDE[SQL Server SQL DB SQL MI](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

この記事では、Python で [pyodbc](../../connect/python/pyodbc/python-sql-driver-pyodbc.md) パッケージを使用して、SQL データベースに [pandas](https://pandas.pydata.org/) データフレームを挿入する方法について説明します。

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

**HumanResources.Department** テーブルに対してクエリを実行して、復元されたデータベースが存在することを確認できます。

```sql
USE AdventureWorks;
SELECT * FROM HumanResources.Department;
```

## <a name="install-python-packages"></a>Python パッケージのインストール

* [Azure Data Studio のダウンロードとインストール](../../azure-data-studio/download-azure-data-studio.md)

次の Python パッケージをインストールします。
  * pyodbc
  * pandas

  これらのパッケージをインストールするには:

  1. Azure Data Studio ノートブックで、 **[パッケージの管理]** を選択します。
  2. **[パッケージの管理]** ペインで **[新規追加]** タブを選択します。
  3. 次の各パッケージについてパッケージ名を入力し、 **[検索]** をクリックし、 **[インストール]** をクリックします。

## <a name="connect-to-sql-server-using-azure-data-studio"></a>Azure Data Studio を使用して SQL Server に接続する

[Azure Data Studio を使用して接続します](../../azure-data-studio/quickstart-sql-server.md)。

1. Adventureworks データベースに接続して、新しいテーブル HumanResources.DepartmentTest を作成します。 SQL テーブルは、データフレームの挿入に使用されます。

```sql
CREATE TABLE [HumanResources].[DepartmentTest](
[DepartmentID] [smallint] NOT NULL,
[Name] [dbo].[Name] NOT NULL,
[GroupName] [dbo].[Name] NOT NULL
)
GO
```

## <a name="create-csv-file"></a>CSV ファイルの作成

データフレームのテキストをコピーし、ファイルを department .csv として保存します。

```text
DepartmentID,Name,GroupName,
1,Engineering,Research and Development,
2,Tool Design,Research and Development,
3,Sales,Sales and Marketing,
4,Marketing,Sales and Marketing,
5,Purchasing,Inventory Management,
6,Research and Development,Research and Development,
7,Production,Manufacturing,
8,Production Control,Manufacturing,
9,Human Resources,Executive General and Administration,
10,Finance,Executive General and Administration,
11,Information Services,Executive General and Administration,
12,Document Control,Quality Assurance,
13,Quality Assurance,Quality Assurance,
14,Facilities and Maintenance,Executive General and Administration,
15,Shipping and Receiving,Inventory Management,
16,Executive,Executive General and Administration
```

## <a name="connect-to-sql-using-python"></a>Python を使用した SQL への接続

1. 接続文字列変数 'server'、'database'、'username'、および 'password' を編集して、SQL データベースに接続します。

2. CSV ファイルのパスを編集します。

## <a name="load-dataframe-from-csv-file"></a>CSV ファイルからデータフレームを読み込む

Python `pandas` パッケージを使用してデータフレームを作成し、CSV ファイルを読み込みます。 SQL に接続して、新しい SQL テーブル HumanResources.DepartmentTest にデータフレームを読み込みます。

新しいノートブックを作成するには:

1. Azure Data Studio で **[ファイル]** を選択し、 **[新しいノートブック]** を選択します。
2. ノートブックで、カーネル **[Python3]** を選択し、 **[+ コード]** を選択します。
3. ノートブックにコードを貼り付け、 **[すべて実行]** を選択します。

 ```Python
import pyodbc
import pandas as pd
# insert data from csv file into dataframe.
# working directory for csv file: type "pwd" in Azure Data Studio or Linux
# working directory in Windows c:\users\username
df = pd.read_csv("c:\\user\\username\department.csv")
# Some other example server values are
# server = 'localhost\sqlexpress' # for a named instance
# server = 'myserver,port' # to specify an alternate port
server = 'yourservername' 
database = 'AdventureWorks' 
username = 'username' 
password = 'yourpassword' 
cnxn = pyodbc.connect('DRIVER={SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
# Insert Dataframe into SQL Server:
for index, row in df.iterrows():
     cursor.execute("INSERT INTO HumanResources.DepartmentTest (DepartmentID,Name,GroupName) values(?,?,?)", row.DepartmentID, row.Name, row.GroupName)
cnxn.commit()
cursor.close()
```

## <a name="confirm-row-count-in-sql"></a>SQL での行数の確認

SQL ステートメントを実行して、テーブルにデータフレームからのデータが正常に読み込まれたことを確認します。

```sql
SELECT count(*) from HumanResources.DepartmentTest;
```

結果

```bash
(No column name)
16
```

## <a name="next-steps"></a>次のステップ

+ [Python によるデータ探索のためのヒストグラムのプロット](../data-exploration/python-plot-histogram.md)