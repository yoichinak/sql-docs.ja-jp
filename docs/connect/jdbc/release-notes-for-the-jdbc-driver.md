---
title: JDBC ドライバーのリリース ノート
description: この記事には、Microsoft JDBC Driver for SQL Server の各リリースが記載されています。 リリース バージョンごとに、変更された点とそれに関する説明が示されています。
ms.custom: ''
ms.date: 08/27/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bcbaee78dc7dcb0de053756aacfe2e1711679fe
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005670"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server のリリース ノート

この記事では、_Microsoft JDBC Driver for SQL Server_ のリリースを示します。 リリース バージョンごとに、変更された点とそれに関する説明が示されています。

## <a name="84"></a><a id="84"></a> 8.4

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 8.4 for SQL Server (zip) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2137600)**  
**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 8.4 for SQL Server (tar.gz) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2137502)**  

バージョン番号: 8.4.1  
リリース日:2020 年 8 月 27 日

自動的に検出されたもの以外の言語でドライバーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
zip ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2137600&clcid=0x40a)  
tar.gz ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2137502&clcid=0x40a)  

### <a name="compliance"></a>コンプライアンス

| コンプライアンスの変更 | 詳細 |
| :---------------- | :------ |
| JDBC Driver 8.4 用の最新の更新のダウンロード。 | &bull; &nbsp; [GitHub、8.4.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v8.4.1)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| JDBC API 仕様 4.2 への完全準拠。 | 8\.4 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされています。<br/><br/>たとえば、8.4 パッケージの mssql-jdbc-8.4.1.jre14.jar ファイルは、Java 14 で使用する必要があります。 |
| Java Development Kit (JDK) バージョン 14.0、11.0 および 1.8 と互換性があります。 | Microsoft JDBC Driver 8.4 for SQL Server は、JDK 11.0 と 1.8 に加え、Java Development Kit (JDK) バージョン 14.0 と互換性を持つようになりました。 |
| &nbsp; | &nbsp; |

### <a name="releases"></a>リリース

バージョン番号: 8.4.1  
リリース日:2020 年 8 月 27 日  
修正された問題:  

- `SQLServerConnectionPoolProxy` に `delayLoadingLobs` との互換性がない問題を修正しました
- `delayLoadingLobs` の潜在的な `NullPointerException` の問題を修正しました
- Windows Certificate Store 使用時の列暗号化キーの復号化に関する問題を修正しました

バージョン番号: 8.4.0  
リリース日:2020 年 7 月 31 日  

### <a name="support-for-jdk-14"></a>JDK 14 のサポート

Microsoft JDBC Driver 8.4 for SQL Server は、JDK 11.0 と 1.8 に加え、Java Development Kit (JDK) バージョン 14.0 と互換性を持つようになりました。

### <a name="added-support-for-authentication-to-azure-key-vault-using-managed-identity"></a>マネージド ID を使用した Azure Key Vault への認証のサポートを追加

| 認証の種類の追加 | 説明 |
| :---------- | :------ |
| Microsoft JDBC Driver 8.4 for SQL Server で、マネージド ID を使用した Azure Key Vault への認証がサポートされるようになりました。 | 「[JDBC ドライバーでの Always Encrypted の使用](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)」を参照してください。 |
| &nbsp; | &nbsp; |

### <a name="extended-support-for-bulk-copy-for-azure-data-warehouse"></a>Azure Data Warehouse の一括コピーの拡張サポート

| Azure Data Warehouse の一括コピーの変更 | 詳細 |
| :------------------- | :------ |
| Microsoft JDBC Driver 8.4 には、新しい接続プロパティである `sendTemporalDataTypesAsStringForBulkCopy` が追加されています。 このブール型プロパティの既定値は TRUE です。 | 「[JDBC ドライバーでの一括コピーの使用](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)」を参照してください。 |
| &nbsp; | &nbsp; |

### <a name="added-support-for-azure-sql-dns-caching"></a>Azure SQL DNS キャッシュのサポートを追加

| DNS キャッシュ | 詳細 |
| :------------------- | :------ |
| Microsoft JDBC Driver 8.4 for SQL Server では、Azure SQL Server に対する DNS キャッシュがサポートされるようになりました。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="added-backwards-compatibility-for-streaming-lob-objects"></a>LOB オブジェクトのストリーミングとの下位互換性を追加

| LOB ストリーミング | 説明 |
| :------------------- | :------ |
| Microsoft JDBC Driver 8.4 for SQL Server には、新しい接続プロパティである `delayLoadingLobs` が追加されました。 | `delayLoadingLobs` を FALSE に設定すると、結果セットから取得されるすべての LOB オブジェクトがストリーミングされなくなります。 これは、バージョン 6.4 リリースより前のドライバーの動作と同様に、ドライバーが LOB オブジェクト全体をメモリに一度に読み込むことを意味します。 |
| &nbsp; | &nbsp; |

### <a name="added-support-for-client-certificate-authentication-for-loopback-scenarios"></a>Loopback シナリオにおけるクライアント証明書認証のサポートを追加

| クライアント証明書認証 | 説明 |
| :------------------- | :------ |
| Microsoft JDBC Driver 8.4 for SQL Server には、Loopback シナリオ向けにクライアント証明書認証と呼ばれる新しい認証方法が追加されました。 | 「[Loopback シナリオにおけるクライアント証明書の認証](../../connect/jdbc/client-certification-authentication-for-loopback-scenarios.md)」を参照してください。 |

## <a name="previous-releases"></a>以前のリリース

## <a name="82"></a><a id="82"></a> 8.2

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 8.2 for SQL Server (zip) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122433)**  
**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 8.2 for SQL Server (tar.gz) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122536)**  

バージョン番号: 8.2.2 リリース日:2020 年 3 月 24 日

自動的に検出されたもの以外の言語でドライバーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
zip ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122433&clcid=0x40a)  
tar.gz ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122536&clcid=0x40a)  

### <a name="compliance"></a>コンプライアンス

| コンプライアンスの変更 | 詳細 |
| :---------------- | :------ |
| JDBC Driver 8.2 用の最新の更新のダウンロード。 | &bull; &nbsp; [GitHub、8.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v8.2.2)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| JDBC API 仕様 4.2 への完全準拠。 | 8\.2 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされています。<br/><br/>たとえば、8.2 パッケージの mssql-jdbc-8.2.2.jre11.jar ファイルは、Java 11 で使用する必要があります。 |
| Java Development Kit (JDK) バージョン 13.0、11.0 および 1.8 と互換性があります。 | Microsoft JDBC Driver 8.2 for SQL Server は、JDK 11.0 と 1.8 に加え、Java Development Kit (JDK) バージョン 13.0 と互換性を持つようになりました。 |
| &nbsp; | &nbsp; |

### <a name="releases"></a>リリース

バージョン番号: 8.2.2  
リリース日:2020 年 3 月 24 日  
修正された問題:  

- 信頼済みの Azure Key Vault エンドポイントの一覧を構成するオプションを追加

バージョン番号: 8.2.1  
リリース日:2020 年 2 月 26 日  
修正された問題:  

- `SQLServerResultSet.getObject()` を使用して `java.time.LocalTime` または `java.time.LocalDate` としてデータを取得するときの潜在的な `NullPointerException` の問題を修正しました

バージョン番号: 8.2.0  
リリース日:2020 年 1 月 31 日  

### <a name="support-for-jdk-13"></a>JDK 13 のサポート

Microsoft JDBC Driver 8.2 for SQL Server は、JDK 11.0 と 1.8 に加え、Java Development Kit (JDK) バージョン 13.0 と互換性を持つようになりました。

### <a name="always-encrypted-with-secure-enclaves"></a>セキュア エンクレーブを使用する Always Encrypted

| Always Encrypted の変更 | 詳細 |
| :--------- | :------ |
| Microsoft JDBC Driver 8.2 for SQL Server では、セキュア エンクレーブを使用する Always Encrypted がサポートされるようになりました。 詳細については、以下を参照してください。セキュリティで保護されたエンクレーブが設定された Always Encrypted |
| 詳細情報とサンプル コード。 | 「[セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../connect/jdbc/using-always-encrypted-with-secure-enclaves-with-the-jdbc-driver.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

### <a name="performance-improvement-when-retrieving-temporal-datatypes-from-sql-server-sup1sup"></a>SQL Server <sup>1</sup> からテンポラル データ型を取得するときのパフォーマンスの向上

| テンポラル データ型の変更 | 詳細 |
| :---------- | :------ |
| Microsoft JDBC Driver 8.2 for SQL Server では、SQL Server からテンポラル データ型を取得するときのパフォーマンスが向上しています。 | この変更により、可能な場合、java.util.Calendar を使用する必要がなくなるため、不要なテンポラル データ型変換を行わなくて済みます。 |
| このパフォーマンス向上の影響を受けているテンポラル データ型の一覧を次に示します。SQL Server データ型に続き、それぞれの Java マッピングが括弧内に記載されています。 | date (java.sql.Date)、datetime (java.sql.Timestamp)、datetime2 (java.sql.Timestamp)、smalldatetime (java.sql.Timestamp)、time (java.sql.Time)。 |
| &nbsp; | &nbsp; |

<sup>1</sup> java.util.Calendar と java.time.LocalDateTime API の間でタイム ゾーンの処理方法に違いがあるため、ユーザーが指定した java.util.Calendar オブジェクトに関連付けられたテンポラル データ型、または microsoft.sql.DateTimeOffset データ型は、このパフォーマンス向上からメリットを得られません。

### <a name="deployment-of-mssql-jdbc_auth-version-archdll-previously-sqljdbc_authdll-to-maven-repository"></a>Maven リポジトリへの mssql-jdbc_auth-\<version>-\<arch>.dll (previously sqljdbc_auth.dll) の展開

| sqljdbc_auth.dll change | 詳細 |
| :------------------- | :------ |
| Microsoft JDBC Driver 8.2 for SQL Server 以降では、ドライバーは、Azure Active Directory 認証機能を使用するために、sqljdbc_auth.dll ではなく mssql-jdbc_auth-\<version>-\<arch>.dll に依存しています。 | &nbsp; |
| また、簡単にアクセスできるように、DLL も Maven リポジトリにアップロードされています。 | [このページ](https://search.maven.org/artifact/com.microsoft.sqlserver/mssql-jdbc_auth)を参照してください。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>既知の問題

| 既知の問題 | 詳細 |
| :----------- | :------ |
| Java 8 でセキュア エンクレーブを使用する Always Encrypted を使用する場合。 | ユーザーは、BouncyCastle プロバイダーを依存関係として含めるか、または RSASSA-PSS 署名アルゴリズムをサポートするセキュリティ プロバイダーをマップするか読み込む必要があります。 |
| &nbsp; | &nbsp; |

## <a name="a-id74-741"></a><a id="74"> 7.4.1

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 7.4.1 for SQL Server (self-extracting exe) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122712)**  
**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 7.4.1 for SQL Server (tar.gz) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122613)**  

バージョン番号: 7.4.1  
リリース日:2019 年 8 月 2 日

自動的に検出されたもの以外の言語でドライバーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
自己解凍形式 exe ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122712&clcid=0x40a)  
tar.gz ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122613&clcid=0x40a)  

### <a name="compliance"></a>コンプライアンス

| コンプライアンスの変更 | 詳細 |
| :---------------- | :------ |
| JDBC Driver 7.4 用の最新の更新のダウンロード。 | &bull; &nbsp; [GitHub, 7.4.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.4.1)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| JDBC API 仕様 4.2 への完全準拠。 | 7\.4 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされています。<br/><br/>たとえば、7.4 パッケージの mssql-jdbc-7.4.1.jre11.jar ファイルは、Java 11 で使用する必要があります。 |
| Java Development Kit (JDK) バージョン 12.0、11.0 および 1.8 と互換性があります。 | Microsoft JDBC Driver 7.4 for SQL Server は、JDK 11.0 と 1.8 に加え、Java Development Kit (JDK) バージョン 12.0 と互換性を持つようになりました。 |
| &nbsp; | &nbsp; |

### <a name="releases"></a>リリース

バージョン番号: 7.4.1  
リリース日:2019 年 8 月 2 日  
修正された問題:  

- API の変更によって下位互換性が損なわれたため、新しい `hashCode()` および `equals()` API の実装が `SQLServerDataTable` および `SQLServerDataColumn` から取り消されました

バージョン番号: 7.4.0  
リリース日:2019 年 7 月 31 日  

### <a name="support-for-jdk-12"></a>JDK 12 のサポート

Microsoft JDBC Driver 7.4 for SQL Server は、JDK 11.0 と 1.8 に加え、Java Development Kit (JDK) バージョン 12.0 と互換性を持つようになりました。

### <a name="introduces-ntlm-authentication"></a>NTLM 認証の導入

| NTLM の変更 | 詳細 |
| :--------- | :------ |
| NTLM 認証モードのサポート。 | この認証モードでは、Windows クライアントと Windows 以外のクライアントの両方が Windows ドメイン ユーザーを使用して SQL Server に対して自身の認証を行うことができます。 |
| この認証モードを使用するための詳細とサンプル アプリケーション。 | [NTLM 認証を使用した接続](using-ntlm-authentication-to-connect-to-sql-server.md)に関するページを参照してください。 |
| &nbsp; | &nbsp; |

### <a name="introduces-querying-parametermetadata-via-_usefmtonly_"></a>_useFmtOnly_ を使用した ParameterMetaData のクエリの導入

| useFmtOnly の変更 | 詳細 |
| :---------- | :------ |
| **useFmtOnly** 接続プロパティの追加。 | この機能を使用すると、ユーザーは `SET FMTONLY ON` レガシ API を使用して必要に応じて ParameterMetaData にクエリを実行できます。 これは、`sp_describe_undeclared_parameters` が想定どおりに実行されないシナリオに役立ちます。 |
| 詳細と制限。 | 「[useFMTOnly の使用](using-usefmtonly.md)」をご覧ください |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-key-vault-sdk-for-java_-version-121"></a>_Microsoft Azure Key Vault SDK for Java_ を更新 (バージョン 1.2.1)

| Key Vault SDK の変更 | 詳細 |
| :------------------- | :------ |
| _Microsoft Azure Key Vault SDK for Java_ の Maven の依存関係がバージョン 1.2.1 に更新されました。 | &nbsp; |
| Maven の依存関係としての _Microsoft Azure SDK for Key Vault WebKey_ が削除されます。 | &nbsp; |
| 追加の詳細。 | 「[Feature dependencies of the Microsoft JDBC Driver for SQL Server (Microsoft JDBC Driver for SQL Server の機能の依存関係)](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>既知の問題

| 既知の問題 | 詳細 |
| :----------- | :------ |
| NTLM 認証を使用するとき。 | 現在、拡張保護と暗号化された接続を同時に有効化することはできません。 |
| useFmtOnly を使用するとき。 | SQL の解析ロジックの欠陥に起因する、いくつかの機能のイシューがあります。 詳細と回避策の提案については、[useFmtOnly の使用](using-usefmtonly.md)に関するページを参照してください。 |
| &nbsp; | &nbsp; |

## <a name="a-id72-722"></a><a id="72"> 7.2.2

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 7.2.2 for SQL Server (自己解凍形式 exe) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122435)**  
**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 7.2.2 for SQL Server (tar.gz) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122434)**  

バージョン番号: 7.2.2  
リリース日:2019 年 4 月 16 日

自動的に検出されたもの以外の言語でドライバーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
自己解凍形式 exe ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122435&clcid=0x40a)  
tar.gz ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122434&clcid=0x40a)  

### <a name="compliance"></a>コンプライアンス

| コンプライアンスの変更 | 詳細 |
| :---------------- | :------ |
| JDBC Driver 7.2 用の最新の更新のダウンロード。 | &bull; &nbsp; [GitHub, 7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| JDBC API 仕様 4.2 への完全準拠。 | 7\.2 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされています。<br/><br/>たとえば、7.2 パッケージの mssql-jdbc-7.2.2.jre11.jar ファイルは、Java 11 で使用する必要があります。 |
| Java Development Kit (JDK) バージョン 11.0 および JDK 1.8 と互換性があります。 | Microsoft JDBC Driver 7.2 for SQL Server は、JDK 1.8 に加え、Java Development Kit (JDK) バージョン 11.0 と互換性を持つようになりました。 |
| &nbsp; | &nbsp; |

### <a name="releases"></a>リリース

バージョン番号: 7.2.2  
リリース日:2019 年 4 月 16 日  
修正された問題:  

- ActivityID が適切にクリーンアップされない問題を修正しました

バージョン番号: 7.2.1  
リリース日:2019 年 2 月 11 日  
修正された問題:  

- 特定のパラメーター化されたクエリに関する問題を修正しました

バージョン番号: 7.2.0  
リリース日:2019 年 1 月 31 日  

### <a name="active-directory-_managed-identity_-msi-authentication"></a>Active Directory _マネージド ID_ (MSI) 認証

| MSI の変更 | 詳細 |
| :--------- | :------ |
| Active Directory マネージド ID (MSI) 認証モードのサポート。 | この認証モードは、"ID" 機能の有効化がサポートされている Azure リソースに適用できます。<br/><br/>ドライバーによって両方の種類のマネージド ID (MSI) がサポートされ、セキュリティで保護された接続を確立するための **accessToken** が取得されます。 |
| この認証モードを使用するための詳細とサンプル アプリケーション。 | 「[Connecting using Azure Active Directory Authentication (Azure Active Directory 認証を利用した接続)](connecting-using-azure-active-directory-authentication.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

### <a name="introduces-_open-service-gateway-initiative_-osgi-support"></a>"_オープン サービス ゲートウェイ イニシアチブ_" (OSGi) のサポートを導入

| OSGi の変更 | 詳細 |
| :---------- | :------ |
| **DataSourceFactory** の実装の追加。 | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| **アクティベーター**の実装の追加。 | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-_sqlservererror_-apis"></a>_SQLServerError_ API を導入

| エラー API の変更 | 詳細 |
| :--------------- | :------ |
| SQLServerError API が導入されました。 | 生成されたエラーの追加の詳細をサーバーから取得する getter API。<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| 追加の詳細。 | 「[Handling Errors (エラーの処理)](handling-errors.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-active-directory-authentication-library-adal4j-for-java_-version-163"></a>"_Microsoft Azure Active Directory 認証ライブラリ (ADAL4J) for Java_" の更新、バージョン 1.6.3

| ADAL4J の変更 | 詳細 |
| :------------ | :------ |
| ADAL4J の Maven の依存関係がバージョン 1.6.3 に更新されました。 | &nbsp; |
| Maven の依存関係として、_Java Client Runtime for AutoRest_ が導入されています (バージョン 1.6.5)。 | &nbsp; |
| 追加の詳細。 | 「[Feature dependencies of the Microsoft JDBC Driver for SQL Server (Microsoft JDBC Driver for SQL Server の機能の依存関係)](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

### <a name="updated-_microsoft-azure-key-vault-sdk-for-java_-version-120"></a>_Microsoft Azure Key Vault SDK for Java_ を更新 (バージョン 1.2.0)

| Key Vault SDK の変更 | 詳細 |
| :------------------- | :------ |
| _Microsoft Azure Key Vault SDK for Java_ の Maven の依存関係がバージョン 1.2.0 に更新されました。 | &nbsp; |
| Maven の依存関係として _Microsoft Azure SDK for Key Vault WebKey_、バージョン 1.2.0 が導入されます。 | &nbsp; |
| 追加の詳細。 | 「[Feature dependencies of the Microsoft JDBC Driver for SQL Server (Microsoft JDBC Driver for SQL Server の機能の依存関係)](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)」をご覧ください。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>既知の問題

| 既知の問題 | 詳細 |
| :----------- | :------ |
| クエリがパラメーター化される場合があります。 | この問題に対応するために、7.2.0 バージョンの更新である v7.2.1 が 2019 年 2 月にリリースされました。 |
| ActivityId のクリーンアップ。 | この問題に対応するために、7.2.1 バージョンの更新である v7.2.2 が 2019 年 4 月にリリースされました。 |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 7.0 for SQL Server (自己解凍形式 exe) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122713)**  
**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 7.0 for SQL Server (tar.gz) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122614)**  

バージョン番号: 7.0.0  
リリース日:2018 年 7 月 31日

自動的に検出されたもの以外の言語でドライバーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
自己解凍形式 exe ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122713&clcid=0x40a)  
tar.gz ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122614&clcid=0x40a)  

Microsoft JDBC Driver 7.0 for SQL Server は、JDBC API 仕様 4.2 に完全に準拠しています。 7\.0 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされます。 たとえば、7.0 パッケージの mssql-jdbc-7.0.0.jre10.jar ファイルは、Java 10 で使用する必要があります。

### <a name="support-for-jdk-10"></a>JDK 10 のサポート

Microsoft JDBC Driver 7.0 for SQL Server は、JDK 1.8 に加え、Java Development Kit (JDK) バージョン 10.0 と互換性を持つようになりました。 さらに、この更新により、ドライバーの `Automatic-Module-Name` が、MANIFEST ファイルを通して `com.microsoft.sqlserver.jdbc` として公開されます。

### <a name="support-for-spatial-datatypes"></a>空間データ型のサポート

Microsoft JDBC Driver 7.0 for SQL Server で、SQL Server の空間データ型である Geography と Geometry のサポートが提供されるようになりました。 空間データ型の API の詳細とそれらの使用方法については、「[空間データ型の使用](use-spatial-datatypes.md)」を参照してください。

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>JDBC 4.3 の実装で、java.sql.Connection の API beginRequest() と endRequest() が導入されました。

Microsoft JDBC Driver 7.0 for SQL Server で、`java.sql.Connection` クラスから `beginRequest()` API と `endRequest()` API が実装されるようになりました。 これらの API は、JDBC 4.3 仕様と JDK 9 で導入されました。 ドライバーでのこれらの API の実装の詳細については、「[JDBC Driver の JDBC 4.3 への準拠](jdbc-4-3-compliance-for-the-jdbc-driver.md)」を参照してください。

### <a name="support-for-sql-data-discovery-and-classification"></a>SQL データの検出と分類のサポート

Microsoft JDBC Driver 7.0 for SQL Server には、SQL データの検出と分類に関するサポートが、この機能に対応している任意のターゲット データベースに向けて用意されています。 ドライバーで、フェッチされた `ResultSet` からこの情報を抽出するための `SQLServerResultSet.getSensitivityClassification()` API が公開されるようになりました。

JDBC Driver でこの機能を使用する方法の詳細については、「[SQL データの検出と分類](data-discovery-classification-sample.md)」内の例を参照してください。

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>接続プロパティ useBulkCopyForBatchInsert を追加

Microsoft JDBC Driver 7.0 for SQL Server には、新しい接続プロパティである `useBulkCopyForBatchInsert` が導入されています。 このプロパティは、Azure Synapse Analytics に対してのみサポートされます。

このプロパティは、既定では無効になっています。 Azure Synapse Analytics に大量のデータをプッシュするときに、それを有効にすることで、ユーザー アプリケーションのパフォーマンスを向上させることができます。 このプロパティを有効にすると、バッチ挿入操作の動作が変更され、ユーザー指定のデータを一括コピーする操作に切り替わります。 このプロパティとその制約については、「[Using Bulk Copy API for batch insert operation (一括挿入操作での Bulk Copy API の使用)](use-bulk-copy-api-batch-insert-operation.md)」を参照してください。

### <a name="added-connection-property-cancelquerytimeout"></a>接続プロパティ cancelQueryTimeout を追加

Microsoft JDBC Driver 7.0 for SQL Server には、新しい接続プロパティである `cancelQueryTimeout` が導入されています。これは `java.sql.Connection` オブジェクトと `java.sql.Statement` オブジェクトの `queryTimeout` をキャンセルします。

### <a name="added-azure-key-vault-provider-constructors"></a>Azure Key Vault プロバイダー コンストラクターを追加

Microsoft JDBC Driver 7.0 for SQL Server には、以前削除された `SQLServerColumnEncryptionAzureKeyVaultProvider` 用のコンストラクターが再び導入されています。 それは `SQLServerKeyVaultAuthenticationCallback` で実装されたカスタム メソッドを通して認証を行うことを可能にしていました。

新しいコンストラクターには、次の定義が含まれています。

```java
/* This constructor is added to provide backward compatibility with 6.0
* version of the driver. It is marked deprecated for removal in the next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-160"></a>"Microsoft Azure Active Directory 認証ライブラリ (ADAL4J) for Java" の更新、バージョン:1.6.0

Microsoft JDBC Driver 7.0 for SQL Server では、"Java 用 Microsoft Azure Active Directory 認証ライブラリ (ADAL4J)" に関する Maven の依存関係が 1.6.0 に更新されています。 依存関係の詳細については、「[Microsoft JDBC Driver for SQL Server の機能の依存関係](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)」をご覧ください。

## <a name="64"></a>6.4

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 6.4 for SQL Server (self-extracting exe) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122436)**  
**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 6.4 for SQL Server (tar.gz) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122537)**  

バージョン番号: 6.4.0  
リリース日:2018 年 2 月 27 日

自動的に検出されたもの以外の言語でドライバーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
自己解凍形式 exe ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122436&clcid=0x40a)  
tar.gz ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122537&clcid=0x40a)  

Microsoft JDBC Driver 6.4 for SQL Server は、JDBC 仕様 4.1 および 4.2 に完全に準拠しています。 6\.4 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされています。 たとえば、6.4 パッケージの mssql-jdbc-6.4.0.jre8.jar ファイルは、Java 8 で使用する必要があります。

### <a name="support-for-jdk-9"></a>JDK 9 のサポート

ドライバーでは、JDK 8.0 および 7.0 に加えて JDK バージョン 9.0 がサポートされています。

### <a name="jdbc-43-compliance"></a>JDBC 4.3 に準拠

ドライバーでは、Java Database Connectivity API 4.1 および 4.2 に加えて、4.3 の仕様もサポートされます。 JDBC 4.3 API メソッドは追加されていますが、まだ実装されていません。 詳細については、「[JDBC Driver の JDBC 4.3 への準拠](jdbc-4-3-compliance-for-the-jdbc-driver.md)」をご覧ください。

### <a name="added-connection-property-sslprotocol"></a>接続プロパティ sslProtocol を追加

新しい接続プロパティを使用して、TLS プロトコルのキーワードを指定できます。 次のいずれかの値になります。"TLS"、"TLSv1"、"TLSv 1.1"、および "TLSv 1.2"。 詳細については、「[SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)」を参照してください。

### <a name="deprecated-connection-property-fipsprovider"></a>非推奨の接続プロパティ fipsProvider

接続プロパティ `fipsProvider` は、指定できる接続プロパティの一覧から削除されています。 詳細については、関連する [GitHub pull request](https://github.com/Microsoft/mssql-jdbc/pull/460) を参照してください。

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>カスタムの TrustManager を指定するための接続プロパティを追加

ドライバーでは、`trustManagerClass` および `trustManagerConstructorArg` 接続プロパティの追加によって、カスタムの TrustManager の指定がサポートされるようになりました。 Java 仮想マシン (JVM) 環境でのグローバル設定の変更なしで、信頼できる一連の証明書を接続ごとに動的に指定できます。

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>テーブル値パラメーターでの datetime/smallDatetime 型のサポートを追加

ドライバーでは、テーブル値パラメーター (TVP) を使用している場合に、`datetime` および `smallDatetime` データ型がサポートされるようになりました。

### <a name="added-support-for-the-sql_variant-datatype"></a>sql_variant データ型のサポートを追加

JDBC ドライバーでは、SQL Server で使用する `sql_variant` データ型がサポートされるようになりました。 `sql_variant` データ型は、TVP や一括コピーなどの機能でもサポートされますが、次の制約があります。

* **日付の値の場合**:

  `sql_variant` 列に `datetime` 値、`smalldatetime` 値、または `date` 値が格納されているテーブルに TVP を使用して入力する場合、結果セットに対する `getDateTime()` メソッド、`getSmallDateTime()` メソッド、または `getDate()` メソッドの呼び出しは機能せず、次の例外がスローされます。

  `java java.lang.String cannot be cast to java.sql.Timestamp`

  回避策として、代わりに `getString()` メソッドまたは `getObject()` メソッドを使用してください。

* **null 値に対して TVP を sql_variant と共に使用する**:
  
  TVP を使用してテーブルに入力しているときに、`sql_variant` 型の列に NULL 値を送信した場合、例外が発生します。 TVPでの `sql_variant` 型の列への NULL 値の挿入は、現在サポートされていません。

### <a name="implemented-prepared-statement-metadata-caching"></a>準備されたステートメントのメタデータのキャッシュを実装

JDBC Driver では、パフォーマンスを向上させるための準備されたステートメントのメタデータのキャッシュが実装されています。 ドライバーでは、準備されたステートメントのメタデータをドライバー内でキャッシュすることがサポートされるようになりました。これには、接続プロパティ `disableStatementPooling` と `statementPoolingCacheSize` が使用されます。 この機能は、既定では無効化されています。 詳細については、「[Prepared statement metadata caching for the JDBC Driver (JDBC Driver での準備されたステートメントのメタデータのキャッシュ)](prepared-statement-metadata-caching-for-the-jdbc-driver.md)」を参照してください。

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmacos"></a>Linux/macOS での Azure AD 統合認証のサポートを追加

JDBC ドライバーでは、サポート対象のすべてのオペレーティング システム (Windows、Linux、macOS) 上で Kerberos を使った Azure Active Directory (Azure AD) 統合認証がサポートされるようになりました。 別の方法として、Windows オペレーティング システムでは、ユーザーは mssql-jdbc_auth-\<version>-\<arch>.dll を使用して認証することができます。

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>"Microsoft Azure Active Directory 認証ライブラリ (ADAL4J) for Java" の更新、バージョン:1.4.0

SQL Server 用 Microsoft JDBC Driver 7.0 では、"Microsoft Azure Active Directory 認証ライブラリ (ADAL4J) for Java" に関する Maven の依存関係が 1.4.0 に更新されています。 依存関係の詳細については、「[Microsoft JDBC Driver for SQL Server の機能の依存関係](feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)」をご覧ください。

## <a name="62"></a>6.2

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 6.2 for SQL Server (自己解凍形式 exe) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122616)**  
**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 6.2 for SQL Server (tar.gz) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122615)**  

バージョン番号: 6.2.2  
リリース日:2017 年 9 月 29 日

自動的に検出されたもの以外の言語でドライバーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
自己解凍形式 exe ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122616&clcid=0x40a)  
tar.gz ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122615&clcid=0x40a)  

SQL Server 用 Microsoft JDBC Driver 6.2 は、JDBC 仕様 4.1 および 4.2 に完全に準拠しています。 6\.2 パッケージ内の jar は Java のバージョンの互換性に従って名前付けされています。 たとえば、6.2 パッケージの mssql-jdbc-6.2.2.jre8.jar ファイルは、Java 8 で使用することが推奨されています。

### <a name="releases"></a>リリース

バージョン番号: 6.2.2  
リリース日:2017 年 10 月 3 日  
修正された問題:  

- ADAL4J の依存関係がバージョン 1.2.0 に更新され、Azure Key Vault の依存関係がバージョン 1.0.0 に更新されました

バージョン番号: 6.2.1  
リリース日:2017 年 7 月 14 日  
修正された問題:  

- `preparedStatement` を使用してパラメーターなしでクエリを実行するときの問題を修正しました

バージョン番号: 6.2.0  
リリース日:2017 年 6 月 30 日  

> [!NOTE]  
> 2017 年 6 月 29 日にリリースされた JDBC 6.2 RTW で、メタデータのキャッシュの機能強化に問題があることがわかりました。 この機能強化はロールバックされ、2017 年 7 月 17 日に新しい jar (バージョン 6.2.1) がリリースされました。
>
> 別の機能強化として、Azure Key Vault に依存するライブラリのバージョンが 1.0.0 にアップグレードされ、2017 年 10 月 19 日に新しい jar (バージョン 6.2.2) がリリースされました。
>
> 上記のリンク、[GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) または [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) から JDBC Driver 6.2 の最新更新プログラムをダウンロードします。 6\.2.2 リリースの jar を使用するようにプロジェクトを更新してください。 詳細については、[6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) および [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) のリリース ノートをご覧ください。

### <a name="azure-ad-support-for-linux"></a>Linux での Azure AD のサポート

ユーザー名/パスワードとアクセス トークンによる Azure AD 認証を使用して、Linux アプリケーションを Azure SQL Database に接続します。

### <a name="fips-enabled-jvms"></a>FIPS 対応 JVM

米国連邦標準規格を満たす Federal Information Processing Standard (FIPS) 140 準拠モードで実行されている JVM で JDBC Driver を使用できるようになりました。

### <a name="kerberos-authentication-improvements"></a>Kerberos 認証の機能強化

JDBC Driver で、以下がサポートされるようになりました。

* Kerberos 構成を変更できない、または新しいトークンまたは keytab を取得できないアプリケーションでのプリンシパル/パスワードの使用。 Kerberos 認証のみが許可される SQL Server インスタンスへの認証でこの方法を使用できます。
* サーバー SPN の明示的な設定なしで Kerberos 統合認証を使用するレルム間認証。 ドライバーでは、レルムが提供されていない場合でも、自動的にそれを計算するようになりました。
* 偽装されたユーザーの資格情報をデータ ソース経由の GSS 資格情報オブジェクトとして受け入れることによる Kerberos の制約付き委任。 この偽装された資格情報を使用して、Kerberos 接続が確立されます。

### <a name="added-timeouts"></a>タイムアウトを追加

JDBC Driver では、次の構成可能なタイムアウトがサポートされるようになりました。 アプリケーションのニーズに基づいてそれらを変更できます。

* クエリを実行しているときに、タイムアウトが発生する前に待機する秒数を制御するクエリのタイムアウト。
* ソケットの読み取りまたは受け入れで、タイムアウトが発生する前に待機するミリ秒数を指定するソケットのタイムアウト。

## <a name="61"></a>6.1

バージョン番号: 6.1.0  
リリース日:2016 年 11 月 17 日  

Microsoft JDBC Driver 6.1 for SQL Server は、JDBC 仕様 4.1 および 4.2 に完全に準拠しています。 これは、JDBC ドライバーの最初のオープン ソースのリリースです。 ソース コードは [GitHub v6.1.0 タグ](https://github.com/microsoft/mssql-jdbc/releases/tag/v6.1.0)にあります。 それにより、Java のバージョンの互換性に対応する mssql-jdbc-6.1.0.jre8.jar ファイルと mssql-jdbc-6.1.0.jre7.jar ファイルがビルドされます。

## <a name="60"></a>6.0

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 6.0 for SQL Server (自己解凍形式 exe) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122617)**  
**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 6.0 for SQL Server (tar.gz) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122714)**  

バージョン番号: 6.0.8112  
リリース日:2017 年 1 月 17 日

自動的に検出されたもの以外の言語でドライバーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
自己解凍形式 exe ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122617&clcid=0x40a)  
tar.gz ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122714&clcid=0x40a)  

Microsoft JDBC Driver 6.0 for SQL Server は、JDBC 仕様 4.1 および 4.2 に完全に準拠しています。 6\.0 パッケージ内の Jar は、JDBC API のバージョンの準拠に従って名前付けされています。 たとえば、6.0 パッケージの sqljdbc42.jar ファイルは、JDBC API 4.2 準拠です。 同様に、sqljdbc41.jar ファイルは、JDBC API 4.1 準拠です。

適切な sqljdbc42.jar または sqljdbc41.jar ファイルがあることを確認するには、次のコード行を実行します。 出力が "Driver version:6.0.7507.100" であれば、JDBC Driver 6.0 パッケージがあります。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>Always Encrypted

ドライバーでは、SQL Server 2016 の Always Encrypted 機能がサポートされます。 この機能により、SQL Server インスタンスで機密データがプレーン テキストで表示されることはないことが保証されます。 Always Encrypted はアプリケーション内のデータを透過的に暗号化することによって動作します。そのため、SQL Server では暗号化データのみが処理され、プレーンテキスト値は処理されません。 SQL Server のインスタンスまたはホスト コンピューターが侵害されたとしても、攻撃者が取得できるものは機密データの暗号化テキストだけになります。 詳細については、「[JDBC ドライバーでの Always Encrypted の使用](using-always-encrypted-with-the-jdbc-driver.md)」をご覧ください。

### <a name="internationalized-domain-names"></a>国際化ドメイン名

ドライバーでは、サーバー名に関する国際化ドメイン名 (IDN) がサポートされます。 詳細については、記事「[International features of the JDBC Driver (JDBC Driver の国際化機能)](international-features-of-the-jdbc-driver.md)」の「Using International Domain Names (国際化ドメイン名の使用)」を参照してください。

### <a name="parameterized-queries"></a>パラメーター化されたクエリ

ドライバーで、サブクエリや結合など、複雑なクエリのために準備されたステートメントを使ったパラメーター メタデータの取得がサポートされました。 この機能強化を使用できるのは、SQL Server 2012 以降のバージョンを使用している場合のみであることに注意してください。

### <a name="azure-active-directory"></a>Azure Active Directory

Azure AD 認証は、Azure AD の ID を使用して Azure SQL Database v12 に接続するメカニズムです。 Azure AD 認証は、データベース ユーザーの ID を一元管理するために、SQL Server 認証の代替として使用します。

JDBC Driver 6.0 を使用して、Azure AD の資格情報を JDBC 接続文字列内に指定して Azure SQL Database に接続できます。 詳細については、「[Setting the connection properties (接続プロパティの設定)](setting-the-connection-properties.md)」の認証プロパティを参照してください。

### <a name="table-valued-parameters"></a>テーブル値パラメーター

TVP は、複数行のデータをクライアント アプリケーションから SQL Server に簡単にマーシャリングするための手段です。複数のラウンド トリップや、データ処理用の特別なサーバー側ロジックは必要ありません。 TVP を使用すると、1 つのパラメーター化コマンドで、クライアント アプリケーションで複数行のデータをカプセル化し、そのデータをサーバーに送信できます。 受信データ行はテーブル変数に格納され、Transact-SQL を使用して操作できます。 詳細については、「[テーブル値パラメーターの使用](using-table-valued-parameters.md)」を参照してください。

### <a name="always-on-availability-groups"></a>Always On 可用性グループ

ドライバーでは、AlwaysOn 可用性グループへの透過的な接続がサポートされるようになりました。 ドライバーによってサーバー インフラストラクチャの現在の Always On トポロジがすばやく検出され、現在アクティブなサーバーに透過的に接続されます。

## <a name="42"></a>4.2

**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 4.2 for SQL Server (自己解凍形式 exe) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122538)**  
**[![ダウンロード](../../ssms/media/download-icon.png) Microsoft JDBC Driver 4.2 for SQL Server (tar.gz) のダウンロード](https://go.microsoft.com/fwlink/?linkid=2122437)**  

バージョン番号: 4.2.8112  
リリース日:2015 年 8 月 24 日

自動的に検出されたもの以外の言語でドライバーをダウンロードする必要がある場合は、以下の直接リンクを使用できます。  
自己解凍形式 exe ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122538&clcid=0x40a)  
tar.gz ファイルのドライバーの場合:[簡体中国語](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x804) | [繁体中国語](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x404) | [英語 (米国)](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x409) | [フランス語](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x40c) | [ドイツ語](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x407) | [イタリア語](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x410) | [日本語](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x411) | [韓国語](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x412) | [ポルトガル語 (ブラジル)](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x416) | [ロシア語](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x419) | [スペイン語](https://go.microsoft.com/fwlink/?linkid=2122437&clcid=0x40a)  

Microsoft JDBC Driver 4.2 for SQL Server は、JDBC 仕様 4.1 および 4.2 に完全に準拠しています。 4\.2 パッケージ内の Jar は、JDBC API のバージョンの準拠に従って名前付けされています。 たとえば、4.2 パッケージの sqljdbc42.jar ファイルは、JDBC API 4.2 準拠です。 同様に、sqljdbc41.jar ファイルは、JDBC API 4.1 準拠です。

適切な sqljdbc42.jar または sqljdbc41.jar ファイルがあることを確認するには、次のコード行を実行します。 出力が "Driver version:4.2.6420.100" であれば、JDBC Driver 4.2 パッケージがあります。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>JDK 8 のサポート

ドライバーでは、JDK 7.0、6.0、および 5.0 に加え、JDK バージョン 8.0 がサポートされています。

### <a name="jdbc-41-and-42-compliance"></a>JDBC 4.1 および 4.2 への準拠

ドライバーで、Java Database Connectivity API 4.0 だけでなく、4.1 と 4.2 の仕様もサポートされるようになりました。 詳細については、「[JDBC Driver の JDBC 4.1 への準拠](jdbc-4-1-compliance-for-the-jdbc-driver.md)」および「[JDBC Driver の JDBC 4.2 への準拠](jdbc-4-2-compliance-for-the-jdbc-driver.md)」を参照してください。

### <a name="bulk-copy"></a>一括コピー

一括コピー機能を使うと、SQL Server データベースのテーブルまたはビューに大量のデータを簡単にコピーできます。 詳細については、「[JDBC ドライバーでの一括コピーの使用](using-bulk-copy-with-the-jdbc-driver.md)」をご覧ください。

### <a name="xa-transaction-rollback-option"></a>XA トランザクション ロールバック オプション

既存の準備解除されたトランザクションの自動ロールバックに向けた、新しいタイムアウト オプションがドライバーに追加されました。 詳細については、「[Understanding XA transactions (XA トランザクションについて)](understanding-xa-transactions.md)」を参照してください。

### <a name="new-kerberos-principal-connection-property"></a>新しい Kerberos プリンシパル接続プロパティ

Kerberos 接続での柔軟性を強化するために、ドライバーで新しい接続プロパティが使用されます。 詳細については、「[Kerberos 統合認証による SQL Server への接続](using-kerberos-integrated-authentication-to-connect-to-sql-server.md)」をご覧ください。

## <a name="41"></a>4.1

バージョン番号: 4.1.8112  
リリース日:2014 年 12 月 12 日

### <a name="support-for-jdk-7"></a>JDK 7 のサポート

ドライバーでは、JDK 6.0 および 5.0 に加え、JDK バージョン 7.0 がサポートされています。

## <a name="itanium-not-supported-for-jdbc-driver-applications"></a>Itanium では JDBC Driver アプリケーションがサポートされない

Microsoft JDBC Driver for SQL Server アプリケーションは、Itanium コンピューター上での実行がサポートされていません。

## <a name="see-also"></a>関連項目

[JDBC ドライバーの概要](overview-of-the-jdbc-driver.md)
