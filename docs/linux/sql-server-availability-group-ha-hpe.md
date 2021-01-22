---
title: HPE Serviceguard を使用して可用性グループを展開する - SQL Server on Linux
description: クラスター マネージャーとして HPE Serviceguard を使用して、SQL Server on Linux で可用性グループによる高可用性を実現する
ms.date: 01/15/2021
ms.prod: sql
ms.technology: linux
ms.topic: tutorial
author: amvin87
ms.author: amitkh
ms.reviewer: vanto
ms.openlocfilehash: 3956c0470ac9f4b3ac2f2a35ed057015db6ea0e0
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534896"
---
# <a name="tutorial---setup-a-three-node-always-on-availability-group-with-hpe-serviceguard-for-linux"></a>チュートリアル - HPE Serviceguard for Linux を使用して 3 ノード Always On 可用性グループをセットアップする 

このチュートリアルでは、オンプレミスの Virtual Machines (VM) で実行されている HPE Serviceguard for Linux を使用して SQL Server Always On 可用性グループを構成する方法について説明します。

HPE Serviceguard クラスターの概要については、[HPE Serviceguard クラスター](https://h20195.www2.hpe.com/v2/GetPDF.aspx/c04154488.pdf)に関する記事を参照してください。

> [!NOTE]
> Microsoft では、データ移動、可用性グループ、および SQL Server コンポーネントをサポートしています。 HPE Serviceguard クラスターとクォーラム管理のドキュメントに関するサポートについては、HPE にお問い合わせください。

このチュートリアルは、次のタスクで構成されています。

> [!div class="checklist"]
> * 可用性グループに含める 3 つのすべての VM に SQL Server をインストールする
> * VM に HPE Serviceguard をインストールする
> * HPE Serviceguard クラスターを作成する
> * 可用性グループを作成し、その可用性グループにサンプル データベースを追加する
> * Serviceguard クラスター マネージャーを使用して可用性グループに SQL Server ワークロードを展開する
> * 自動フェールオーバーを実行し、ノードをクラスターに再び参加させる

## <a name="prerequisites"></a>前提条件

* サポートされている Linux ディストリビューションで HPE Serviceguard を実行する、オンプレミス環境内の 3 つの VM。

   サポートされているディストリビューションの例については、「[HPE Serviceguard for Linux](https://h20195.www2.hpe.com/v2/gethtml.aspx?docname=c04154488)」を参照してください。

   パブリック クラウド環境のサポートについては、HPE に関する情報を確認してください。

   このチュートリアルの手順は、HPE Serviceguard for Linux に対して検証されています。 試用版は [HPE](https://www.hpe.com/us/en/resources/servers/serviceguard-linux-trial.html) からダウンロードできます。

* 3 つのすべての仮想マシンに対する論理ボリューム マウント (LVM) 上の SQL Server データベース ファイル。 [Serviceguard Linux (HPE) のクイック スタート ガイド](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us)を参照してください。

* VM に OpenJDK java ランタイムがインストールされていることを確認してください。

   > [!NOTE]
   > IBM java sdk はサポートされていません。

## <a name="install-sql-server"></a>SQL Server をインストールする

3 つのすべての VM で、このチュートリアルで選択した Linux ディストリビューションに基づいて、次のいずれかの手順に従って SQL Server とツールをインストールします。

### <a name="rhel"></a>RHEL

* [Red Hat に SQL Server をインストールする](quickstart-install-connect-red-hat.md#install)
* [ツール](quickstart-install-connect-red-hat.md#tools)

### <a name="sles"></a>SLES

* [SLES に SQL Server をインストールする](quickstart-install-connect-suse.md#install)
* [ツール](quickstart-install-connect-suse.md#tools)

この手順を完了すると、可用性グループに参加する 3 つのすべての VM に SQL Server サービスおよびツールがインストールされます。

## <a name="install-hpe-serviceguard-on-the-vms"></a>VM に HPE Serviceguard をインストールする

この手順では、3 つのすべての VM に HPE Serviceguard for Linux をインストールします。 次の表では、各サーバーがクラスターで果たすロールについて説明します。

|[Number of VMs]\(VM の数\) | HPE Servicguard ロール | Microsoft SQL Server 可用性グループのレプリカ ロール|
|--------------|-----------------|------------|
|1 | HPE Serviceguard クラスター ノード | プライマリ レプリカ |
|1 つ以上 | HPE Serviceguard クラスター ノード | セカンダリ レプリカ |
|1 | HPE Serviceguard クォーラム サーバー | 構成専用レプリカ |

Serviceguard をインストールするには、`cminstaller` メソッドを使用します。 具体的な手順については、以下のリンクを参照してください。

Serviceguard クラスターと Serviceguard クォーラム サーバー

* [2 つのノードに Serviceguard for Linux をインストールします](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Install_serviceguard_using_cminstaller)。 「**Install_serviceguard_using_cminstaller**」セクションを参照してください。
* [3 番目のノードに Serviceguard クォーラム サーバーをインストールします](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Install_QS_from_the_ISO)。 「**Install_QS_from_the_ISO**」セクションを参照してください。

HPE Serviceguard クラスターのインストールが完了したら、プライマリ レプリカ ノード上の TCP ポート 5522 でクラスター管理ポータルを有効にすることができます。 次の手順では、5522 を許可するルールをファイアウォールに追加します。次のコマンドは RHEL ディストリビューション用で、他のディストリビューションについては同様のコマンドを実行する必要があります。

```console
sudo firewall-cmd --zone=public --add-port=5522/tcp --permanent

sudo firewall-cmd --reload 
```

## <a name="create-hpe-serviceguard-cluster"></a>HPE Serviceguard クラスターを作成する

HPE Serviceguard クラスターを構成して作成するには、次の手順に従います。 この手順では、クォーラム サーバーも構成します。

1. [3 番目のノードで Serviceguard クォーラム サーバーを構成します](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Configure_QS)。 「**Configure_QS**」セクションを参照してください。
2. [他の 2 つのノードで Serviceguard クラスターを構成して作成します](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Configure_and_create_cluster)。 「**Configure_and_create_Cluster**」セクションを参照してください。

## <a name="create-the-availability-group-and-add-a-sample-database"></a>可用性グループを作成し、サンプル データベースを追加する

この手順では、2 つ (以上) の同期レプリカと構成専用レプリカを持つ可用性グループを作成します。これにより、データ保護が提供され、また高可用性を提供することもできます。 次の図は、このアーキテクチャを表したものです。

:::image type="content" source="media/sql-server-linux-availability-group-ha/2-configuration-only.png" alt-text="プライマリ レプリカにより、ユーザー データおよび構成データがセカンダリ レプリカと同期されます。プライマリ レプリカにより、構成データのみが構成専用レプリカと同期されます。構成専用レプリカにはユーザー データは含まれません。":::

1. セカンダリ レプリカへのユーザー データの同期レプリケーションです。 これには、可用性グループの構成メタデータも含まれます。

2. 可用性グループの構成メタデータの同期レプリケーションです。 ユーザー データは含まれません。

詳細については、「[2 つの同期レプリカと 1 つの構成専用レプリカ](sql-server-linux-availability-group-ha.md)」を参照してください。

可用性グループを作成するには、次の手順に従います。

1. 構成専用レプリカを含むすべての VM で [Always On 可用性グループを有効にし、mssql-server を再起動する](#enable-always-on-availability-groups-and-restart-mssql-server)。
2. [`AlwaysOn_health` イベント セッションを有効にする (省略可能)](#enable-an-alwayson_health-event-session---optional)
3. [プライマリ VM で証明書を作成する](#create-a-certificate-on-the-primary-vm)
4. [セカンダリ サーバーで証明書を作成する](#create-the-certificate-on-secondary-servers)
5. [レプリカにデータベース ミラーリング エンドポイントを作成する](#create-the-database-mirroring-endpoints-on-the-replicas)
6. [可用性グループを作成する](#create-availability-group)
7. [セカンダリ レプリカに参加する](#join-the-secondary-replicas)
8. [先ほど作成した可用性グループにデータベースを追加する](#add-a-database-to-the-availability-group-created-above)

### <a name="enable-always-on-availability-groups-and-restart-mssql-server"></a>Always On 可用性グループを有効にして mssql-server を再起動する

SQL Server インスタンスをホストするすべてのノードで、Always On 機能を有効にします。 次に、mssql-server を再起動します。 3 つのすべてのノードで次のスクリプトを実行します。

```console
sudo /opt/mssql/bin/mssql-conf
set hadr.hadrenabled 1 sudo systemctl restart mssql-serve
```

### <a name="enable-an-alwayson_health-event-session---optional"></a>`AlwaysOn_health` イベント セッションを有効にする (省略可能)

オプションで、AlwaysOn 可用性グループの拡張イベントを有効にすると、可用性グループのトラブルシューティング時の根本原因の診断に役立ちます。 SQL Server の各インスタンスで次のコマンドを実行します。

```tsql
ALTER EVENT SESSION AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

### <a name="create-a-certificate-on-the-primary-vm"></a>プライマリ VM で証明書を作成する

次の Transact-SQL スクリプトでは、マスター キーと証明書を作成します。 その後、証明書をバックアップし、秘密キーでファイルをセキュリティ保護します。 強力なパスワードでスクリプトを更新してください。 プライマリ SQL Server インスタンスに接続し、次の Transact-SQL スクリプトを実行します。

```tsql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<Master_Key_Password';

CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';

BACKUP CERTIFICATE dbm_certificate TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
WITH PRIVATE KEY 
    ( FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
      ENCRYPTION BY PASSWORD = '<Private_Key_Password>' );

```

この時点で、プライマリ SQL Server レプリカの `/var/opt/mssql/data/dbm_certificate.cer` には証明書が、`var/opt/mssql/data/dbm_certificate.pvk` には秘密キーが作成されています。 これら 2 つのファイルを、可用性レプリカをホストするすべてのサーバー上の同じ場所にコピーします。 mssql ユーザーを使うか、またはこれらのファイルへのアクセス許可を mssql ユーザーに付与します。

たとえば、ソース サーバーでは、次のコマンドでファイルがターゲット コンピューターにコピーされます。 `'node2'` の値を、セカンダリ SQL Server インスタンスを実行しているホストの名前に置き換えます。 同様に、構成専用レプリカの証明書をコピーし、そのノードで次のコマンドを実行します。

```console
cd /var/opt/mssql/data
scp dbm_certificate.* root@<node2>:/var/opt/mssql/data/
```

次に、セカンダリ インスタンスを実行しているセカンダリ VM、および SQL Server の構成専用レプリカで、次のコマンドを実行します。これにより、mssql ユーザーはコピーした証明書を所有できます。

```console
cd /var/opt/mssql/data

chown mssql:mssql dbm_certificate.*
```

### <a name="create-the-certificate-on-secondary-servers"></a>セカンダリ サーバーで証明書を作成する

次の Transact-SQL スクリプトでは、プライマリ SQL Server レプリカで作成したバックアップからマスター キーと証明書を作成します。 強力なパスワードでスクリプトを更新してください。 暗号化解除パスワードは、前の手順で .pvk ファイルの作成に使ったものと同じパスワードです。 証明書を作成するには、構成専用レプリカを除くすべてのセカンダリ サーバーで次のスクリプトを実行します。

```tsql
CREATE MASTER KEY ENCRYPTION BY PASSWORD =
'<Master_Key_Password>';

CREATE CERTIFICATE dbm_certificate FROM FILE =
'/var/opt/mssql/data/dbm_certificate.cer'
WITH PRIVATE KEY ( FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
DECRYPTION BY PASSWORD = '<Private_Key_Password>' );
```

### <a name="create-the-database-mirroring-endpoints-on-the-replicas"></a>レプリカにデータベース ミラーリング エンドポイントを作成する

プライマリ レプリカとセカンダリ レプリカで次のコマンドを実行して、データベース ミラーリング エンドポイントを作成します。

```tsql
CREATE ENDPOINT [hadr_endpoint] AS TCP (LISTENER_PORT = 5022)
    FOR DATABASE_MIRRORING 
        (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );

ALTER ENDPOINT [hadr_endpoint] STATE = STARTED;
```

> [!NOTE]
> 5022 は、データベース ミラーリング エンドポイントで使用される標準ポートですが、使用可能な任意のポートに変更することができます。

構成専用レプリカで、次のコマンドを使用してデータベース ミラーリング エンドポイントを作成します。ここでのロールの値は、構成専用レプリカに必要な `WITNESS` に設定されています。

```tsql
CREATE ENDPOINT [hadr_endpoint] AS TCP (LISTENER_PORT = 5022)
    FOR DATABASE_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );

ALTER ENDPOINT [hadr_endpoint] STATE = STARTED;
```

### <a name="create-availability-group"></a>可用性グループを作成する

プライマリ レプリカ インスタンスで、次のコマンドを実行します。 これらのコマンドにより、**ag1** という名前の可用性グループが作成されます。これには **External** `cluster_type` が含まれており、これにより、この可用性グループにデータベースの作成権限が付与されます。

次のスクリプトを実行する前に、`<node1>`、`<node2>`、および `<node3>` (構成専用レプリカ) プレースホルダーを、前の手順で作成した VM の名前に置き換えます。

```tsql
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR REPLICA ON
    N'<node1>' WITH (
        ENDPOINT_URL = N'tcp://<node1>:<5022>',
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
        FAILOVER_MODE = EXTERNAL,
        SEEDING_MODE = AUTOMATIC
        ),

    N'<node2>' WITH (
        ENDPOINT_URL = N'tcp://<node2>:\<5022>',
        AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
        FAILOVER_MODE = EXTERNAL,
        SEEDING_MODE = AUTOMATIC
        ),
    
    N'<node3>' WITH (
        ENDPOINT_URL = N'tcp://<node3>:<5022>',
        AVAILABILITY_MODE = CONFIGURATION_ONLY
        );
          
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-the-secondary-replicas"></a>セカンダリ レプリカに参加する

すべてのセカンダリ レプリカで次のコマンドを実行します。 これらのコマンドにより、セカンダリ レプリカがプライマリ レプリカと共に "ag1" 可用性グループに参加し、ag1 可用性グループにデータベースの作成アクセスが付与されます。

```tsql
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
GO
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
GO
```

### <a name="add-a-database-to-the-availability-group-created-above"></a>先ほど作成した可用性グループにデータベースを追加する

プライマリ レプリカに接続し、次の T-SQL コマンドを実行して、次の操作を実行します。

1. 可用性グループに追加する **db1** という名前のサンプル データベースを作成します。
2. データベースの復旧モデルを full に設定します。 可用性グループ内のすべてのデータベースには、full 復旧モデルが必要です。
3. データベースをバックアップします。 可用性グループにデータベースを追加するには、データベースに少なくとも 1 つの完全バックアップが必要です。

```tsql
CREATE DATABASE [db1]; -- creates a database named db1
GO
ALTER DATABASE [db1] SET RECOVERY FULL; -- set the database in full recovery mode
GO
BACKUP DATABASE [db1] -- backs up the database to disk TO DISK = N'/var/opt/mssql/data/db1.bak';
GO
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1]; -- adds the database db1 to the AG
GO
```

前の手順が正常に完了すると、**ag1** 可用性グループが作成され、1 つのプライマリ レプリカ、1 つのセカンダリ レプリカ、および 1 つの構成専用レプリカを含むレプリカとして 3 つの VM が追加されます。 **ag1** には、データベースが 1 つ含まれています。

## <a name="deploy-the-sql-server-availability-group-workload-hpe-cluster-manager"></a>SQL Server 可用性グループ ワークロードを展開する (HPE クラスター マネージャー)

HPE Serviceguard で、Serviceguard クラスター マネージャー UI を使用して可用性グループに SQL Server ワークロードを展開します。
   
[Serviceguard マネージャーのグラフィカル ユーザー インターフェイス](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Protect_your_alwayson_availability_group)を使用して、可用性グループ ワークロードを展開し、高可用性 (HA)、Serviceguard クラスター経由でのディザスター リカバリー (DR) を有効にします。 **Always On 可用性グループの Microsoft SQL Server on Linux の保護** に関するセクションを参照してください。

## <a name="perform-automatic-failover-and-join-the-node-back-to-cluster"></a>自動フェールオーバーを実行し、ノードをクラスターに再び参加させる

自動フェールオーバー テストでは、プライマリ レプリカをダウンさせて (電源オフ)、プライマリ ノードの突然の停止をレプリケートできます。 予期される動作は次のとおりです。

1. クラスター マネージャーにより、可用性グループ内のいずれかのセカンダリ レプリカがプライマリに昇格します。
2. 失敗したプライマリ レプリカは、バックアップされた後に自動的にクラスターに参加します。 これは、クラスター マネージャーによってセカンダリ レプリカに昇格します。

HPE Serviceguard については、「[**Testing the setup for failover readiness**](https://support.hpe.com/hpesc/public/docDisplay?docId=a00107699en_us#Test_the_setup_preparedness)」(フェールオーバーの準備のセットアップのテスト) セクションを参照してください。

## <a name="next-steps"></a>次のステップ

Always On の詳細については、[Linux 上の可用性グループ](sql-server-linux-availability-group-overview.md)に関するページを参照してください。
