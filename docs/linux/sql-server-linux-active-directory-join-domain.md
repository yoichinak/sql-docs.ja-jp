---
title: SQL Server on Linux を Active Directory に参加させる
titleSuffix: SQL Server
description: この記事では、SQL Server Linux ホスト マシンを AD ドメインに参加させるためのガイダンスを提供します。 組み込みの SSSD パッケージを使用することも、サードパーティの AD プロバイダーを使用することもできます。
author: tejasaks
ms.author: tejasaks
ms.reviewer: vanto
ms.date: 11/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 184744aeea40dd8d21c023806cc63d644311ffde
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419847"
---
# <a name="join-sql-server-on-a-linux-host-to-an-active-directory-domain"></a>Linux ホスト上の SQL Server を Active Directory ドメインに参加させる

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

この記事では、SQL Server Linux ホスト コンピューターを Active Directory (AD) ドメインに参加させる方法に関する一般的なガイダンスを提供します。 組み込みの SSSD パッケージを使用する方法と、サードパーティの Active Directory プロバイダーを使用する方法の 2 つがあります。 サードパーティのドメイン参加製品の例としては、[PowerBroker Identity Services (PBIS)](https://www.beyondtrust.com/)、[One Identity](https://www.oneidentity.com/products/authentication-services/)、[Centrify](https://www.centrify.com/) があります。 このガイドには、Active Directory の構成を確認する手順が含まれます。 ただし、サードパーティのユーティリティを使用してコンピューターをドメインに参加させる方法については説明しません。

## <a name="prerequisites"></a>前提条件

Active Directory 認証を構成する前に、ネットワーク上に Active Directory ドメイン コントローラー (Windows) をセットアップする必要があります。 その後、SQL Server on Linux ホストを Active Directory ドメインに参加させます。

> [!IMPORTANT]
> この記事で説明されている手順の例はガイダンスのみを目的としており、Ubuntu 16.04、Red Hat Enterprise Linux (RHEL) 7.x、および SUSE Enterprise Linux (SLES) 12 オペレーティング システムを参照しています。 お使いの環境での実際の手順は、環境全体の構成方法やオペレーティング システムのバージョンによって多少異なる場合があります。 たとえば、ネットワークの管理と構成には、Ubuntu 18.04 では netplan が使用されますが、Red Hat Enterprise Linux (RHEL) 8.x では nmcli のツールが特に使用されます。 具体的なツール、構成、カスタマイズ、および必要なトラブルシューティングについては、お使いの環境のシステム管理者とドメイン管理者と連携することをお勧めします。

### <a name="reverse-dns-rdns"></a>逆引き DNS (RDNS)

Windows Server を実行しているコンピューターをドメイン コントローラーとして設定した場合、既定では RDNS ゾーンが存在しない可能性があります。 ドメイン コントローラーと、SQL Server を実行する Linux マシンの IP アドレスの両方に適用可能な RDNS ゾーンが必ず存在するようにしてください。

また、ドメイン コントローラーをポイントする PTR レコードが必ず存在するようにしてください。

## <a name="check-the-connection-to-a-domain-controller"></a>ドメイン コントローラーへの接続を確認する

ドメインの短い名前と完全修飾名の両方を使用し、ドメイン コントローラーのホスト名を使って、ドメイン コントローラーに接続できることを確認します。 ドメイン コントローラーの IP は、ドメイン コントローラーの FQDN にも解決される必要があります。

```bash
ping contoso
ping contoso.com
ping dc1.contoso.com
nslookup <IP address of dc1.contoso.com>
```

> [!TIP]
> このチュートリアルでは、ドメイン名と領域名の例として、それぞれ **contoso.com** と **CONTOSO.COM** を使用します。 また、ドメイン コントローラーの完全修飾ドメイン名の例として、**DC1.CONTOSO.COM** も使用します。 これらの名前は実際の値に置き換える必要があります。

これらの名前のチェックのいずれかが失敗した場合は、ドメイン検索リストを更新します。 以下のセクションでは、Ubuntu、Red Hat Enterprise Linux (RHEL)、および SUSE Linux Enterprise Server (SLES) について説明します。

### <a name="ubuntu-1604"></a>Ubuntu 16.04

1. **/etc/network/interfaces** ファイルを編集して、Active Directory ドメインがドメイン検索リストに含まれるようにします。

   ```/etc/network/interfaces
   # The primary network interface
   auto eth0
   iface eth0 inet dhcp
   dns-nameservers **<AD domain controller IP address>**
   dns-search **<AD domain name>**
   ```

   > [!NOTE]
   > ネットワーク インターフェイス `eth0` は、コンピューターによって異なる場合があります。 使用しているものを確認するには、**ifconfig** を実行します。 その後、IP アドレスを持ち、バイトが送受信されたインターフェイスをコピーします。

1. このファイルを編集した後、ネットワーク サービスを再起動します。

   ```bash
   sudo ifdown eth0 && sudo ifup eth0
   ```

1. 次に、**/etc/resolv.conf** ファイルに次の例のような行が含まれていることを確認します。

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="ubuntu-1804"></a>Ubuntu 18.04

1. [sudo vi /etc/netplan/******.yaml] ファイルを編集して、Active Directory ドメインがドメイン検索リストに含まれるようにします。

   ```/etc/netplan/******.yaml
   network:
     ethernets:
       eth0:
               dhcp4: true

               dhcp6: true
               nameservers:
                       addresses: [ **<AD domain controller IP address>**]
                       search: [**<AD domain name>**]
     version: 2
   ```

   > [!NOTE]
   > ネットワーク インターフェイス `eth0` は、コンピューターによって異なる場合があります。 使用しているものを確認するには、**ifconfig** を実行します。 その後、IP アドレスを持ち、バイトが送受信されたインターフェイスをコピーします。

1. このファイルを編集した後、ネットワーク サービスを再起動します。

   ```bash
   sudo netplan apply
   ```

1. 次に、 **/etc/resolv.conf** ファイルに次の例のような行が含まれていることを確認します。

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

### <a name="rhel-7x"></a>RHEL 7.x

1. **/etc/sysconfig/network-scripts/ifcfg-eth0** ファイルを編集して、Active Directory ドメインがドメイン検索リストに含まれるようにします。 または、必要に応じて別のインターフェイス構成ファイルを編集します。

   ```/etc/sysconfig/network-scripts/ifcfg-eth0
   PEERDNS=no
   DNS1=**<AD domain controller IP address>**
   DOMAIN="contoso.com com"
   ```

1. このファイルを編集した後、ネットワーク サービスを再起動します。

   ```bash
   sudo systemctl restart network
   ```

1. 次に、**/etc/resolv.conf** ファイルに次の例のような行が含まれていることを確認します。

   ```/etc/resolv.conf
   search contoso.com com  
   nameserver **<AD domain controller IP address>**
   ```

1. それでもドメイン コントローラーに対して ping を実行できない場合は、ドメイン コントローラーの完全修飾ドメイン名と IP アドレスを検索します。 ドメイン名の例は **DC1.CONTOSO.COM** です。 次のエントリを **/etc/hosts** に追加します。

   ```/etc/hosts
   **<IP address>** DC1.CONTOSO.COM CONTOSO.COM CONTOSO
   ```

### <a name="sles-12"></a>SLES 12

1. **/etc/sysconfig/network/config** ファイルを編集して、Active Directory ドメイン コントローラーの IP アドレスが DNS クエリに対して使用され、Active Directory ドメインがドメイン検索リストに含まれるようにします。

   ```/etc/sysconfig/network/config
   NETCONFIG_DNS_STATIC_SEARCHLIST=""
   NETCONFIG_DNS_STATIC_SERVERS="**<AD domain controller IP address>**"
   ```

1. このファイルを編集した後、ネットワーク サービスを再起動します。

   ```bash
   sudo systemctl restart network
   ```

1. 次に、**/etc/resolv.conf** ファイルに次の例のような行が含まれていることを確認します。

   ```/etc/resolv.conf
   search contoso.com com
   nameserver **<AD domain controller IP address>**
   ```

## <a name="join-to-the-ad-domain"></a>AD ドメインに参加する

基本的な構成およびドメイン コントローラーとの接続を確認した後、SQL Server の Linux ホスト コンピューターを Active Directory ドメイン コントローラーに参加させるには、次の 2 つのオプションがあります。

- [オプション 1: SSSD パッケージを使用する](#option1)
- [オプション 2: サードパーティの openldap プロバイダー ユーティリティを使用する](#option2)

### <a name="option-1-use-sssd-package-to-join-ad-domain"></a><a id="option1"></a> オプション 1: SSSD パッケージを使用して AD ドメインに参加する

この方法では、**realmd** パッケージと **sssd** パッケージを使用して、SQL Server ホストを AD ドメインに参加させます。

> [!NOTE]
> これは、Linux ホストを AD ドメイン コントローラーに参加させる場合に推奨される方法です。

SQL Server ホストを Active Directory ドメイン に参加させるには、次の手順のようにします。

1. [realmd](https://www.freedesktop.org/software/realmd/docs/guide-active-directory-join) を使用して、ホスト コンピューターを AD ドメインに参加させます。 最初に、お使いの Linux ディストリビューションのパッケージ マネージャーを用して、SQL Server ホスト コンピューターに **realmd** パッケージと Kerberos クライアント パッケージの両方をインストールする必要があります。

   **RHEL:**

   ```base
   sudo yum install realmd krb5-workstation
   ```
   
   **SLES 12:**
   
   これらの手順は SLES 12 (Linux で公式にサポートされている唯一の SUSE のバージョン) に固有のものであることに注意してください。

   ```bash
   sudo zypper addrepo https://download.opensuse.org/repositories/network/SLE_12/network.repo
   sudo zypper refresh
   sudo zypper install realmd krb5-client sssd-ad
   ```

   **Ubuntu 16.04:**

   ```bash
   sudo apt-get install realmd krb5-user software-properties-common python-software-properties packagekit
   ```

   **Ubuntu 18.04:**

   ```bash
   sudo apt-get install realmd krb5-user software-properties-common python3-software-properties packagekit
   sudo apt-get install adcli libpam-sss libnss-sss sssd sssd-tools
   ```

1. Kerberos クライアント パッケージのインストール時に、領域名の入力を求められた場合は、ドメイン名を大文字で入力します。

1. DNS が正しく構成されたことを確認した後、次のコマンドを実行してドメインに参加します。 新しいコンピューターをドメインに参加させるのに十分な特権を AD に持っている AD アカウントを使って、認証を行う必要があります。 このコマンドでは、AD に新しいコンピューター アカウントが作成され、**/etc/krb5.keytab** ホスト keytab ファイルが作成され、**/etc/sssd/sssd.conf** でドメインが構成されて、**/etc/krb5.conf** が更新されます。

   **realmd** に問題があるため、まず、コンピューターのホスト名をコンピューター名ではなく、FQDN に設定します。 そうしないと、**realmd** によってコンピューターに必要なすべての SPN が作成されない可能性があり、DNS エントリが自動的に更新されません。これは、ドメイン コントローラーで動的 DNS 更新がサポートされている場合でも同様です。
   
   ```bash
   sudo hostname <old hostname>.contoso.com
   ```
   
   上記のコマンドを実行した後、/etc/hostname ファイルには <old hostname>.contoso.com が含まれているはずです。

   ```bash
   sudo realm join contoso.com -U 'user@CONTOSO.COM' -v
   ```

   `Successfully enrolled machine in realm` というメッセージが表示されます。

   受け取る可能性のあるエラー メッセージとその解決方法を、次の表に示します。

   | エラー メッセージ | 推奨 |
   |---|---|
   | `Necessary packages are not installed` | realm join コマンドを再び実行する前に、お使いの Linux ディストリビューションのパッケージ マネージャーを使って、それらのパッケージをインストールします。 |
   | `Insufficient permissions to join the domain` | ドメイン管理者に連絡し、Linux コンピューターをドメインに参加させるのに十分なアクセス許可があることを確認します。 |
   | `KDC reply did not match expectations` | ユーザーに対して正しい領域名を指定していない可能性があります。 領域名は大文字と小文字が区別され、通常は大文字であり、コマンド realm discover contoso.com で識別できます。 |

   SQL Server では、ユーザー アカウントとグループをセキュリティ識別子 (SID) にマップするために、SSSD と NSS が使われます。 AD ログインを正常に作成するには、SSSD が SQL Server 用に構成されて実行されている必要があります。 通常、これは **realmd** によってドメインへの参加の一環として自動的に行われますが、場合によってはこれを別途行う必要があります。

   詳しくは、[SSSD を手動で構成する](https://access.redhat.com/articles/3023951)方法および [NSS を SSSD で動作するように構成する](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/system-level_authentication_guide/configuring_services#Configuration_Options-NSS_Configuration_Options)方法を参照してください。

1. ドメインからユーザーに関する情報を収集できるようになったこと、およびそのユーザーとして Kerberos チケットを取得できることを確認します。 次の例では、これのために **id**、[kinit](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/kinit.html)、および [klist](https://web.mit.edu/kerberos/krb5-1.12/doc/user/user_commands/klist.html) コマンドが使われています。

   ```bash
   id user@contoso.com

   uid=1348601103(user@contoso.com) gid=1348600513(domain group@contoso.com) groups=1348600513(domain group@contoso.com)

   kinit user@CONTOSO.COM

   Password for user@CONTOSO.COM:

   klist
   Ticket cache: FILE:/tmp/krb5cc_1000
   Default principal: user@CONTOSO.COM
   ```

   > [!NOTE]
   > - **id user\@contoso.com** で `No such user` が返される場合は、`sudo systemctl status sssd` コマンドを実行して、SSSD サービスが正常に開始されていることを確認します。 サービスが実行されているのにエラーが表示される場合は、SSSD の詳細ログを有効にしてみます。 詳しくは、[SSSD のトラブルシューティング](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/System-Level_Authentication_Guide/trouble.html#SSSD-Troubleshooting)に関する Red Hat のドキュメントを参照してください。
   >
   > - **kinit user\@CONTOSO.COM** から `KDC reply did not match expectations while getting initial credentials` が返される場合は、領域を大文字で指定したことを確認します。

詳しくは、[ID ドメインの検出と参加](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/realmd-domain.html)に関する Red Hat のドキュメントを参照してください。

### <a name="option-2-use-third-party-openldap-provider-utilities"></a><a id="option2"></a> オプション 2: サードパーティの openldap プロバイダー ユーティリティを使用する

[PBIS](https://www.beyondtrust.com/)、[VAS](https://www.oneidentity.com/products/authentication-services/)、[Centrify](https://www.centrify.com/) などのサードパーティ製ユーティリティを使用できます。 この記事では、個々のユーティリティの手順については説明しません。 最初に、これらのユーティリティのいずれかを使って、SQL Server 用 Linux ホストをドメインに参加させる必要があります。  

SQL Server では、AD 関連のクエリに対して、サードパーティのインテグレーターのコードまたはライブラリは使われません。 SQL Server では常に、このセットアップでの openldap ライブラリの直接呼び出しを使って、AD のクエリが行われます。 サードパーティのインテグレーターは、Linux ホストを AD ドメインに参加させるためにのみ使われ、SQL Server ではこれらのユーティリティとの直接的な通信は行われません。

> [!IMPORTANT]
> 記事「[SQL Server on Linux で Active Directory 認証を使用する](sql-server-linux-active-directory-authentication.md#additionalconfig)」の「**その他の構成オプション**」セクションで、**mssql-conf** `network.disablesssd` 構成オプションの使用に関する推奨事項を参照してください。

**/etc/krb5.conf** が正しく構成されていることを確認します。 ほとんどのサードパーティ製 Active Directory プロバイダーでは、この構成は自動的に行われます。 ただし、後で問題が発生するのを防ぐため、**/etc/krb5.conf** で次の値を確認してください。

```/etc/krb5.conf
[libdefaults]
default_realm = CONTOSO.COM

[realms]
CONTOSO.COM = {
}

[domain_realm]
contoso.com = CONTOSO.COM
.contoso.com = CONTOSO.COM
```

## <a name="check-that-the-reverse-dns-is-properly-configured"></a>逆引き DNS が正しく構成されていることを確認する

次のコマンドでは、SQL Server が実行されているホストの完全修飾ドメイン名 (FQDN) が返されます。 たとえば、**SqlHost.contoso.com** などです。

```bash
host **<IP address of SQL Server host>**
```

このコマンドの出力は、`**<reversed IP address>**.in-addr.arpa domain name pointer SqlHost.contoso.com` のようになる必要があります。 このコマンドでホストの FQDN が返されない場合、または FQDN が正しくない場合は、SQL Server on Linux ホストの逆引き DNS エントリを DNS サーバーに追加します。

## <a name="next-steps"></a>次のステップ

この記事では、Active Directory 認証を使用する Linux ホストコンピューターで SQL Server を構成するための前提条件が示されています。 Active Directory アカウントをサポートするための SQL Server on Linux の構成を完了するには、「[SQL Server on Linux で Active Directory 認証を使用する](sql-server-linux-active-directory-authentication.md)」の手順に従ってください。
