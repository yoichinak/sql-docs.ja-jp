---
title: SQL Server 2017 on Linux の新機能
description: この記事では、Linux 上で実行される SQL Server 2017 で使用できる主な機能とサービスについて説明します。
author: VanMSFT
ms.author: vanto
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5f2b955579853c48f7899614f0e87dd996f3076e
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115585"
---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>SQL Server 2017 on Linux の新機能

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

この記事では、Linux 上で実行される SQL Server 2017 で使用できる主な機能とサービスについて説明します。

> [!NOTE]
> この記事に含まれているこれらの機能に加えて、累積的な更新プログラムが定期的にリリースされます。 これらの累積的な更新プログラムでは、多くの機能強化と修正が提供されます。 最新の CU リリースについて詳しくは、[https://aka.ms/sql2017cu](https://aka.ms/sql2017cu) を参照してください。 パッケージのダウンロードと既知の問題については、[リリース ノート](sql-server-linux-release-notes.md)のページをご覧ください。

## <a name="ubuntu-1804-supported"></a>Ubuntu 18.04 をサポート

SQL Server 2017 CU20 以降では、Ubuntu 18.04 がサポートされるようになりました。 [Ubuntu での SQL Server のインストールとデータベースの作成](quickstart-install-connect-ubuntu.md?view=sql-server-2017)に関するクイック スタートを参照してください。

## <a name="rhel-8-supported"></a>RHEL 8 をサポート

SQL Server 2017 CU20 以降では、RHEL 8 がサポートされるようになりました。 [Red Hat での SQL Server のインストールとデータベースの作成](quickstart-install-connect-red-hat.md?view=sql-server-2017)に関するクイック スタートを参照してください。

## <a name="sql-server-database-engine"></a>SQL Server データベース エンジン

- コア SQL Server データベース エンジンの機能が有効になりました。
- ネイティブ Linux パスのサポート。
- IPv6 のサポート。
- NFS 上のデータベース ファイルのサポート。
- [トランスポート層セキュリティ](sql-server-linux-encrypted-connections.md) (TLS) の暗号化が有効になりました。
- [Active Directory 認証](sql-server-linux-active-directory-authentication.md)が有効になりました。
- 高可用性のための[可用性グループ機能](sql-server-linux-availability-group-overview.md)。
- [フルテキスト検索](sql-server-linux-setup-full-text-search.md)のサポート。

## <a name="sql-server-agent"></a>SQL Server エージェント

- 次のタスクに対する [SQL Server エージェント](sql-server-linux-setup-sql-agent.md)のサポートが有効になりました。
  - [Transact-SQL ジョブ](sql-server-linux-run-sql-server-agent-job.md)
  - [DB メール](sql-server-linux-db-mail-sql-agent.md)
  - [ログ配布](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- Linux 上で SSIS パッケージを実行する機能。 詳しくは、「[ssis-conf を使用して Linux で SQL Server Integration Services を構成する](sql-server-linux-configure-ssis.md)」をご覧ください。

## <a name="other-improvements"></a>その他の機能強化

- コマンドライン構成ツール、[mssql-confmssql-conf](sql-server-linux-configure-mssql-conf.md)。
- [環境変数](sql-server-linux-configure-environment-variables.md)での無人インストールのサポート。
- クロスプラットフォームの [Visual Studio Code mssql-server 拡張機能](../tools/visual-studio-code/sql-server-develop-use-vscode.md)。
- クロスプラットフォームのスクリプト ジェネレーター、[mssql-scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md)。
- クロスプラットフォームの動的管理ビュー (DMV) モニター、[DBFS ツール](https://github.com/Microsoft/dbfs)。

## <a name="next-steps"></a>次のステップ

SQL Server on Linux をインストールするには、次のチュートリアルのいずれかを使用します。

- [Red Hat Enterprise Linux へのインストール](quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server へのインストール](quickstart-install-connect-suse.md)
- [Ubuntu へのインストール](quickstart-install-connect-ubuntu.md)
- [Docker 上での実行](quickstart-install-connect-docker.md)
- [Azure での SQL VM プロビジョニング](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

よく寄せられる質問に対する回答については、「[SQL Server on Linux に関する FAQ](sql-server-linux-faq.md)」を参照してください。 SQL Server 2017 で導入されたその他の改善点については、「[SQL Server 2017 の新機能](../sql-server/what-s-new-in-sql-server-2017.md)」を参照してください。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]