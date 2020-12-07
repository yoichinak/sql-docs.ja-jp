---
title: Java ランタイムを呼び出す
titleSuffix: SQL Server Language Extensions
description: SQL Server 言語拡張を使用し、SQL Server ストアド プロシージャから Java クラスを呼び出す方法について説明します。
author: dphansen
ms.author: davidph
ms.date: 06/25/2020
ms.topic: how-to
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c4d12382cf1e498b33f202bb1b775ba63458a5a5
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870189"
---
# <a name="how-to-call-the-java-runtime-in-sql-server-language-extensions"></a>SQL Server 言語拡張で Java ランタイムを呼び出す方法
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

[SQL Server 言語拡張](../language-extensions-overview.md)には、Java ランタイムを呼び出すインターフェイスとして [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) システム ストアド プロシージャが使用されます。 

このハウツー記事では、SQL Server 上で実行される Java クラスとメソッドの実装について詳しく説明します。

## <a name="where-to-place-java-classes"></a>Java クラスの配置場所

SQL Server で Java クラスを呼び出すには、次の 2 つの方法があります。

1. **.class** または **.jar** ファイルを [Java クラスパス](#classpath)に配置します。 

2. [外部ライブラリ](#external-library) DDL を使用して、 **.jar** ファイルのコンパイル済みクラスおよびその他の依存関係をデータベースにアップロードします。 

> [!NOTE]
> 一般的な推奨事項として、個別の **.class** ファイルではなく、 **.jar** ファイルを使用してください。 これは Java での一般的な方法であり、全体的なエクスペリエンスが簡単になります。 [クラス ファイルから jar ファイルを作成する方法](create-a-java-jar-file-from-class-files.md)に関する記事を参照してください。

<a name="classpath"></a>

## <a name="use-classpath"></a>クラスパスを使用する

### <a name="basic-principles"></a>基本原則

SQL Server で Java を実行する場合の基本的な原則を次に示します。

* コンパイル済みのカスタムの Java クラスは、Java クラスパスの **.class** ファイルまたは **.jar** ファイルに存在する必要があります。 [CLASSPATH パラメーター](#set-classpath)には、コンパイル済みの Java ファイルへのパスを指定します。 

* 呼び出す Java メソッドは、ストアド プロシージャの **script** パラメーターに指定する必要があります。

* クラスがパッケージに属している場合は、**packageName** を指定する必要があります。

* **params** は、Java クラスにパラメーターを渡すために使用されます。 引数を必要とするメソッドの呼び出しはサポートされていません。 そのため、引数の値をメソッドに渡すには、パラメーターが唯一の方法です。 

> [!NOTE]
> この注意では、SQL Server 2019 リリース候補 1 の Java に固有のサポートされている操作とサポートされていない操作について説明します。
> * ストアド プロシージャでは、入力パラメーターがサポートされています。 出力パラメーターはそうではありません。

### <a name="call-java-class"></a>Java クラスを呼び出す

[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) システム ストアド プロシージャは、Java ランタイムの呼び出しに使用されるインターフェイスです。 Java 拡張を使用する `sp_execute_external_script` と、パス、スクリプト、およびカスタム コードを指定するパラメーターの例を次に示します。

> [!NOTE]
> 呼び出すメソッドを定義する必要がないことに注意してください。 既定では、**execute** というメソッドが呼び出されます。 つまり、[SQL Server の拡張機能 SDK for Java](extensibility-sdk-java-sql-server.md) に従い、Java クラスに execute メソッドを実装する必要があります。

```sql
DECLARE @param1 int
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>'
, @input_data_1 = N'<Input Query>'
, @param1 = @param1
```

<a name="set-classpath"></a>

### <a name="set-classpath"></a>CLASSPATH を設定する

1 つまたは複数の Java クラスをコンパイルし、Java クラスパスに jar ファイルを作成した後に、SQL Server Java 拡張機能のクラスパスを指定する方法は 2 つあります。

1. 外部ライブラリを使用する

    最も簡単な方法は、外部ライブラリを作成し、ライブラリを jar にポイントして、SQL Server からクラスを自動的に見つけられるようにすることです。 [Java 用外部ライブラリを使用する](#external-library)

2. システム環境変数を登録する

    システム環境変数を作成し、クラスを含む jar ファイルのパスを指定することができます。 **CLASSPATH** というシステム環境変数を作成します。

<a name="external-library"></a>

## <a name="use-external-library"></a>外部ライブラリを使用する

SQL Server 2019 リリース候補 1 では、Windows および Linux 上で Java 言語用の外部ライブラリを使用できます。 クラスを .jar ファイルにコンパイルし、[CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md) DDL を使用して .jar ファイルとその他の依存関係をデータベースにアップロードできます。

外部ライブラリを使用して .jar ファイルをアップロードする方法の例:

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

外部ライブラリを作成すると、SQL Server から Java クラスに自動的にアクセスできるようになり、クラスパスに特別なアクセス許可を設定する必要がなくなります。

外部ライブラリとしてアップロードされたパッケージからクラスのメソッドを呼び出す例:

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

詳細については、「[CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)」を参照してください。

## <a name="loopback-connection-to-sql-server"></a>SQL Server への Loopback 接続

`sp_execute_external_script` から実行される Java からデータの読み取りまたは書き込みを行うために、Loopback 接続を使用して JDBC 経由で SQL Server に接続します。 この方法は、`sp_execute_external_script` の **InputDataSet** 引数と **OutputDataSet** 引数を使用できない場合に使用できます。
Windows で Loopback 接続するには、次の例を使用します。

```
jdbc:sqlserver://localhost:1433;databaseName=Adventureworks;integratedSecurity=true;
``` 

Linux で Loopback 接続するには、JDBC ドライバーに、次の証明書に定義されている 3 つの接続プロパティが必要になります。

[Client-Certificate-Authentication](https://github.com/microsoft/mssql-jdbc/wiki/Client-Certificate-Authentication-for-Loopback-Scenarios)


## <a name="next-steps"></a>次のステップ

+ [チュートリアル:Java で正規表現を使用して文字列を検索する](../tutorials/search-for-string-using-regular-expressions-in-java.md)