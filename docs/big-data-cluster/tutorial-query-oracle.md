---
title: Oracle の外部データにクエリを実行する
titleSuffix: SQL Server big data clusters
description: このチュートリアルでは、SQL Server 2019 ビッグ データ クラスターから Oracle データにクエリを実行する方法について説明します。 Oracle のデータに対する外部テーブルを作成し、クエリを実行します。
author: MikeRayMSFT
ms.author: dacoelho
ms.reviewer: mikeray
ms.date: 10/01/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 48d7fb0f41446fa54f1376a9a84f7dbff7017960
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196086"
---
# <a name="tutorial-query-oracle-from-sql-server-big-data-cluster"></a>チュートリアル:SQL Server ビッグ データ クラスターから Oracle にクエリを実行する

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

このチュートリアルでは、SQL Server 2019 ビッグ データ クラスターから Oracle データにクエリを実行する方法について説明します。 このチュートリアルを実行するには、Oracle サーバーにアクセスできる必要があります。 外部オブジェクトに対して読み取り特権を持つ Oracle ユーザー アカウントが必要です。 Oracle プロキシ ユーザー認証がサポートされています。 アクセスできない場合は、このチュートリアルで、SQL Server ビッグ データ クラスター内の外部データ ソースに対してデータ仮想化がどのように機能するかを理解できます。

このチュートリアルでは、以下の内容を学習します。

> [!div class="checklist"]
> * 外部 Oracle データベースのデータ用の外部テーブルを作成する。
> * このデータを、マスター インスタンスの価値の高いデータと結合する。

> [!TIP]
> 必要に応じて、このチュートリアルのコマンド用のスクリプトをダウンロードして実行できます。 手順については、GitHub の[データ仮想化のサンプル](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization)を参照してください。

## <a name="prerequisites"></a><a id="prereqs"></a> 前提条件

- [ビッグ データ ツール](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 の拡張機能**
- [ビッグ データ クラスターにサンプル データを読み込む](tutorial-load-sample-data.md)

## <a name="create-an-oracle-table"></a>Oracle テーブルを作成する

次の手順では、Oracle で `INVENTORY` という名前のサンプル テーブルを作成します。

1. このチュートリアルで使用する Oracle インスタンスとデータベースに接続します。

1. `INVENTORY` テーブルを作成するには、次のステートメントを実行します。

   ```sql
    CREATE TABLE "INVENTORY"
    (
        "INV_DATE" NUMBER(10,0) NOT NULL,
        "INV_ITEM" NUMBER(10,0) NOT NULL,
        "INV_WAREHOUSE" NUMBER(10,0) NOT NULL,
        "INV_QUANTITY_ON_HAND" NUMBER(10,0)
    );

    CREATE INDEX INV_ITEM ON HR.INVENTORY(INV_ITEM);
    ```

1. このテーブルに、 **inventory.csv** ファイルの内容をインポートします。 このファイルは、「[前提条件](#prereqs) 」セクションのサンプル作成スクリプトによって作成されたものです。

## <a name="create-an-external-data-source"></a>外部データ ソースを作成する

最初の手順では、Oracle サーバーにアクセスできる外部データ ソースを作成します。

1. Azure Data Studio で、ビッグ データ クラスターの SQL Server マスター インスタンスに接続します。 詳細については、「[SQL Server マスター インスタンスに接続する](connect-to-big-data-cluster.md#master)」を参照してください。

1. **[サーバー]** ウィンドウで接続をダブルクリックして、SQL Server マスター インスタンスのサーバー ダッシュボードを表示します。 **[新しいクエリ]** を選択します。

   ![SQL Server マスター インスタンス クエリ](./media/tutorial-query-oracle/sql-server-master-instance-query.png)

1. 次の Transact-SQL コマンドを実行し、マスター インスタンスの **Sales** データベースにコンテキストを変更します。

   ```sql
   USE Sales
   GO
   ```

1. Oracle サーバーに接続するためのデータベース スコープ資格情報を作成します。 次のステートメントで、Oracle サーバーに適切な資格情報を指定します。

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleCredential]
   WITH IDENTITY = '<oracle_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_user_password,nvarchar(100),manager>';
   ```

1. Oracle サーバーを指す外部データ ソースを作成します。

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',CREDENTIAL = [OracleCredential]);
   ```

### <a name="optional-oracle-proxy-authentication"></a>省略可能:Oracle プロキシ認証

Oracle は、きめ細かいアクセス制御を備えるプロキシ認証をサポートしています。 プロキシ ユーザーは、その資格情報を使用して Oracle データベースに接続し、データベース内の別のユーザーの権限を借用します。 

プロキシ ユーザーは、権限が借用されているユーザーと比較してアクセスが制限されるように構成することができます。 たとえば、プロキシ ユーザーは、権限が借用されているユーザーの特定のデータベース ロールを使用して接続することができます。 複数のユーザーがプロキシ認証を使用して接続している場合でも、プロキシ ユーザーを介して Oracle データベースに接続しているユーザーの ID は接続に保持されます。 Oracle では、これを利用してアクセス制御を実施し、実際のユーザーに代わって実行されたアクションを監査することができます。

oracle プロキシ ユーザーの使用が必要なシナリオの場合は、 __前の手順の 4 と 5 を次のものに置き換えてください__ 。

4. Oracle サーバーに接続するためのデータベース スコープ資格情報を作成します。 次のステートメントで、Oracle サーバーに適切な oracle プロキシ ユーザーの資格情報を指定します。

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleProxyCredential]
   WITH IDENTITY = '<oracle_proxy_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_proxy_user_password,nvarchar(100),manager>';
   ```

5. Oracle サーバーを指す外部データ ソースを作成します。

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',
   CONNECTION_OPTIONS = 'ImpersonateUser=% CURRENT_USER',
   CREDENTIAL = [OracleProxyCredential]);
   ```

## <a name="create-an-external-table"></a>外部テーブルを作成する

次に、Oracle サーバー上の `INVENTORY` テーブルに対して **iventory_ora** という名前の外部テーブルを作成します。

```sql
CREATE EXTERNAL TABLE [inventory_ora]
    ([inv_date] DECIMAL(10,0) NOT NULL, [inv_item] DECIMAL(10,0) NOT NULL,
    [inv_warehouse] DECIMAL(10,0) NOT NULL, [inv_quantity_on_hand] DECIMAL(10,0))
WITH (DATA_SOURCE=[OracleSalesSrvr],
        LOCATION='<oracle_service_name,nvarchar(30),xe>.<oracle_schema,nvarchar(128),HR>.<oracle_table,nvarchar(128),INVENTORY>');
```

> [!NOTE]
> Oracle に対するクエリの実行中に、テーブル名と列名では ANSI SQL 引用符で囲まれた識別子が使用されます。 その結果、名前では大文字と小文字が区別されます。 Oracle メタデータ内のテーブル名と列名の大文字と小文字が正確に一致する、外部テーブル定義で名前を指定することが重要です。

## <a name="query-the-data"></a>データにクエリを実行する

次のクエリを実行し、`iventory_ora` 外部テーブルのデータを、ローカルの `Sales` データベース内のテーブルと結合します。

```sql
SELECT TOP(100) w.w_warehouse_name, i.inv_item, SUM(i.inv_quantity_on_hand) as total_quantity
  FROM [inventory_ora] as i
  JOIN item as it
    ON it.i_item_sk = i.inv_item
  JOIN warehouse as w
    ON w.w_warehouse_sk = i.inv_warehouse
 WHERE it.i_category = 'Books' and i.inv_item BETWEEN 1 and 18000 --> get items within specific range
 GROUP BY w.w_warehouse_name, i.inv_item;
```

## <a name="clean-up"></a>クリーンアップ

このチュートリアルで作成されたデータベース オブジェクトを削除するには、次のコマンドを使用します。

```sql
DROP EXTERNAL TABLE [inventory_ora];
DROP EXTERNAL DATA SOURCE [OracleSalesSrvr] ;
DROP DATABASE SCOPED CREDENTIAL [OracleCredential];
```

## <a name="next-steps"></a>次のステップ

データ プールにデータを取り込む方法を学習します:
> [!div class="nextstepaction"]
> [データをデータ プールに読み込む](tutorial-data-pool-ingest-sql.md)
