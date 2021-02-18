---
title: adutil を使用して SQL Server on Linux で Active Directory 認証を構成する
description: adutil を使用して SQL Server on Linux で Active Directory 認証を構成する方法を順を追って説明します
author: amvin87
ms.author: amitkh
ms.reviewer: vanto
ms.date: 12/10/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: e1e14db6e55ca4af4f76220c0e3f377c38e41165
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100351873"
---
# <a name="tutorial-configure-active-directory-authentication-with-sql-server-on-linux-using-adutil"></a>チュートリアル:adutil を使用して SQL Server on Linux で Active Directory 認証を構成する

> [!NOTE]
> **adutil** は現在、**パブリック プレビュー** 段階にあります

このチュートリアルでは、adutil を使用して SQL Server on Linux 用に Active Directory 認証を構成する方法について説明します。 ktpass を使用して AD 認証を構成する別の方法については、「[チュートリアル: SQL Server on Linux で Active Directory 認証を使用する](sql-server-linux-active-directory-authentication.md)」を参照してください。

このチュートリアルは、次のタスクで構成されています。

> [!div class="checklist"]
> - adutil-preview をインストールする
> - AD ドメインに Linux マシンを参加させる
> - SQL Server 用の AD ユーザーを作成し、adutil ツールを使用して ServicePrincipalName (SPN) を設定する
> - SQL Server サービスの keytab ファイルを作成する
> - keytab ファイルを使用するように SQL Server を構成する
> - Transact-SQL を使用して AD ベースの SQL Server ログインを作成する
> - AD 認証を使用して SQL Server に接続する

## <a name="prerequisites"></a>前提条件

AD 認証を構成する前に、次のものが必要です。

- ネットワークに AD ドメイン コントローラー (Windows) を用意します。
- Linux ホスト マシンに adutil-preview ツールをインストールします。 実行している Linux ディストリビューションに基づき、以下のセクションに従って、adutil-preview をインストールします。

## <a name="install-adutil-preview"></a>adutil-preview をインストールする

Linux ホスト マシンで、次のコマンドを使用して adutil-preview をインストールします。

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

1. 次のコマンドを実行して adutil-preview をインストールします。 `ACCEPT_EULA=Y` により、adutil のプレビュー EULA が受け入れられます。 EULA はパス "/usr/share/adutil/" に格納されます。

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

1. 次のコマンドを実行して adutil-preview をインストールします。 `ACCEPT_EULA=Y` により、adutil のプレビュー EULA が受け入れられます。 EULA はパス "/usr/share/adutil/" に格納されます。

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

1. 次のコマンドを実行して adutil-preview をインストールします。 `ACCEPT_EULA=Y` により、adutil のプレビュー EULA が受け入れられます。 EULA はパス "/usr/share/adutil/" に格納されます。

    ```bash
    sudo ACCEPT_EULA=Y zypper install -y adutil-preview
    ```

## <a name="domain-machine-preparation"></a>ドメイン マシンの準備

Linux ホストの IP アドレスに対する転送ホスト (A) エントリが、Active Directory に追加されていることを確認します。 このチュートリアルでは、`myubuntu` ホスト マシンの IP アドレスは `10.0.0.10` です。 次に示すように、Active Directory に転送ホスト エントリを追加します。 このエントリにより、ユーザーが myubuntu.contoso.com に接続すると、適切なホストに到達することが保証されます。

:::image type="content" source="media/sql-server-linux-ad-auth-adutil-tutorial/host-a-record.png" alt-text="ホスト レコードを追加する":::

このチュートリアルでは、3 つの VM がある Azure の環境を使用しています。 1 つの VM は Windows ドメイン コントローラー (DC) として機能し、ドメイン名は `contoso.com` です。 ドメイン コントローラーの名前は `adVM.contoso.com` です。 2 つ目のマシンは `winbox` という名前の Windows マシンで、Windows 10 デスクトップがを実行されており、クライアント ボックスとして使用され、SQL Server Management Studio (SSMS) がインストールされています。 3 つ目のマシンは、`myubuntu` という名前の Ubuntu 18.04 LTS マシンで、SQL Server がホストされています。

## <a name="join-the-linux-host-machine-to-your-ad-domain"></a>Linux ホスト マシンを AD ドメインに参加させる

SQL Server Linux ホストを Active Directory ドメイン コントローラーに参加させます。 Active Directory ドメインに参加する方法については、「[Linux ホスト上の SQL Server を Active Directory ドメインに参加させる](sql-server-linux-active-directory-join-domain.md)」をご覧ください。

## <a name="create-an-ad-user-for-sql-server-and-set-the-serviceprincipalname-spn-using-the-adutil-tool"></a>SQL Server 用の AD ユーザーを作成し、adutil ツールを使用して ServicePrincipalName (SPN) を設定する

1. `kinit` コマンドを使用して、Kerberos TGT (Ticket Granting Ticket) を取得または更新します。 `kinit` コマンドには特権アカウントを使用します。 このアカウントには、ドメインに接続するためのアクセス許可が必要であり、ドメインにアカウントと SPN を作成できる必要もあります。

    > [!IMPORTANT]
    > このコマンドを実行する前に、前のステップで示したように、ホスト マシンが既にドメインに属している必要があります。

    ```bash
    kinit privilegeduser@DOMAIN.COM
    ```

    例:上で説明した環境の場合、特権アカウントは `amvin@CONTOSO.COM` です

    ```bash
    kinit amvin@CONTOSO.COM
    ```

2. adutil ツールを使用して、SQL Server によって特権 AD アカウントとして使用される新しいユーザーを作成します。

   ```bash
   adutil user create --name sqluser -distname CN=sqluser,CN=Users,DC=CONTOSO,DC=COM --password 'P@ssw0rd'
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

3. 上で作成したプリンシパルに SPN を登録します。 マシンの FQDN を使用します。 このチュートリアルでは、SQL Server の既定のポート 1433 を使用しています。 ポート番号は異なる場合があります。

    ```bash
    adutil spn addauto -n sqluser -s MSSQLSvc -H myubuntu.contoso.com -p 1433
    ```

    > [!NOTE]
    >
    > - kinit アカウントに十分な特権がある場合、`addauto` により SPN が自動的に作成されます。
    > - `-n`:SPN が割り当てられるアカウントの名前。
    > - `-s`:SPN の生成に使用するサービス名。 この場合は、SQL Server サービス用であるため、サービス名は `MSSQLSvc` です。
    > - `-H`:SPN の生成に使用するホスト名。 指定しないと、ローカル ホストの FQDN が使用されます。 この場合、ホスト名は `myubuntu` であり、FQDN は `myubuntu.contoso.com` です。
    > - `-p`:SPN の生成に使用するポート。 指定しないと、SPN はポートなしで生成されます。 この場合、SQL Server が既定のポート 1433 をリッスンしている場合にのみ、SQL 接続は機能します。

## <a name="create-the-sql-server-service-keytab-file"></a>SQL Server サービスの keytab ファイルを作成する

前に作成した 4 つの各 SPN に対するエントリと、ユーザー用の 1 つが含まれる、keytab ファイルを作成します。

```bash
adutil keytab createauto -k /var/opt/mssql/secrets/mssql.keytab -p 1433 -H myubuntu.contoso.com --password 'P@ssw0rd' -s MSSQLSvc 
```

> [!NOTE]
>
> - `-k`:`mssql.keytab` ファイルの作成先となるパス。 上の例では、ディレクトリ `/var/opt/mssql/secrets/` が既にホスト上に存在している必要があります。
> - `-p`:SPN の生成に使用するポート。 指定しないと、SPN はポートなしで生成されます。
> - `-H`:SPN の生成に使用するホスト名。 指定しないと、ローカル ホストの FQDN が使用されます。 この場合、ホスト名は `myubuntu` であり、FQDN は `myubuntu.contoso.com` です。
> - `-s`:SPN の生成に使用するサービス名。 この場合は、SQL Server サービス用であるため、サービス名は `MSSQLSvc` です。
> - `--password`:これは、前に作成した特権 AD ユーザー アカウントのパスワードです。
> - `-e` または `--enctype`: keytab エントリの暗号化の種類。 コンマで区切られた値のリストを使用します。 指定しないと、対話形式のプロンプトが表示されます。

暗号化の種類を選択する場合は、複数選択できます。 この例では、`aes256-cts-hmac-sha1-96` と `arcfour-hmac` を選択しています。 ホストとドメインで確実にサポートされている暗号化の種類を選択してください。

暗号化の種類を非対話形式で選択する場合は、上のコマンドの -e 引数を使用して暗号化の種類の選択を指定できます。 adutil コマンドの詳細については、次のコマンドを実行してください。

```bash
adutil keytab createauto --help
```

> [!NOTE]
> `arcfour-hmac` は弱い暗号化であり、運用環境での暗号化の種類として使用することは推奨されません。

SQL Server によって AD に接続するために使用されるプリンシパル名とパスワードのエントリを、keytab に追加します。

```bash
adutil keytab create -k /var/opt/mssql/secrets/mssql.keytab -p sqluser --password 'P@ssw0rd!'
```

> [!NOTE]
>
> - `-k`:`mssql.keytab` ファイルの作成先となるパス。
> - `-p`:keytab に追加するプリンシパル。

adutil による keytab の作成と自動作成では、以前のファイルは上書きされません。既に存在する場合は、ファイルに追加されるだけです。

確実に作成された keytab が `mssql` ユーザーによって所有されていて、そのファイルへの読み書きアクセス権を `mssql` ユーザーのみが持っているようにします。 次に示すように、`chown` と `chmod` コマンドを実行できます。

```bash
chown mssql. /var/opt/mssql/secrets/mssql.keytab
chmod 440 /var/opt/mssql/secrets/mssql.keytab
```

## <a name="configure-sql-server-to-use-the-keytab"></a>keytab を使用するように SQL Server を構成する

次のコマンドを実行して、前のステップで作成した keytab を使用するように SQL Server を構成し、上記で作成したユーザーとして特権 AD アカウントを設定します。 この例では、ユーザー名は `sqluser` です。

```bash
/opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
/opt/mssql/bin/mssql-conf set network.privilegedadaccount sqluser
```

## <a name="restart-sql-server"></a>SQL Server を再起動する

次のコマンドを実行して、SQL Server サービスを再起動します。

```bash
sudo systemctl restart mssql-server
```

## <a name="create-ad-based-sql-server-logins-in-transact-sql"></a>Transact-SQL で AD ベースの SQL Server ログインを作成する

SQL Server に接続し、次のコマンドを実行して、ログインを作成し、一覧に表示されることを確認します。

```sql
create login [contoso\amvin] From Windows
SELECT name FROM sys.server_principals;
```

## <a name="connect-to-sql-server-using-ad-authentication"></a>AD 認証を使用して SQL Server に接続する。

[SSMS](../ssms/download-sql-server-management-studio-ssms.md) または [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md) を使用して接続するには、Windows 資格情報を使用して SQL Server にログインします。

また、[sqlcmd](../tools/sqlcmd-utility.md) などのツールを使用し、Windows 認証を使用して SQL Server に接続することもできます。

```bash
sqlcmd -E -S 'myubuntu.contoso.com'
```

## <a name="next-steps"></a>次の手順

- [Linux ホスト上の SQL Server を Active Directory ドメインに参加させる](sql-server-linux-active-directory-auth-overview.md)
- SQL Server on Linux コンテナーで AD 認証を構成する方法については、「[SQL Server on Linux コンテナーで Active Directory 認証を構成する](sql-server-linux-containers-ad-auth-adutil-tutorial.md)」を参照してください
