---
title: adutil を使用して SQL Server on Linux ベースのコンテナーで Active Directory 認証を構成する
description: adutil を使用して SQL Server on Linux コンテナーで Active Directory 認証を構成する方法を順を追って説明します
author: amvin87
ms.author: amitkh
ms.reviewer: vanto
ms.date: 12/10/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: c82362cf9a3d73d1bd9a7c714957e222ad15af18
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101837633"
---
# <a name="tutorial-configure-active-directory-authentication-with-sql-server-on-linux--containers"></a>チュートリアル:SQL Server on Linux コンテナーで Active Directory 認証を構成する

> [!NOTE]
> **adutil** は現在、**パブリック プレビュー** 段階にあります

このチュートリアルでは、Active Directory (AD) 認証 (統合認証とも呼ばれます) をサポートするように SQL Server on Linux コンテナーを構成する方法について説明します。 概要については、「[SQL Server on Linux に対する Active Directory 認証](sql-server-linux-active-directory-auth-overview.md)」をご覧ください。

このチュートリアルは、次のタスクで構成されています。

> [!div class="checklist"]
> - adutil-preview をインストールする
> - Linux ホストを AD ドメインに参加させる
> - SQL Server 用の AD ユーザーを作成し、adutil ツールを使用して ServicePrincipalName (SPN) を設定する
> - SQL Server サービスの keytab ファイルを作成する
> - SQL Server コンテナーによって使用される mssql.conf および krb5.conf ファイルを作成する
> - 構成ファイルをマウントし、SQL Server コンテナーをデプロイする
> - Transact-SQL を使用して AD ベースの SQL Server ログインを作成する
> - AD 認証を使用して SQL Server に接続する

## <a name="prerequisites"></a>前提条件

AD 認証を構成する前に、次のものが必要です。

- ネットワークに AD ドメイン コントローラー (Windows) を用意します。
- ドメインに参加させる Linux ホスト マシンに adutil-preview ツールをインストールします。 実行している Linux ディストリビューションに基づき、後の「[adutil-preview をインストールする](#install-adutil-preview)」セクションに従って、adutil-preview ツールをインストールします。

## <a name="container-deployment-and-preparation"></a>コンテナーのデプロイと準備

コンテナーを設定するには、ホスト上のコンテナーによって使用されるポートを事前に知っておく必要があります。 お使いのコンテナー ホストでは、既定のポート 1433 のマップが異なっている場合があります。 このチュートリアルでは、ホスト上のポート 5433 をコンテナーのポート 1433 にマップします。 詳細については、「[クイックスタート: Docker を使用して SQL Server コンテナー イメージを実行する](quickstart-install-connect-docker.md)」を参照してください

サービス プリンシパル名 (SPN) を登録するときは、マシンのホスト名またはコンテナーの名前を使用できますが、コンテナーに外部から接続したときに表示されるようにしたいものに従って設定する必要があります。

Linux ホストの IP アドレスに対する転送ホスト (A) エントリが、Active Directory に追加されていることを確認します。これは、SQL Server コンテナーの名前へのマッピングです。 このチュートリアルでは、`myubuntu` ホスト マシンの IP アドレスは `10.0.0.10` であり、SQL Server コンテナーの名前は `sql1` です。 次に示すように、Active Directory に転送ホスト エントリを追加します。 このエントリにより、ユーザーが sql1.contoso.com に接続すると、適切なホストに到達することが保証されます。

:::image type="content" source="media/sql-server-linux-containers-ad-auth-adutil-tutorial/host-a-record.png" alt-text="ホスト レコードを追加する":::

このチュートリアルでは、3 つの VM がある Azure の環境を使用しています。 1 つの VM は Windows ドメイン コントローラー (DC) として機能し、ドメイン名は `contoso.com` です。 ドメイン コントローラーの名前は `adVM.contoso.com` です。 2 つ目のマシンは `winbox` という名前の Windows マシンで、Windows 10 デスクトップがを実行されており、クライアント ボックスとして使用され、SQL Server Management Studio (SSMS) がインストールされています。 3 つ目のマシンは、`myubuntu` という名前の Ubuntu 18.04 LTS マシンで、SQL Server コンテナーがホストされています。 すべてのマシンが `contoso.com` ドメインに参加しています。 詳細については、「[Linux ホスト上の SQL Server を Active Directory ドメインに参加させる](sql-server-linux-active-directory-join-domain.md)」を参照してください。

> [!NOTE]
> この記事で後ほど説明するように、ホスト コンテナー マシンをドメインに参加させることは必須ではありません。

## <a name="install-adutil-preview"></a>adutil-preview をインストールする

Linux ホスト マシンで、次のコマンドを使用し、Linux のディストリビューションに基づいて adutil-preview をインストールします。

> [!NOTE]
> このプレビュー バージョンの場合、特定の Linux ディストリビューションでは、`ACCEPT_EULA` パラメーターを指定せずに adutil をインストールしようとすると、インストール エクスペリエンスが妨げられることがわかっています。 以下では、`ACCEPT_EULA=Y` を設定して adutil-preview ツールをインストールすることをお勧めします。 インストールの前に、プレビューの [EULA](https://go.microsoft.com/fwlink/?linkid=2151376) を読むことができます。 Microsoft ではこれに関する作業に積極的に取り組んでおり、GA リリースでは修正されるはずです。

### <a name="rhel"></a>RHEL

1. Microsoft Red Hat リポジトリ構成ファイルをダウンロードします。

    ```bash
    sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/8/prod.repo
    ```

1. 以前のバージョンの adutil がインストールされている場合は、古い adutil パッケージを削除します。

    ```bash
    sudo yum remove adutil
    ```

1. 次のコマンドを実行して adutil-preview をインストールします。 `ACCEPT_EULA=Y` により、adutil のプレビュー EULA が受け入れられます。 EULA はパス `/usr/share/adutil/` に格納されます。

    ```bash
    sudo ACCEPT_EULA=Y yum install -y adutil-preview
    ```

### <a name="ubuntu"></a>Ubuntu

1. パブリック リポジトリの GPG キーをインポートしてから、Microsoft Ubuntu リポジトリを登録します。

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    sudo curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
    ```

1. 以前のバージョンの adutil がインストールされている場合は、次のコマンドを使用して、古い adutil パッケージを削除します

    ```bash
    sudo apt-get remove adutil
    ```

1. 次のコマンドを実行して adutil-preview をインストールします。 `ACCEPT_EULA=Y` により、adutil のプレビュー EULA が受け入れられます。 EULA はパス `/usr/share/adutil/` に格納されます。

    ```bash
    sudo apt-get update
    sudo ACCEPT_EULA=Y apt-get install -y adutil-preview
    ```

### <a name="sles"></a>SLES

1. Zypper に Microsoft SQL Server リポジトリを追加します。

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo
    ```

1. 以前のバージョンの adutil がインストールされている場合は、古い adutil パッケージを削除します。

    ```bash
    sudo zypper remove adutil
    ```

1. 次のコマンドを実行して adutil-preview をインストールします。 `ACCEPT_EULA=Y` により、adutil のプレビュー EULA が受け入れられます。 EULA はパス `/usr/share/adutil/` に格納されます。

    ```bash
    sudo ACCEPT_EULA=Y zypper install -y adutil-preview
    ```

## <a name="creating-the-ad-user-spns-and-sql-server-service-keytab"></a>AD ユーザー、SPN、SQL Server サービスの keytab の作成

SQL Server on Linux コンテナー ホストをドメインの一部にするのが望ましくなく、マシンをドメインに参加させる手順に従っていない場合は、既に AD ドメインの一部になっている別の Linux マシンで、次の手順のようにします。

 1. SQL Server 用の AD ユーザーを作成し、adutil ツールを使用して SPN を設定します。

 2. SQL Server サービスの keytab ファイルを作成して構成します。

作成された mssql.keytab ファイルを SQL Server コンテナーを実行するホスト マシンにコピーし、コピーした mssql.keytab を使用するようにコンテナーを構成します。 必要に応じて、SQL Server コンテナーを実行する Linux ホストを AD ドメインに参加させ、同じマシンで次の手順のようにすることもできます。

### <a name="create-an-ad-user-for-sql-server-and-set-the-serviceprincipalname-using-the-adutil-tool"></a>SQL Server 用の AD ユーザーを作成し、adutil ツールを使用して ServicePrincipalName を設定する

SQL Server on Linux コンテナーで AD 認証を有効にするには、以下で説明するステップ 1 から 3 を、AD ドメインの一部である Linux マシンで実行する必要があります。

1. `kinit` コマンドを使用して、Kerberos TGT (Ticket Granting Ticket) を取得または更新します。 `kinit` コマンドには特権アカウントを使用します。 このアカウントには、ドメインに接続するためのアクセス許可が必要であり、ドメインにアカウントと SPN を作成できる必要もあります。

    > [!IMPORTANT]
    > このコマンドを実行する前に、前のステップで示したように、ホストが既にドメインに属している必要があります。

    ```bash
    kinit privilegeduser@DOMAIN.COM
    ```

    例:上で説明した環境の場合、特権アカウントは `amvin@CONTOSO.COM` です

    ```bash
    kinit amvin@CONTOSO.COM
    ```

2. adutil ツールを使用して、SQL Server によって特権 AD アカウントとして使用される新しいユーザーを作成します。

   ```bash
   adutil user create --name sqluser --distname CN=sqluser,CN=Users,DC=CONTOSO,DC=COM --password 'P@ssw0rd'
   ```

    > [!NOTE]
    > パスワードは、次の 3 つの方法のいずれでも指定できます。
    >
    > - パスワード フラグ: --password \<password\>
    > - 環境変数 - `ADUTIL_ACCOUNT_PWD`
    > - 対話形式での入力
    >
    > パスワードの入力方法の優先順位は、上記のオプションの順序に従います。 推奨されるオプションは、環境変数または対話形式の入力を使用してパスワードを指定することです。これらの方がパスワード フラグより安全です。

    上で示したように、識別名 (`-distname`) を使用してアカウントの名前を指定することも、組織単位 (OU) 名を使用することもできます。 両方を指定した場合は、OU 名 (`--ou`) が識別名より優先されます。 次のコマンドを実行して詳細を確認できます。

    ```bash
    adutil user create --help
    ```

3. 上で作成したユーザーに SPN を登録します。 接続を外部に表示する方法に応じて、必要な場合は、コンテナー名の代わりにホスト マシン名を使用できます。 このチュートリアルでは、1433 の代わりにポート 5433 を使用します。 これは、コンテナーのポート マッピングです。 ポート番号は異なる場合があります。

    ```bash
    adutil spn addauto -n sqluser -s MSSQLSvc -H sql1.contoso.com -p 5433
    ```

    > [!NOTE]
    >
    > - kinit アカウントに十分な特権がある場合、`addauto` により SPN が自動的に作成されます。
    > - `-n`:SPN が割り当てられるアカウントの名前。
    > - `-s`:SPN の生成に使用するサービス名。 この場合は、SQL Server サービス用であるため、サービス名は MSSQLSvc です。
    > - `-H`:SPN の生成に使用するホスト名。 指定しないと、ローカル ホストの FQDN が使用されます。 コンテナー名の FQDN も指定してください。 この場合、コンテナー名は `sql1` であり、FQDN は `sql1.contoso.com` です。
    > - `-p`:SPN の生成に使用するポート。 指定しないと、SPN はポートなしで生成されます。 この場合、SQL Server が既定のポート 1433 をリッスンしている場合にのみ、SQL 接続は機能します。

### <a name="create-the-sql-server-service-keytab-file"></a>SQL Server サービスの keytab ファイルを作成する

前に作成した 4 つの各 SPN に対するエントリと、ユーザー用の 1 つが含まれる、keytab ファイルを作成します。 keytab ファイルはコンテナーにマウントされるので、ホスト上の任意の場所に作成できます。 docker や podman を使用してコンテナーをデプロイするときに、結果の keytab が正しくマウントされている限り、このパスを変更しても安全です。

すべての SPN に対して keytab を作成するには、`createauto` オプションを使用します。

```bash
adutil keytab createauto -k /container/sql1/secrets/mssql.keytab -p 5433 -H sql1.contoso.com --password 'P@ssw0rd' -s MSSQLSvc
```

> [!NOTE]
>
> - `-k`:`mssql.keytab` ファイルの作成先となるパス。 上の例では、ディレクトリ "/container/sql1/secrets" が既にホスト上に存在している必要があります。
> - `-p`:SPN の生成に使用するポート。 指定しないと、SPN はポートなしで生成されます。
> - `-H`:SPN の生成に使用するホスト名。 指定しないと、ローカル ホストの FQDN が使用されます。 コンテナー名の FQDN も指定してください。 この場合、コンテナー名は `sql1` であり、FQDN は `sql1.contoso.com` です。
> - `-s`:SPN の生成に使用するサービス名。 この場合は、SQL Server サービス用であるため、サービス名は MSSQLSvc です。
> - `--password`:これは、前に作成した特権 AD ユーザー アカウントのパスワードです。
> - `-e` または `--enctype`: keytab エントリの暗号化の種類。 コンマで区切られた値のリストを使用します。 指定しないと、対話形式のプロンプトが表示されます。

暗号化の種類を選択する場合は、複数選択できます。 この例では、`aes256-cts-hmac-sha1-96` と `arcfour-hmac` を選択しています。 ホストとドメインで確実にサポートされている暗号化の種類を選択してください。

暗号化の種類を非対話形式で選択する場合は、上のコマンドの -e 引数を使用して暗号化の種類の選択を指定できます。 adutil コマンドの詳細については、次のコマンドを実行してください。

```bash
adutil keytab createauto --help
```

> [!NOTE]
> `arcfour-hmac` は弱い暗号化であり、運用環境での暗号化の種類として使用することは推奨されません。

ユーザーの keytab を作成するには、次のコマンドを使用します。

```bash
adutil keytab create -k /container/sql1/secrets/mssql.keytab -p sqluser --password 'P@ssw0rd!'
```

> [!NOTE]
>
> - `-k`:`mssql.keytab` ファイルの作成先となるパス。 上の例では、ディレクトリ "/container/sql1/secrets" が既にホスト上に存在している必要があります。
> - `-p`:keytab に追加するプリンシパル。

adutil による keytab の作成と自動作成では、以前のファイルは上書きされません。既に存在する場合は、ファイルに追加されるだけです。

コンテナーをデプロイするとき、作成された keytab に適切なアクセス許可が確実に設定されているようにします。

```bash
chmod 440 /container/sql1/secrets/mssql.keytab
```

> [!NOTE]
> この時点で、現在の Linux ホストから SQL Server コンテナーをデプロイする Linux ホストに mssql.keytab をコピーし、SQL Server コンテナーを実行する Linux ホストで残りの手順を行います。 SQL コンテナーをデプロイするのと同じ Linux ホストで上記の手順を行った場合は、同じホストで次の手順を行います。

## <a name="create-the-config-files-to-be-used-by-the-sql-server-container"></a>SQL Server コンテナーによって使用される構成ファイルを作成する

1. AD の設定を使用して `mssql.conf` ファイルを作成します。 このファイルはホスト上の任意の場所に作成でき、docker run コマンドの間に正しくマウントする必要があります。 この例では、このファイル `mssql.conf` を `/container/sql1 `の下に格納します。これはコンテナー ディレクトリです。 `mssql.conf` の内容は次のようになります。

    ```output
    [network]
    privilegedadaccount = sqluser
    kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
    ```

    > [!NOTE]
    >
    > - `privilagedadaccount`:AD 認証に使用する特権 AD ユーザー。
    > - `kerberoskeytabfile`:mssql.keytab ファイルが格納されるコンテナー内のパス。

1. krb5.conf ファイルを作成します。 サンプルを次に示します。 これらのファイルでは大文字と小文字が区別されます。

    ```output
    [libdefaults]
    default_realm = DOMAIN.COM

    [realms]
     CONTOSO.COM = {
         kdc = adVM.contoso.com
         admin_server = adVM.contoso.com
         default_domain = CONTOSO.COM
     }

    [domain_realm]
     .contoso.com = CONTOSO.COM
     contoso.com = CONTOSO.COM


1. Copy all files, `mssql.conf`, `krb5.conf`, `mssql.keytab` to a location that will be mounted to the SQL Server container. In this example, these files are placed on the host at the following locations: `mssql.conf` and `krb5.conf` at `/container/sql1/`. `mssql.keytab` is placed at the location `/container/sql1/secrets/`.

1. Make sure there's enough permission on these folders for the user running the docker/podman command. When the container starts, the user needs access to the folder path created. In this example, we provided the below permissions given to the folder path:

    ```bash
    sudo chmod 755 /container/sql1/
    ```

## <a name="mount-the-config-files-and-deploy-the-sql-server-container"></a>構成ファイルをマウントし、SQL Server コンテナーをデプロイする

SQL Server コンテナーを実行し、次に示すように、前に作成した正しい AD 構成ファイルをマウントします。

```bash
sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=\<YourStrong@Passw0rd\>" \
-p 5433:1433 --name sql1 \
-v /container/sql1:/var/opt/mssql \
-v /container/sql1/krb5.conf:/etc/krb5.conf \
-d mcr.microsoft.com/mssql/server:2019-latest
```

> [!NOTE]
> SELinux が有効なホストのような LSM (Linux セキュリティ モジュール) でコンテナーを実行する場合は、`Z` オプションを使用してボリュームをマウントする必要があります。これは、プライベートな非共有ラベルでコンテンツにラベルを付けるよう docker に指示するものです。 詳細については、[SE Linux ラベルの構成](https://docs.docker.com/storage/bind-mounts/#configure-the-selinux-label)に関するページを参照してください。

この例には、次のコマンドが含まれています。

```bash
sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=P@ssw0rd" -p 5433:1433 --name sql1 \
-v /container/sql1:/var/opt/mssql/ \
-v /container/sql1/krb5.conf:/etc/krb5.conf \
--dns-search contoso.com \
--dns 10.0.0.4 \
--add-host adVM.contoso.com:10.0.0.4 \
--add-host contoso.com:10.0.0.4 \
--add-host contoso:10.0.0.4 \
-d mcr.microsoft.com/mssql/server:2019-latest
```

> [!NOTE]
>
> - ファイル `mssql.conf` と `krb5.conf` は、ホスト ファイルのパス `/container/sql1` にあります。
> - 作成された `mssql.keytab` は、ホスト ファイルのパス `/container/sql1/secrets` にあります。
> - ホスト マシンは Azure 上にあるため、AD の詳細を同じ順序で docker run コマンドに追加する必要があります。 この例では、ドメイン コントローラー `adVM` はドメイン `contoso.com` 内にあり、IP アドレスは `10.0.0.4` です。 ドメイン コントローラーにより DNS と KDC が実行されます。

## <a name="create-ad-based-sql-server-logins-in-transact-sql"></a>Transact-SQL で AD ベースの SQL Server ログインを作成する

SQL コンテナーに接続し、次のコマンドを実行して、ログインを作成し、一覧に表示されることを確認します。 このコマンドは、SSMS、Azure Data Studio (ADS)、またはその他のコマンド ライン インターフェイス (CLI) ツールを実行しているクライアント コンピューター (Windows または Linux) から実行できます。

```sql
create login [contoso\amvin] From Windows
SELECT name FROM sys.server_principals;
```

## <a name="connect-to-sql-server-using-ad-authentication"></a>AD 認証を使用して SQL Server に接続する。

[SSMS](../ssms/download-sql-server-management-studio-ssms.md) または [ADS](../azure-data-studio/download-azure-data-studio.md) を使用して接続するには、SQL Server の名前とポート番号 (名前はコンテナー名またはホスト名) を使用し、Windows 資格情報を使用して、SQL Server にログインします。 この例では、サーバー名は `sql1.contoso.com, 5433` です。

また、[sqlcmd](../tools/sqlcmd-utility.md) などのツールを使用して、コンテナー内の SQL Server に接続することもできます。

```bash
sqlcmd -E -S 'sql1.contoso.com, 5433'
```

## <a name="next-steps"></a>次の手順

- [クイックスタート:Docker を使用して SQL Server コンテナー イメージを実行する](quickstart-install-connect-docker.md)
- [Linux ホスト上の SQL Server を Active Directory ドメインに参加させる](sql-server-linux-active-directory-auth-overview.md)
