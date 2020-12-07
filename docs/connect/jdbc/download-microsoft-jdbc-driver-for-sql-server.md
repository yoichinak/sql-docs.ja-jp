---
title: Microsoft SQL Server 用 JDBC Driver のダウンロード
description: SQL Server や Azure SQL Database に接続する Java アプリケーションを開発するには、Microsoft JDBC Driver for SQL Server をダウンロードします。
ms.date: 08/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 451181b8-11e6-4d01-b547-9ac5aada8238
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c7d16eeaf72d5faa2c5bad47b8b8331dfdb6b54
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725483"
---
# <a name="download-microsoft-jdbc-driver-for-sql-server"></a>Microsoft SQL Server 用 JDBC Driver のダウンロード

Microsoft JDBC Driver for SQL Server は Type 4 JDBC Driver であり、Java Platform で利用できる標準の JDBC アプリケーション プログラム インターフェイス (API) によって、データベース接続が提供されます。 ドライバーのダウンロードは、すべてのユーザーが追加料金なしで利用できます。 任意の Java アプリケーション、アプリケーション サーバー、Java 対応アプレットから、SQL Server にアクセスできます。

## <a name="download"></a>ダウンロード

最新の一般提供 (GA) バージョンはバージョン 8.4 です。 Java 8、11、14 がサポートされています。 それ以前の Java ランタイムを実行する必要がある場合、[Java と JDBC の仕様のサポート表](microsoft-jdbc-driver-for-sql-server-support-matrix.md#java-and-jdbc-specification-support)を見て、サポートされているドライバー バージョンの中で利用できるものがあるか確認してください。 Microsoft は Java 接続のサポートの向上を継続的に進めています。 そのため、最新バージョンの Microsoft JDBC ドライバーを使用することを強くおすすめします。

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 8.4 for SQL Server (zip) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2137600)**  
**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 8.4 for SQL Server (tar.gz) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2137502)**  

### <a name="version-information"></a>バージョン情報

- リリース番号:8.4.1
- リリース日:2020 年 8 月 27 日

ドライバーをダウンロードすると、複数の JAR ファイルがあります。 JAR ファイルの名前は、サポートされている Java のバージョンを示します。

> [!Note]
> 英語以外のバージョンからこのページにアクセスしていて、最新の内容を見たい場合は、[サイトの英語 (米国) 版]()をご覧ください。 [使用できる言語](#available-languages)を選択して、英語 (米国) 版のサイトから別の言語をダウンロードできます。ます。

## <a name="available-languages"></a>使用できる言語

Microsoft JDBC Driver for SQL Server のこのリリースは、次の言語で利用できます。

Microsoft JDBC Driver 8.4.1 for SQL Server (zip):[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x40a)

Microsoft JDBC Driver 8.4.1 for SQL Server (tar.gz):[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x40a)

### <a name="release-notes"></a>リリース ノート

このリリースの詳細については、[リリース ノート](release-notes-for-the-jdbc-driver.md)と[システム要件](system-requirements-for-the-jdbc-driver.md)をご覧ください。

### <a name="previous-releases"></a>以前のリリース

以前のリリースをダウンロードするには、[以前の Microsoft JDBC Driver for SQL Server のリリース](release-notes-for-the-jdbc-driver.md#previous-releases)に関する記事を参照してください。

## <a name="using-the-jdbc-driver-with-maven-central"></a>JDBC ドライバーと Maven Central の使用

JDBC ドライバーを Maven プロジェクトに追加するには、次のコードを使って POM.xml ファイルに依存関係としてこれを追加します。

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>8.4.1.jre11</version>
</dependency>
```  

## <a name="unsupported-drivers"></a>サポートされていないドライバー

サポートされていないバージョンのドライバーは、ここではダウンロードできません。 Microsoft は Java 接続のサポートの向上を継続的に進めています。 そのため、最新バージョンの Microsoft JDBC ドライバーを使用することを強くおすすめします。  
  
## <a name="next-steps"></a>次のステップ

SQL Server 用 Microsoft JDBC Driver の詳細については、「[JDBC ドライバーの概要](overview-of-the-jdbc-driver.md)」と [JDBC ドライバーの GitHub リポジトリ](https://github.com/microsoft/mssql-jdbc/blob/dev/README.md)を参照してください。