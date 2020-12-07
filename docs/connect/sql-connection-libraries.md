---
title: Microsoft SQL Database の接続ライブラリ | Microsoft Docs
description: 各種のクライアント プログラミング言語から Microsoft SQL Server および Azure SQL Database への接続を可能にするモジュールのダウンロード リンクを示します。
author: David-Engel
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.topic: article
ms.date: 03/06/2020
ms.author: v-daenge
ms.openlocfilehash: 8d5c44c11d9f5158abc52634f648a4159f86c143
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726613"
---
# <a name="connection-modules-for-microsoft-sql-database"></a>Microsoft SQL Database の接続モジュール

この記事では、クライアント プログラムが [Microsoft SQL Server](../relational-databases/databases/databases.md)、およびそれとよく似たクラウド版 [Azure SQL Database](/azure/sql-database/) との対話に使用できる接続モジュール (*ドライバー*) のダウンロード リンクを示します。 次のオペレーティング システムで実行されるさまざまなプログラミング言語用のドライバーが用意されています。

- Linux
- macOS
- Windows

**OOP とリレーショナルの不一致:**

*リレーショナル*:オブジェクト指向プログラミング (OOP) 言語で記述されたクライアント プログラムでは、多くの場合、オブジェクト指向よりもリレーショナルな形式でクエリ データを返す SQL ドライバーを使用します。 ADO.NET を使用する C# がその一例です。 OOP とリレーショナルの形式の不一致により、OOP コードの記述と理解が困難になることがあります。

*ORM*:ほかのドライバーまたはフレームワークは、OOP 形式のクエリ データを返すことで、不一致を回避します。 これらのドライバーは、特定の SQL テーブルのデータ列と一致するようにクラスが定義されていることを前提として機能します。 次に、ドライバーは*オブジェクト リレーショナル マッピング* (ORM) を実行して、クエリ データをクラスのインスタンスとして返します。 Microsoft の Entity Framework (EF) for C#、および Hibernate for Java の 2 つがその例です。

この記事では、この 2 種類の接続ドライバーに個別のセクションを割り当てています。

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>リレーショナル アクセス用のドライバー

| Language | SQL ドライバーのダウンロード |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[.NET Core: Linux-Ubuntu、macOS、Windows](https://dotnet.microsoft.com/download) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js ドライバー、インストール手順](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc、インストール手順](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[ODBC のダウンロード](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby ドライバー、インストール手順](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby のダウンロード ページ](https://rubyinstaller.org/downloads/) |
| &nbsp; | &nbsp; |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM アクセス用のドライバー

次の表は、クライアントアプリケーションが Microsoft SQL Database に接続するために使用するオブジェクト リレーショナル マッピング (ORM) フレームワークの例を示しています。

| Language | ORM ドライバーのダウンロード |
| :------- | :------------------ |
| C# | [Entity Framework Core](/ef/core/)<br />[Entity Framework (6.x 以降)](/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP | [Eloquent ORM (Laravel のインストールに含まれています)](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://sequelize.org/) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |
| &nbsp; | &nbsp; |

<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>Build-an-app の Web ページ

**[https://aka.ms/sqldev](https://aka.ms/sqldev)** により、*Build-an-app* の一連の Web ページが表示されます。 これらの Web ページには、プログラミング言語、オペレーティング システム、および SQL 接続ドライバーのさまざまな組み合わせに関する情報が記載されています。 Build-an-app の Web ページで提供される情報の中には、次の項目があります。

- 言語 + オペレーティングシステム + ドライバーの組み合わせごとに、作業を開始する方法についての詳細。
  - 最新の SQL 接続ドライバーをインストールするための手順。
- 次の各項目のコード例。
  - オブジェクト リレーショナル コードの例。
  - RDS のコード例です。
  - パフォーマンスの大幅な向上のための列ストア インデックスのデモ。

**Build-an-app の Web ページの最初のページ:**  
![Build-an-app の Web ページの最初のページのスクリーンショット](media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png)

**Build-an-app の Web ページの [Java] メニューの [Ubuntu]**  
![Build-an-app の Web ページの [Java] メニューの [Ubuntu]](media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png)

&nbsp;

## <a name="related-links"></a>関連リンク

- [Java およびその他の言語を使用してクラウド内の Azure SQL Database に接続する方法のコード例](/azure/sql-database/sql-database-connect-query-java)

<!--
Image references, **obsolete** markdown syntax alternative:

![Build-an-app webpages, first page screenshot][image-ref-163-buildanapp-webpages-first-page]
![Build-an-app webpages, menu Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
-->