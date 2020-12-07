---
title: Windows の分離の変更
description: この記事では、Windows 上の SQL Server 2019 の Machine Learning Services での分離メカニズムに対する変更について説明します。 これらの変更は、SQLRUserGroup、ファイアウォール規則、ファイルのアクセス許可、および暗黙の認証に影響します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/05/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4a4f32c73d1fdf0cd47caaa031321eaa0ef52092
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956743"
---
# <a name="sql-server-2019-on-windows-isolation-changes-for-machine-learning-services"></a>Windows 上の SQL Server 2019:Machine Learning Services の分離の変更
[!INCLUDE [SQL Server 2019 - Windows only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

この記事では、Windows 上の SQL Server 2019 の Machine Learning Services での分離メカニズムに対する変更について説明します。 これらの変更は、**SQLRUserGroup**、ファイアウォール規則、ファイルのアクセス許可、および暗黙の認証に影響します。

詳細については、「[Windows に SQL Server Machine Learning Services をインストールする方法](sql-machine-learning-services-windows-install.md)」を参照してください。

## <a name="changes-to-isolation-mechanism"></a>分離メカニズムの変更

Windows では、SQL Server 2019 セットアップにより、外部プロセスの分離メカニズムが変更されます。 この変更により、ローカル ワーカー アカウントが、Windows で実行されているクライアント アプリケーションの分離テクノロジである [AppContainers](/windows/desktop/secauthz/appcontainer-isolation) に置き換えられます。 

変更の結果に対して、管理者が特別に行うアクション項目はありません。 新規またはアップグレードされたサーバーでは、[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) から実行されるすべての外部スクリプトおよびコードは、自動的に新しい分離モデルに従います。 

要約すると、このリリースの主な違いは次のとおりです。

+ **SQL 制限ユーザー グループ (SQLRUserGroup)** のローカル ユーザー アカウントは、外部プロセスを実行するために作成または使用されなくなりました。 それらは AppContainers によって置き換えられます。
+ **SQLRUserGroup** メンバーシップが変更されました。 メンバーシップは、複数のローカル ユーザー アカウントの代わりに、SQL Server Launchpad サービス アカウントだけで構成されます。 R と Python のプロセスは、AppContainers を通じて分離された Launchpad サービス ID で実行されるようになりました。

分離モデルは変更されていますが、SQL Server 2019 ではインストール ウィザードとコマンドライン パラメーターは同じままです。 インストールの詳細については、「[SQL Server Machine Learning Services をインストールする](sql-machine-learning-services-windows-install.md)」を参照してください。

## <a name="about-appcontainer-isolation"></a>AppContainer の分離について

以前のリリースでは、**SQLRUserGroup** には、外部プロセスの分離と実行に使用されるローカル Windows ユーザー アカウント (MSSQLSERVER00-MSSQLSERVER20) のプールが含まれていました。 外部プロセスが必要な場合、SQL Server Launchpad サービスは使用可能なアカウントを取得し、それを使用してプロセスを実行します。 

SQL Server 2019 では、セットアップでローカル ワーカー アカウントが作成されなくなりました。 代わりに、[AppContainer](/windows/desktop/secauthz/appcontainer-isolation) によって分離が実現されます。 実行時に、ストアド プロシージャまたはクエリで埋め込みスクリプトやコードが検出されると、SQL Server は拡張機能固有の起動ツールの要求を使用して Launchpad を呼び出します。 Launchpad は、自身の ID の下のプロセスで適切なランタイム環境を呼び出し、AppContainer をインスタンス化して、それを含めます。 ローカル アカウントとパスワードの管理が不要になったため、これは有益な変更です。 また、ローカル ユーザー アカウントが禁止されているインストールでは、ローカル ユーザー アカウントの依存関係を削除することで、この機能を使用できるようになります。

AppContainer は、SQL Server に実装されているため、内部メカニズムです。 プロセス モニターには AppContainer の物理的な証拠は表示されませんが、セットアップによって作成された、プロセスによるネットワーク呼び出しを防ぐための送信ファイアウォール規則で AppContainer を見つけることができます。

## <a name="firewall-rules-created-by-setup"></a>セットアップによって作成されたファイアウォール規則

既定では、SQL Server はファイアウォール規則を作成することにより、送信接続を無効にします。 以前は、これらの規則はローカル ユーザー アカウントに基づいており、そこではセットアップが **SQLRUserGroup** のためにアウトバウンド規則を作成し、メンバーへのネットワーク アクセスを拒否していました (各ワーカー アカウントは、規則に従いローカル原則として一覧表示されていました)。 

AppContainers への移行の一環として、AppContainer SID に基づく新しいファイアウォール規則があります。これは、SQL Server セットアップで作成された 20 の AppContainers のそれぞれに 1 つずつあります。 ファイアウォール規則名の名前付け規則は、**Block network access for AppContainer-00 in SQL Server instance MSSQLSERVER** です。ここで、00 は AppContainer の番号 (既定では 00-20) で、MSSQLSERVER は SQL Server インスタンスの名前です。 

> [!Note]
> ネットワーク呼び出しが必要な場合は、Windows ファイアウォールでアウトバウンド規則を無効にすることができます。

<a name="file-permissions"></a>

## <a name="file-permissions"></a>ファイルのアクセス許可

既定では、外部の Python および R スクリプトには、作業ディレクトリに対する読み取りアクセス許可のみが与えられます。 

ご利用の Python または R スクリプトで他の任意のディレクトリへのアクセス権が必要な場合は、**NT Service\MSSQLLaunchpad** サービス ユーザー アカウントおよびこのディレクトリ上の **ALL APPLICATION PACKAGES** に**読み取りおよび実行**アクセス許可または**書き込み**アクセス許可を付与する必要があります。

アクセス権を付与するには、次の手順に従います。

1. ファイル エクスプローラーで、作業ディレクトリとして使用するフォルダーを右クリックし、 **[プロパティ]** を選択します。
1. **[セキュリティ]** を選択し、 **[編集]** をクリックしてアクセス許可を変更します。
1. **[追加]** をクリックします。
1. **[場所の指定]** がローカル コンピューター名であることを確認してください。
1. **[選択するオブジェクト名を入力してください]** に 「**ALL APPLICATION PACKAGES**」と入力し、 **[名前の確認]** をクリックします。 **[OK]** をクリックします。
1. **[許可]** 列の下にある **[読み取りおよび実行]** を選択します。
1. 書き込みアクセス許可を付与する場合は、 **[許可]** 列の下にある **[書き込み]** を選択します。
1. **[OK]** をクリックし、さらに **[OK]** をクリックします。

### <a name="program-file-permissions"></a>プログラム ファイルのアクセス許可

以前のリリースと同様に、**SQLRUserGroup** は、SQL Server **Binn**、**R_SERVICES**、および **PYTHON_SERVICES** ディレクトリの実行可能ファイルに対する読み取りと実行のアクセス許可を、引き続き提供します。 このリリースでは、**SQLRUserGroup** の唯一のメンバーは SQL Server Launchpad サービス アカウントです。  Launchpad サービスが R または Python の実行環境を開始すると、プロセスは LaunchPad サービスとして実行されます。

## <a name="implied-authentication"></a>暗黙の認証

以前と同様に、スクリプトまたはコードが、信頼されている認証を使用してデータまたはリソースを取得するために SQL Server に接続する必要がある場合、*暗黙の認証*には追加の構成が必要です。 追加の構成では、複数のワーカー アカウントではなく、単一の SQL Server Launchpad サービス アカウントが唯一のメンバーである **SQLRUserGroup** のためのデータベース ログインを作成する必要があります。 このタスクの詳細については、「[データベース ユーザーとして SQLRUserGroup を追加する](../security/create-a-login-for-sqlrusergroup.md)」を参照してください。


## <a name="symbolic-link-created-by-setup"></a>セットアップによって作成されたシンボリック リンク

SQL Server セットアップの一環として、現在の既定の **R_SERVICES** および **PYTHON_SERVICES** にシンボリックリンクが作成されています。 このリンクを作成しない場合、代替案としては「すべてのアプリケーション パッケージ」の読み取りアクセス許可を、そのフォルダーまでの階層に付与することがあります。


## <a name="see-also"></a>関連項目

+ [Windows に SQL Server Machine Learning Services をインストールする](sql-machine-learning-services-windows-install.md)
+ [Linux に SQL Server Machine Learning Services をインストールする](../../linux/sql-server-linux-setup-machine-learning.md)