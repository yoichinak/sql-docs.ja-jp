---
title: SQL クライアント プログラミングのホームページ | Microsoft Docs
description: SQL Server または Azure SQL Database に接続するための、さまざまな言語とオペレーティング システムのドキュメントを参照およびダウンロードできるページへの注釈付きリンクが記載されているページ。
author: David-Engel
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: v-daenge
ms.openlocfilehash: 561cb6e02ac26db3c1d5c9a61fcf689bcca5360d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725520"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Microsoft SQL Server に対するクライアント プログラミングのホーム ページ


Microsoft SQL Server を操作するための、およびクラウドで Azure SQL Database を操作するためのクライアント プログラミングに関するホームページへようこそ。 この記事には以下の情報が含まれています。

- 使用できる言語とドライバーの組み合わせについて説明します。
  - Linux (Ubuntu など)、macOS、および Windows のオペレーティング システムに関する情報が提供されています。
- 各組み合わせの詳細なドキュメントへのリンクを提供します。
- 特定の言語の階層型ドキュメントの区分とサブ区分を表示します (該当する場合)。


#### <a name="azure-sql-database"></a>Azure SQL データベース

特定の言語については、SQL Server に接続するコードは、Azure SQL Database に接続するためのコードとほぼ同じです。

Azure SQL Database に接続するための接続文字列の詳細については、以下を参照してください。

- [.NET Core (C#) を使用して Azure SQL データベースに照会する](/azure/sql-database/sql-database-connect-query-dotnet-core)。
- 目次の前の記事の近くにある、他の言語に関するその他の Azure SQL Database の記事。 たとえば、「[PHP を使用して Azure SQL データベースに照会する](/azure/sql-database/sql-database-connect-query-php)」を参照してください。


#### <a name="build-an-app-webpages"></a>Build-an-app の Web ページ

*Build-an-app* の Web ページには、コード例と構成情報を別の形式で示されています。 詳細については、この記事で後述する ["*Build-an-app の Web サイト*" に関するセクション](#an-204-aka-ms-sqldev)をご覧ください。



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>クライアント プログラムの言語とドライバー


次の表の各言語のイメージは、その言語と SQL Server の使用に関する詳細情報にリンクされています。 各リンクをクリックすると、この記事に示されているその言語のセクションに移動します。

:::row:::
    :::column:::
        [![C# のロゴ][image-ref-320-csharp]](#an-110-ado-net-docu)  

        [![Node.js のロゴ][image-ref-340-node]](#an-140-node-js-docu)  

        [![Python のロゴ][image-ref-370-python]](#an-180-python-docu)  
    :::column-end:::
    :::column:::
        [![.NET Framework の ORM Entity Framework][image-ref-333-ef]](#an-116-csharp-ef-orm)  

        [**`ODBC for C++`**](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu)  

        [![Ruby のロゴ][image-ref-380-ruby]](#an-190-ruby-docu)  
    :::column-end:::
    :::column:::
        [![Java のロゴ][image-ref-330-java]](#an-130-jdbc-docu)  

        [![PHP のロゴ][image-ref-360-php]](#an-170-php-docu)  
    :::column-end:::
:::row-end:::

#### <a name="downloads-and-installs"></a>ダウンロードとインストール

次の記事では、プログラミング言語で使用するさまざまな SQL 接続ドライバーのダウンロードとインストールについて説明します。

- [SQL Server ドライバー](./sql-connection-libraries.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C# ロゴ][image-ref-320-csharp] ADO.NET が使用されている C#

ADO.NET を最もよく使用するのが、C#、Visual Basic などの .NET マネージド言語です。 *ADO.NET* は、.NET Framework クラスのサブセットの名前です。

#### <a name="code-examples"></a>コード例

| 例 | 説明 |
| :-- | :-- |
| [ADO.NET を使用した SQL への接続を概念実証する](./ado-net/step-3-connect-sql-ado-net.md) | SQL Server の接続とクエリに重点を置いた小さなコード例。 |
| [ADO.NET で SQL に弾性的に接続する](./ado-net/step-4-connect-resiliently-sql-ado-net.md) | コード例の再試行ロジック (接続が失われる可能性があるため)。<br /><br />再試行ロジックは、インターネットを介して維持される、任意のクラウド データベース (Azure SQL Database など) への接続に適切に適用されます。 |
| [Azure SQL Database: Windows/Linux/macOS で .NET Core を使用して C# プログラムを作成し、接続およびクエリを実行する方法のデモ](/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL Database の例。 |
| [Build-an-app: C#、ADO.NET、Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 構成情報とコード例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>ドキュメント

| 領域 | 説明 |
| :-- | :-- |
| [ADO.NET が使用されている C#](./ado-net/microsoft-ado-net-sql-server.md)| ドキュメントのルート。 |
| [名前空間: System.Data](/dotnet/api/system.data) | ADO.NET に使用されるクラスのセット。 |
| [名前空間: Microsoft.Data.SqlClient](/dotnet/api/microsoft.data.SqlClient) | Microsoft .NET Data Provider for SQL Server に使用されるクラスのセット |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Entity Framework のロゴ][image-ref-333-ef] C# では、Entity Framework(EF)

Entity Framework (EF) は、オブジェクト リレーショナル マッピング (ORM) を提供します。 ORM を使用すると、リレーショナル SQL データベースから取得したデータを、オブジェクト指向プログラミング (OOP) のソース コードで操作しやすくなります。

EF には、次のテクノロジと直接的または間接的なリレーションシップがあります。

- .NET Framework
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/) または [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- 言語構文の拡張機能。C# の **=>** 演算子など。
- SQL データベースのテーブルにマップされるクラスのソース コードを生成する便利なプログラム。 [EdmGen.exe](/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe) など。


#### <a name="original-ef-and-new-ef"></a>元の EF と新しい EF

[Entity Framework の開始ページ](/ef/)では、EF が次のように説明されています。

- Entity Framework は、.NET 開発者が .NET オブジェクトを使用してデータベースを操作できるようにする、オブジェクト リレーショナル マッパー (O/RM) です。 これにより、開発者が通常は記述する必要のあるデータアクセス ソース コードの大部分が不要になります。

*Entity Framework* は、2 つの異なるソース コード分岐によって共有される名前です。 一方の EF 分岐は古く、そのソース コードはパブリックで管理できるようになりました。 もう一方は新しい EF です。 この 2 つの EF について次に説明します。

| Version | Description |
| :-- | :-- |
| [EF 6.x](/ef/ef6/) | Microsoft が最初に EF をリリースしたのは 2008 年 8 月です。 そして 2015 年 3 月、Microsoft は、最後の Microsoft 開発バージョンとして EF 6.x を発表し、 ソース コードをパブリック ドメインに公開しました。<br /><br />当初、EF は .NET Framework に含まれていましたが、 EF 6 は .NET Framework から削除されました。<br /><br />[GitHub の *aspnet/EntityFramework6* リポジトリの EF 6.x ソース コード](https://github.com/aspnet/EntityFramework6) |
| [EF Core](/ef/core/) | 2016 年 6 月、Microsoft は新しく開発された EF Core をリリースしました。 EF Core は、柔軟性と移植性の向上を目指して設計されたもので、 Microsoft Windows 以外のオペレーティング システムで実行できます。 また、EF Core では、Microsoft SQL Server やその他のリレーショナル データベース以外のデータベースを操作することもできます。<br /><br />**C&#x23; のコード例:**<br />[Entity Framework Core の概要](/ef/core/get-started/index)<br />[既存のデータベースを使用した .NET Framework 上の EF Core の概要](/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF とその関連テクノロジは強力で、すべての区分を習得したいと考えている開発者にとっては学習するべきものが多くあります。

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java のロゴ][image-ref-330-java] Java と JDBC

Microsoft からは、SQL Server (または Azure SQL Database) で使用するための Java Database Connectivity (JDBC) ドライバーが提供されています。 これは Type 4 JDBC ドライバーであり、標準の JDBC アプリケーション プログラム インターフェイス (API) によってデータベース接続を提供します。

#### <a name="code-examples"></a>コード例

| 例 | 説明 |
| :-- | :-- |
| [コード例](./jdbc/sample-jdbc-driver-applications.md) | データ型、結果セット、および大きなデータについて学習するためのコード例。 |
| [接続 URL のサンプル](./jdbc/connection-url-sample.md) | 接続 URL を使用して SQL Server に接続する方法について説明します。 その後、これを使って SQL ステートメントを使用し、データを取得します。 |
| [データ ソースのサンプル](./jdbc/data-source-sample.md) | データ ソースを使用して SQL Server に接続する方法について説明します。 その後、ストアド プロシージャを使用してデータを取得します。 |
| [Java を使用して Azure SQL データベースに照会する](/azure/sql-database/sql-database-connect-query-java) | Azure SQL Database の例。 |
| [Ubuntu で SQL Server を使用して Java アプリを作成する](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 構成情報とコード例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>ドキュメント

JDBC ドキュメントに含まれる主な区分を次に示します。

| 領域 | 説明 |
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/microsoft-jdbc-driver-for-sql-server.md) | JDBC ドキュメントのルート。 |
| [リファレンス](./jdbc/reference/jdbc-driver-api-reference.md) | インターフェイス、クラス、およびメンバー。 |
| [JDBC SQL ドライバーのプログラミング ガイド](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 構成情報とコード例。 |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js のロゴ][image-ref-340-node] Node.js

Node.js を使用すると、Windows、Linux、または macOS から SQL Server に接続できます。 Node.js ドキュメントのルートについては、[こちら](./node-js/node-js-driver-for-sql-server.md)をご覧ください。

SQL Server 用の Node.js 接続ドライバーは JavaScript で実装されます。 このドライバーで使用される TDS プロトコルは、最新バージョンのすべての SQL Server でサポートされています。 このドライバーはオープンソース プロジェクトであり、[GitHub で入手できます](https://tediousjs.github.io/tedious/)。

#### <a name="code-examples"></a>コード例

| 例 | 説明 |
| :-- | :-- |
| [Node.js を使用した SQL への接続を概念実証する](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | SQL Server に接続してクエリを実行するための最小限のソース コード。 |
| [Azure SQL データベース: Node.js を使用してクエリを実行する](/azure/sql-database/sql-database-connect-query-nodejs) | クラウドの Azure SQL Database の例。 |
| [Node.js アプリを作成して macOS で SQL Server を使用する](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 構成情報とコード例。 |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>C++ 用の ODBC

![ODBC のロゴ][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

1990 年代に開発された Open Database Connectivity (ODBC) は、.NET Framework より前に登場しました。 ODBC は、特定のデータベース システムにもオペレーティング システムにも依存しないように設計されています。

長年にわたって、多数の ODBC ドライバーが Microsoft 内外のグループによって作成およびリリースされ、 そのドライバー範囲には、クライアント プログラミング言語が複数含まれます。 データ ターゲットのリストは、SQL Server をはるかに超えています。

他の接続ドライバーの中には、ODBC が内部的に使用されるものもあります。

#### <a name="code-example"></a>コードの例

- [ODBC を使用する C++ コードの例](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>ドキュメントの概要

このセクションの ODBC コンテンツは、C++ から SQL Server または Azure SQL Database にアクセスすることに重点を置いています。 次の表は、ODBC の主要ドキュメントの概要を示しています。


| 領域 | サブ区分 | 説明 |
| :--- | :------ | :---------- |
| [C++ 用の ODBC](./odbc/microsoft-odbc-driver-for-sql-server.md) | ドキュメントのルート。 |
| [Linux-macOS](./odbc/linux-mac/system-requirements.md) | &nbsp; | Linux または macOS オペレーティング システムでの ODBC の使用に関する情報。 |
| [Windows](./odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)     | &nbsp; | Windows オペレーティング システムでの ODBC の使用に関する情報。 |
| [管理](../odbc/admin/odbc-data-source-administrator.md) | &nbsp; | ODBC データ ソースを管理するための管理ツール。 |
| [Microsoft](../odbc/microsoft/microsoft-supplied-odbc-drivers.md)  | &nbsp; | Microsoft によって作成および提供される各種 ODBC ドライバー。 |
| [概念とリファレンス](../odbc/reference/introduction-to-odbc.md) | &nbsp; | 従来のリファレンスのほか、ODBC インターフェイスに関する概念情報。 |
| &nbsp; " | [付録](../odbc/reference/appendixes/odbc-appendixes.md)    | 状態遷移テーブル、ODBC カーソル ライブラリなど。 |
| &nbsp; " | [アプリの開発](../odbc/reference/develop-app/checking-feature-support-and-variability.md)  | 関数、ハンドルなど。 |
| &nbsp; " | [ドライバーの開発](../odbc/reference/develop-driver/developing-an-odbc-driver.md) | 独自の ODBC ドライバーを開発する方法 (特別なデータ ソースがある場合)。 |
| &nbsp; " | [インストール](../odbc/reference/install/odbc-subkey.md) | ODBC のインストール、サブキーなど。 |
| &nbsp; " | [構文](../odbc/reference/syntax/odbc-reference.md)   | セットアップ、インストーラー、翻訳、およびデータ アクセスのための API。 |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP のロゴ][image-ref-360-php] PHP

PHP を使用して SQL Server と対話できます。 PHP ドキュメントのルートについては、[こちら](./php/microsoft-php-driver-for-sql-server.md)をご覧ください。

#### <a name="code-examples"></a>コード例

| 例 | 説明 |
| :-- | :-- |
| [PHP を使用した SQL への接続を概念実証する](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | SQL Server の接続とクエリに重点を置いた小さなコード例。 |
| [PHP で SQL に弾性的に接続する](./php/step-4-connect-resiliently-to-sql-with-php.md) | コード例の再試行ロジック (インターネットおよびクラウドを介した接続が失われる可能性があるため)。 |
| [Azure SQL データベース: PHP を使用してクエリを実行する](/azure/sql-database/sql-database-connect-query-php) | Azure SQL Database の例。 |
| [PHP アプリを作成して RHEL で SQL Server を使用する](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 構成情報とコード例。 |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python ロゴ][image-ref-370-python] Python


Python を使用して SQL Server と対話できます。

#### <a name="code-examples"></a>コード例

| 例 | 説明 |
| :-- | :-- |
| [pyodbc と Python を使用した SQL への接続の概念実証](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | SQL Server の接続とクエリに重点を置いた小さなコード例。 |
| [Azure SQL データベース: Python を使用してクエリを実行する](/azure/sql-database/sql-database-connect-query-python) | Azure SQL Database の例。 |
| [PHP アプリを作成して SLES で SQL Server を使用する](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 構成情報とコード例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>ドキュメント

| 領域 | 説明 |
| :--- | :---------- |
| [Python から SQL Server](./python/python-driver-for-sql-server.md) | ドキュメントのルート。 |
| [pymssql ドライバー](./python/pymssql/python-sql-driver-pymssql.md) | Microsoft では、pymssql ドライバーを保守またはテストしません。<br /><br />pymssql 接続ドライバーは、Python プログラムで使用するための、SQL データベースに対するシンプルなインターフェイスです。 pymssql は FreeTDS を基盤として構築され、Python DB-API (PEP-249) インターフェイスを Microsoft SQL Server に提供します。 |
| [pyodbc ドライバー](./python/pyodbc/python-sql-driver-pyodbc.md)   | pyodbc 接続ドライバーは、ODBC データベースに容易にアクセスできるようにするオープンソースの Python モジュールです。 DB API 2.0 仕様を実装していますが、より Python らしい利便性を備えています。 |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby のロゴ][image-ref-380-ruby] Ruby

Ruby を使用して SQL Server と対話できます。 Ruby ドキュメントのルートについては、[こちら](./ruby/ruby-driver-for-sql-server.md)をご覧ください。

#### <a name="code-examples"></a>コード例

| 例 | 説明 |
| :-- | :-- |
| [Ruby を使用した SQL への接続を概念実証する](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | SQL Server の接続とクエリに重点を置いた小さなコード例。 |
| [Azure SQL データベース: Ruby を使用してクエリを実行する](/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL Database の例。 |
| [Ruby アプリを作成して macOS で SQL Server を使用する](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 構成情報とコード例。 |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-development"></a>[Build-an-app の Web サイト (SQL クライアント開発用)](https://www.microsoft.com/sql-server/developer-get-started/)


[*Build-an-app*](https://www.microsoft.com/sql-server/developer-get-started/) の Web ページには、SQL Server に接続するためのプログラミング言語が多数用意されており、ユーザーは必要な言語をこの一覧から選択できます。 また、お使いのクライアント プログラムでは、さまざまなオペレーティング システムを実行できます。

*Build-an-app* が重視しているのは、作業を開始したばかりの開発者にとってのわかりやすさと完全性です。 この手順では次のタスクについて説明します。

1. Microsoft SQL Server のインストール方法
2. ツールとドライバーのダウンロードおよびインストール方法。
3. 選択したオペレーティング システムに応じて、必要な構成を行う方法。
4. 提供されたソース コードをコンパイルする方法。
5. プログラムの実行方法。

次に Web サイトで提供されている詳細情報の概略をいくつか示します。

#### <a name="java-on-ubuntu"></a>Ubuntu 上の Java

1. 環境の設定方法
    - 手順 1.1 SQL Server をインストールする
    - 手順 1.2 Java をインストールする
    - 手順 1.3 Java Development Kit (JDK) をインストールする
    - 手順 1.4 Maven をインストールする
2. SQL Server を使用して Java アプリケーションを作成します
    - 手順 2.1 SQL Server に接続してクエリを実行する Java アプリを作成する
    - 手順 2.2 一般的なフレームワーク Hibernate を使用して SQL Server に接続する Java アプリを作成する
3. Java アプリを最大 100 倍高速化する
    - 手順3.1 Java アプリを作成して列ストア インデックスを示す

#### <a name="python-on-windows"></a>Windows 上の Python

1. 環境の設定方法
    - 手順 1.1 SQL Server をインストールする
    - 手順 1.2 Python をインストールする
    - 手順 1.3 SQL Server 用の ODBC ドライバーと SQL コマンド ライン ユーティリティをインストールする
2. SQL Server を使用して Python アプリケーションを作成します
    - 手順 2.1 Python Driver for SQL Server をインストールする
    - 手順 2.2 お使いのアプリケーション用のデータベースを作成する
    - 手順 2.3 SQL Server に接続してクエリを実行する Python アプリを作成する
3. Python アプリを最大 100 倍高速化する
    - 手順 3.1 sqlcmd を使用して 500 万を含む新しいテーブルを作成する
    - 手順 3.2 このテーブルに対してクエリを実行し、所要時間を測定する Python アプリを作成する
    - 手順 3.3 クエリの実行にかかる時間を測定する
    - 手順 3.4 列ストア インデックスをお使いのテーブルに追加する
    - 手順 3.5 列ストアでのクエリの実行にかかる時間を測定する

次のスクリーンショットは、SQL 開発ドキュメントの Web サイトがどのように表示されるかを示しています。

#### <a name="choose-a-language"></a>言語の選択

![SQL Dev Web サイト、概要][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>オペレーティング システムの選択

![SQL Dev Web サイト、Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>他の開発


このセクションでは、その他の開発オプションに関するリンクを示します。 これには Azure 開発全般に同じ言語を使用することが含まれます。 この情報は、Azure SQL Database と Microsoft SQL Server のみを対象とするものではありません。

#### <a name="developer-hub-for-azure"></a>Azure 用の開発者ハブ

- [Azure 用の開発者ハブ](/azure/)
- [Azure for .NET 開発者](/dotnet/azure/)
- [Java 開発者向けの Azure](/java/azure/)
- [Node.js 開発者向けの Azure](/nodejs/azure/)
- [Python 開発者向けの Azure](/python/azure/)
- [Azure に PHP Web アプリを作成する](/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>その他の言語

- [Windows で SQL Server を使用して Go アプリを作成する](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-322-cpp]: ./media/homepage-sql-connection-drivers/gm-cpp-4point-p61f.png
[image-ref-320-csharp]: ./media/homepage-sql-connection-drivers/gm-csharp-c10c.png
[image-ref-333-ef]: ./media/homepage-sql-connection-drivers/gm-entity-framework-ef20d.png
[image-ref-330-java]: ./media/homepage-sql-connection-drivers/gm-java-j18c.png
[image-ref-340-node]: ./media/homepage-sql-connection-drivers/gm-node-n30.png
[image-ref-350-odbc]: ./media/homepage-sql-connection-drivers/gm-odbc-ic55826-o35.png
[image-ref-360-php]: ./media/homepage-sql-connection-drivers/gm-php-php60.png
[image-ref-370-python]: ./media/homepage-sql-connection-drivers/gm-python-py72.png
[image-ref-380-ruby]: ./media/homepage-sql-connection-drivers/gm-ruby-un-r82.png
[image-ref-390-aka-ms-sqldev-choose-language]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-400-aka-ms-sqldev-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png