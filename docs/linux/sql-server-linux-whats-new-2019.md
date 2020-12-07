---
title: SQL Server 2019 on Linux の新機能
description: この記事では、SQL Server 2019 on Linux の新機能について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 03/12/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: d0cd1e6c7af5fd4d2f8742e88b4b8853645fe5a7
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115450"
---
# <a name="whats-new-for-sql-server-2019-on-linux"></a>SQL Server 2019 on Linux の新機能

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

この記事では、Linux 上で実行される SQL Server 2019 で使用できる主な機能とサービスについて説明します。 パッケージのダウンロードと既知の問題については、[リリース ノート](sql-server-linux-release-notes-2019.md?view=sql-server-linux-ver15)のページをご覧ください。

## <a name="ubuntu-1804-supported"></a>Ubuntu 18.04 をサポート

SQL Server 2019 CU3 以降では、Ubuntu 18.04 がサポートされるようになりました。 [Ubuntu での SQL Server のインストールとデータベースの作成](quickstart-install-connect-ubuntu.md?view=sql-server-linux-ver15)に関するクイック スタートを参照してください。

## <a name="rhel-8-supported"></a>RHEL 8 をサポート

SQL Server 2019 CU1 以降では、RHEL 8 がサポートされるようになりました。 [Red Hat での SQL Server のインストールとデータベースの作成](quickstart-install-connect-red-hat.md?view=sql-server-linux-ver15)に関するクイック スタートを参照してください。

## <a name="updates"></a>更新プログラム

SQL Server 2019 on Linux では、次の更新が行われています。

| 新機能または更新 | 詳細 |
|:-----|:-----|
|レプリケーションのサポート |[Linux での SQL Server のレプリケーション](sql-server-linux-replication.md)
|Microsoft 分散トランザクション コーディネーター (MSDTC) のサポート |[Linux で MSDTC を構成する方法](sql-server-linux-configure-msdtc.md) |
|サード パーティの AD プロバイダーに対する OpenLDAP のサポート |[チュートリアル:SQL Server on Linux で Active Directory 認証を使用する](sql-server-linux-active-directory-authentication.md) |
|Linux 上の Machine Learning |[Linux に Machine Learning を構成する](sql-server-linux-setup-machine-learning.md) |
|`tempdb` の強化機能 | 既定では、Linux 上に SQL Server を新しくインストールすると、論理コアの数に基づいて複数の `tempdb` データ ファイルが作成されます (最大で 8 個のデータ ファイル)。 これは、マイナー バージョンまたはメジャー バージョンのインプレース アップグレードには適用されません。 各 `tempdb` ファイルは 8 MB で、64 MB まで自動拡張されます。 この動作は、Windows への SQL Server の既定のインストールに似ています。 |
| Linux での PolyBase | 非 Hadoop コネクタ向けに Linux に [PolyBase をインストール](../relational-databases/polybase/polybase-linux-setup.md)します。<br/><br/>[PolyBase 型のマッピング](../relational-databases/polybase/polybase-type-mapping.md) |
| 変更データ キャプチャ (CDC) のサポート | SQL Server 2019 では、変更データ キャプチャ (CDC) が Linux でサポートされるようになりました。 |
| Microsoft Container Registry | [Microsoft Container Registry](https://azure.microsoft.com/blog/microsoft-syndicates-container-catalog/) では、[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] など、Microsoft の新しい公式コンテナー イメージのために Docker Hub が取り替えられます。 |
| ルート以外のコンテナー | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] では、既定でルート以外のユーザーとして [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] を起動することで、より安全なコンテナーを作成できるようになりました。 詳細については、「[非ルート ユーザーとして SQL Server コンテナーを作成して実行する](./sql-server-linux-docker-container-security.md#buildnonrootcontainer)」を参照してください。 |

## <a name="next-steps"></a>次のステップ

SQL Server on Linux をインストールするには、次のチュートリアルのいずれかを使用します。

- [Red Hat Enterprise Linux へのインストール](quickstart-install-connect-red-hat.md?view=sql-server-linux-ver15)
- [SUSE Linux Enterprise Server へのインストール](quickstart-install-connect-suse.md?view=sql-server-linux-ver15)
- [Ubuntu へのインストール](quickstart-install-connect-ubuntu.md?view=sql-server-linux-ver15)
- [Docker 上での実行](quickstart-install-connect-docker.md?view=sql-server-linux-ver15)
- [Azure での SQL VM プロビジョニング](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

よく寄せられる質問に対する回答については、「[SQL Server on Linux に関する FAQ](sql-server-linux-faq.md)」を参照してください。 SQL Server 2019 で導入されたその他の改善点については、[SQL Server 2019 の新機能](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15)に関する記事をご覧ください。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]