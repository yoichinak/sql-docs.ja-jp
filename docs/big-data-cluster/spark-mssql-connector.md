---
title: SQL Server と Azure SQL 用の Apache Spark コネクタの使用
titleSuffix: SQL Server big data clusters
description: SQL Server と Azure SQL の Apache Spark コネクタを使用して SQL Server に読み取りと書き込みを行う方法について学習します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: 454d5fadaa88d645e9d1c2feec2c9d87c2af29c9
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645503"
---
# <a name="use-the-apache-spark-connector-for-sql-server-and-azure-sql"></a>SQL Server と Azure SQL 用の Apache Spark コネクタを使用する

[SQL Server と Azure SQL 用の Apache Spark コネクタ](https://github.com/microsoft/sql-spark-connector)は、パフォーマンスの高いコネクタです。これを使用すると、ビッグ データ分析でトランザクション データを使用し、アドホック クエリやレポートの結果を保持できます。 コネクタを使用すると、オンプレミスまたはクラウド内のあらゆる SQL データベースを、Spark ジョブの入力データ ソースまたは出力データ シンクとして使用できます。 このコネクタでは、SQL Server 一括書き込み API が使用されます。 任意の一括書き込みパラメーターは、任意のパラメーターとして渡される場合があり、コネクタによって基になる API にそのまま渡されます。 一括書き込み操作の詳細については、「[JDBC ドライバーでの一括コピーの使用]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)」を参照してください。

コネクタは SQL Server ビッグ データ クラスターに既定で含まれています。

コネクタの詳細については、[オープン ソース リポジトリ](https://github.com/microsoft/sql-spark-connector)で確認してください。 例については、[サンプル](https://github.com/microsoft/sql-spark-connector/tree/master/samples)を参照してください。

## <a name="write-to-a-new-sql-table"></a>新しい SQL テーブルに書き込む

>[!CAUTION]
> `overwrite` モードでは、テーブルが既定でデータベースに既に存在する場合は、コネクタによって最初に削除されます。 予期しないデータ損失を避けるため、このオプションは十分な注意を払って使用してください。
> 
> モード `overwrite` を使用している場合、テーブルの再作成時にオプション `truncate` を使用しないと、インデックスは失われます。 たとえば、列ストア テーブルがヒープになります。 既存のインデックス作成を維持したい場合は、オプション `truncate` も値 `true` で指定してください。 例: `.option("truncate",true)`。

```python
server_name = "jdbc:sqlserver://{SERVER_ADDR}"
database_name = "database_name"
url = server_name + ";" + "databaseName=" + database_name + ";"

table_name = "table_name"
username = "username"
password = "password123!#" # Please specify password here

try:
  df.write \
    .format("com.microsoft.sqlserver.jdbc.spark") \
    .mode("overwrite") \
    .option("url", url) \
    .option("dbtable", table_name) \
    .option("user", username) \
    .option("password", password) \
    .save()
except ValueError as error :
    print("Connector write failed", error)
```

## <a name="append-to-sql-table"></a>SQL テーブルに追加する
```python
try:
  df.write \
    .format("com.microsoft.sqlserver.jdbc.spark") \
    .mode("append") \
    .option("url", url) \
    .option("dbtable", table_name) \
    .option("user", username) \
    .option("password", password) \
    .save()
except ValueError as error :
    print("Connector write failed", error)
```

## <a name="specify-the-isolation-level"></a>分離レベルを指定する

このコネクタでは、データベースへの一括挿入を実行するときに、既定で READ_COMMITTED 分離レベルが使用されます。 これを別の分離レベルでオーバーライドしたい場合は、次に示すように `mssqlIsolationLevel` オプションを使用します。
```python
    .option("mssqlIsolationLevel", "READ_UNCOMMITTED") \
```

## <a name="read-from-sql-table"></a>SQL テーブルから読み取る

```python
jdbcDF = spark.read \
        .format("com.microsoft.sqlserver.jdbc.spark") \
        .option("url", url) \
        .option("dbtable", table_name) \
        .option("user", username) \
        .option("password", password).load()
```

## <a name="non-active-directory-mode"></a>非 Active Directory モード

非 Active Directory モードのセキュリティでは、各ユーザーがユーザー名とパスワードを持っています。これは、読み取りと書き込みを実行するためのコネクタのインスタンス化時にパラメーターとして指定する必要があります。

非 Active Directory モードでのコネクタのインスタンス化の例を次に示します。 スクリプトを実行する前に、`?` をご自分のアカウントの値に置き換えます。

```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark" 

url = "jdbc:sqlserver://master-p-svc;databaseName=?;"
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("user", ?) \ 
   .option("password",?) 
writer.save() 
```

## <a name="active-directory-mode"></a>Active Directory モード

Active Directory モードのセキュリティでは、ユーザーがキー タブ ファイルを生成した後、コネクタのインスタンス化時に、ユーザーが `principal` と `keytab` をパラメーターとして指定する必要があります。

このモードでは、ドライバーがそれぞれの実行プログラム コンテナーに、keytab ファイルを読み込みます。 次に、この実行プログラムが、プリンシパル名と keytab を使用して、読み取り/書き込み用の JDBC コネクタの作成に使用されるトークンを生成します。

Active Directory モードでのコネクタのインスタンス化の例を次に示します。 スクリプトを実行する前に、`?` をご自分のアカウントの値に置き換えます。

```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark"

url = "jdbc:sqlserver://master-p-svc;databaseName=?;integratedSecurity=true;authenticationScheme=JavaKerberos;" 
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("principal", ?) \ 
   .option("keytab", ?)   

writer.save() 
```

## <a name="next-steps"></a>次のステップ

ビッグ データ クラスターの詳細については、[Kubernetes に [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] を展開する方法](deployment-guidance.md)に関するページを参照してください

SQL Server ビッグ データ クラスターのフィードバックまたは機能に関する推奨事項がありますか? [SQL Server ビッグ データ クラスターのフィードバックにメモを残してください。](https://aka.ms/sql-server-bdc-feedback)
