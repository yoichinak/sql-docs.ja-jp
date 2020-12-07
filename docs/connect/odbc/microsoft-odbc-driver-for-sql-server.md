---
title: Microsoft SQL Server 用 ODBC Driver
description: Microsoft ODBC Driver for SQL Server を使うと、標準の ODBC API を使用して SQL Server や Azure SQL Database に接続できます。
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9f2ae91b-06af-4c9a-9d24-062df7bc4662
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b17517d0a4a904c5a8ffa56a625ba092c6b79b41
ms.sourcegitcommit: 6f49804b863fed44968ea5829e2c26edc5988468
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2020
ms.locfileid: "87807045"
---
# <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft SQL Server 用 ODBC Driver

[!INCLUDE[ODBC_Current_Version](../../includes/odbc-latest-release.md)]

[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

ODBC は、C と C++ で記述された SQL Server 用アプリケーションのプライマリ ネイティブ データ アクセス API です。 ほとんどのデータ ソース用の ODBC ドライバーがあります。 他には、COBOL、Perl、PHP、Python などの言語で ODBC を使用できます。 ODBC は、データ統合シナリオで広く使用されます。

ODBC ドライバーには、[**sqlcmd**](../../tools/sqlcmd-utility.md) や [**bcp**](../../tools/bcp-utility.md) などのツールが付属してします。 **sqlcmd** ユーティリティを使用すると、Transact-SQL ステートメント、システム プロシージャ、SQL スクリプトを実行できます。 **bcp** ユーティリティは、ユーザーが選択した形式で、Microsoft SQL Server インスタンスとデータ ファイルとの間でデータの一括コピーを行います。 **bcp** を使用して、大量の新規行を SQL Server テーブルにインポートしたり、データをテーブルからデータ ファイルにエクスポートしたりできます。  

## <a name="code-example-in-c"></a>C++ でのコードの例

次の C++ のサンプルでは、ODBC API を使用してデータベースに接続し、アクセスする方法を示します。

- [ODBC を使用する C++ コードの例](../../odbc/reference/sample-odbc-program.md)

## <a name="download"></a>ダウンロード

- ![Download-DownArrow-Circled](../../ssms/media/download-icon.png)[ODBC ドライバーをダウンロードするには](download-odbc-driver-for-sql-server.md)

## <a name="documentation"></a>ドキュメント

### <a name="features"></a>特徴

- [カスタム キーストア プロバイダー](../../connect/odbc/custom-keystore-providers.md)
- [データ分類](../../connect/odbc/data-classification.md)
- [DSN と接続文字列のキーワードと属性](dsn-connection-string-attribute.md)
- [SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md) (使用できる機能は、OLEDB なしで、ODBC Driver for SQL Server にも適用されます)
- [Always Encrypted の使用](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [Azure Active Directory の使用](../../connect/odbc/using-azure-active-directory.md)
- [透過的なネットワーク IP の解決の使用](../../connect/odbc/using-transparent-network-ip-resolution.md)
- [XA トランザクションの使用](../../connect/odbc/use-xa-with-dtc.md)

### <a name="linux-and-macos"></a>Linux と macOS

- [Linux へのドライバーのインストール](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [macOS へのドライバーのインストール](../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)
- [SQL Server への接続](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)
- [**bcp** による接続](../../connect/odbc/linux-mac/connecting-with-bcp.md)
- [**sqlcmd** による接続](../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)
- [データ アクセスのトレース](../../connect/odbc/linux-mac/data-access-tracing-with-the-odbc-driver-on-linux.md)
- [よく寄せられる質問](../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)
- [ドライバー マネージャーのインストール](../../connect/odbc/linux-mac/installing-the-driver-manager.md)
- [既知の問題](../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)
- [プログラミング ガイドライン](../../connect/odbc/linux-mac/programming-guidelines.md)
- [リリース ノート](../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)
- [リリース ノート (mssql-tools)](../../connect/odbc/linux-mac/release-notes-tools.md)
- [高可用性とディザスター リカバリーのサポート](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
- [統合認証を使用する (Kerberos)](../../connect/odbc/linux-mac/using-integrated-authentication.md)

### <a name="windows"></a>Windows

- [非同期実行 (通知方法) の例](../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)
- [Windows ODBC ドライバーの接続の復元性](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
- [ドライバー対応接続プール](../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)
- [機能と動作の変更](../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)
- [Windows 上の SQL Server に対する ODBC のリリース ノート](windows/release-notes-odbc-sql-server-windows.md)
- [システム要件、インストール、およびドライバー ファイル](../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)

## <a name="community"></a>コミュニティ

- [SQL Server ドライバーのブログ](https://techcommunity.microsoft.com/t5/SQL-Server/bg-p/SQLServer/label-name/SQLServerDrivers)  
- [SQL Server データ アクセス フォーラム](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
