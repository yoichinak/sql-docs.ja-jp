---
title: Active Directory モードでの展開
titleSuffix: SQL Server Big Data Cluster
description: Active Directory ドメインで SQL Server ビッグ データ クラスターをアップグレードする方法について説明します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 48dde8000274ea74df1c6095714b54669c5becdd
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257292"
---
# <a name="deploy-sql-server-big-data-cluster-in-active-directory-mode"></a>Active Directory モードで SQL Server ビッグ データ クラスターを展開する

この記事では、Active Directory モードで SQL Server ビッグ データ クラスターを展開する方法について説明します。 この記事の手順では、Active Directory ドメインへのアクセスが必要です。 作業を進める前に、「Active Directory モードで [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]SQL Server ビッグ データ クラスターを展開する](active-directory-prerequisites.md)」で説明されている要件を完了する必要があります。

## <a name="prepare-deployment"></a>展開の準備

AD 統合で BDC を展開するためには、AD で BDC 関連のオブジェクトを作成するために必要な情報をいくつか追加します。

`kubeadm-prod` プロファイル (または CU5 リリース以降の `openshift-prod`) を利用することで、AD 統合に必要なセキュリティ関連の情報とエンドポイント関連の情報のプレースホルダーが自動的に作成されます。

さらに、AD で必要なオブジェクトを作成するために [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] で使用される資格情報を提供する必要があります。 これらの資格情報は環境変数として提供されます。

## <a name="set-security-environment-variables"></a>セキュリティ環境変数の設定

次の環境変数からは、BDC ドメイン サービス アカウントの資格情報が与えられます。この情報が AD 統合の設定に使用されます。 このアカウントはまた、この先、BDC 関連の AD オブジェクトを維持する目的で BDC によって使用されます。

```bash
export DOMAIN_SERVICE_ACCOUNT_USERNAME=<AD principal account name>
export DOMAIN_SERVICE_ACCOUNT_PASSWORD=<AD principal password>
```

## <a name="provide-security-and-endpoint-parameters"></a>セキュリティとエンドポイントのパラメーターを指定する

資格情報の環境変数に加えて、AD 統合が機能するためのセキュリティとエンドポイントの情報も提供する必要があります。 必要なパラメーターは、自動的に `kubeadm-prod`/`openshift-prod` [デプロイ プロファイル](deployment-guidance.md#configfile)に含まれます。

AD 統合には次のパラメーターが必要です: この記事の後半に出てくる `config replace` コマンドを使用し、`control.json` ファイルと `bdc.json` ファイルにこれらのパラメーターを追加します。 下の例ではすべて、サンプル ドメイン `contoso.local` が使用されています。

- `security.activeDirectory.ouDistinguishedName`: クラスターにより作成されたあらゆる AD アカウントが追加される組織単位 (OU) の識別名。 ドメインの名前が `contoso.local` の場合、OU の識別名は `OU=BDC,DC=contoso,DC=local` です。

- `security.activeDirectory.dnsIpAddresses`: ドメインの DNS サーバーの IP アドレスの一覧が含まれます。 

- `security.activeDirectory.domainControllerFullyQualifiedDns`:ドメイン コントローラーの FQDN の一覧。 FQDN には、ドメイン コントローラーのコンピューター名またはホスト名が含まれています。 複数のドメイン コントローラーがある場合、ここで一覧を指定できます。 例: `HOSTNAME.CONTOSO.LOCAL`.

  > [!IMPORTANT]
  > 複数のドメイン コントローラーがドメインにサービスを提供している場合は、セキュリティ構成の `domainControllerFullyQualifiedDns` 一覧の最初のエントリとして、プライマリ ドメインコントローラー (PDC) を使用します。PDC 名を取得するには、コマンド プロンプトで「`netdom query fsmo`」と入力し、 **Enter** キーを押します。

- `security.activeDirectory.realm` **省略可能なパラメーター** : ほとんどの場合、領域はドメイン名と同じです。 同じでない場合、このパラメーターを使用し、領域の名前を定義します (例: `CONTOSO.LOCAL`)。 このパラメーターに指定する値は、完全修飾されている必要があります。

  > [!IMPORTANT]
  > 現時点では、BDC では、Active Directory ドメイン名が Active Directory ドメインの **NETBIOS** 名と異なる構成はサポートされていません。

- `security.activeDirectory.domainDnsName`:クラスターに使用される DNS ドメインの名前 (例: `contoso.local`)。

- `security.activeDirectory.clusterAdmins`:このパラメーターは、1 つの AD グループを受け取ります。 AD グループのスコープは、ユニバーサルまたはグローバルである必要があります。 このグループのメンバーには、クラスターの管理者アクセス許可を付与する `bdcAdmin` クラスター ロールが割り当てられます。 これは、[SQL Server で `sysadmin` アクセス許可](../relational-databases/security/authentication-access/server-level-roles.md#fixed-server-level-roles)、[HDFS で `superuser` アクセス許可](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#The_Super-User)、コントローラー エンドポイントに接続したときに管理者アクセス許可が与えられることを意味します。

  >[!IMPORTANT]
  >展開を開始する前に、このグループを AD 内に作成します。 この AD グループのスコープがドメイン ローカルの場合、展開は失敗します。

- `security.activeDirectory.clusterUsers`:ビッグ データ クラスター内で通常のユーザー (管理者権限なし) となる AD グループの一覧。 この一覧には、ユニバーサル グループまたはグローバル グループのいずれかのスコープを持つ AD グループを含めることができます。 ドメイン ローカル グループを含めることはできません。

この一覧の AD グループは、`bdcUser` ビッグデータ クラスター ロールにマップされており、SQL Server ([SQL Server アクセス許可](../relational-databases/security/permissions-hierarchy-database-engine.md)を参照) または HDFS ([HDFS アクセス許可ガイド](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#:~:text=Permission%20Checks%20%20%20%20Operation%20%20,%20%20N%2FA%20%2029%20more%20rows%20)を参照) へのアクセスが許可される必要があります。 コントローラー エンドポイントに接続されている場合、これらのユーザーは `azdata bdc endpoint list` コマンドを使用して、クラスターで使用可能なエンドポイントのみを一覧表示できます。

この設定の AD グループを更新する方法の詳細については、「[Active Directory モードでビッグ データ クラスター アクセスを管理する](manage-user-access.md)」を参照してください。

  >[!TIP]
  >HDFS に接続するために必要な Knox ゲートウェイ エンドポイントを取得するために、Azure Data Studio では `sys.dm_cluster_endpoints` DMV を使用しています。そのため、Azure Data Studio で SQL Server マスターに接続したときの HDFS ブラウジング エクスペリエンスを有効にするには、bdcUser ロールを持つユーザーに VIEW SERVER STATE 権限を付与する必要があります。

  >[!IMPORTANT]
  >展開を開始する前に、これらのグループを AD 内に作成します。 これらの AD グループのいずれかのスコープがドメイン ローカルの場合、展開は失敗します。

  >[!IMPORTANT]
  >ドメイン ユーザーが多数のグループ メンバーシップを所有している場合は、カスタム *bdc.json* デプロイ構成ファイルを使用して、ゲートウェイ設定 `httpserver.requestHeaderBuffer` (既定値は `8192`) と HDFS 設定 `hadoop.security.group.mapping.ldap.search.group.hierarchy.levels` (既定値は `10`) の値を調整する必要があります。 これは、ゲートウェイへの接続タイムアウトや 431 ( *Request Header Fields Too Large* ) 状態コードの HTTP 応答を回避するためのベスト プラクティスです。 以下は、これらの設定の値を定義する方法と、グループ メンバーシップの数が多い場合に推奨される値を示す構成ファイルのセクションです。

```json
{
    ...
    "spec": {
        "resources": {
            ...
            "gateway": {
                "spec": {
                    "replicas": 1,
                    "endpoints": [{...}],
                    "settings": {
                        "gateway-site.gateway.httpserver.requestHeaderBuffer": "65536"
                    }
                }
            },
            ...
        },
        "services": {
            ...
            "hdfs": {
                "resources": [...],
                "settings": {
                  "core-site.hadoop.security.group.mapping.ldap.search.group.hierarchy.levels": "4"
                }
            },
            ...
        }
    }
}
```

  >[!IMPORTANT]
  >デプロイを開始する前に、AD で下記の設定に提供されるグループを作成します。 これらの AD グループのいずれかのスコープがドメイン ローカルの場合、展開は失敗します。

- `security.activeDirectory.appOwners` **省略可能なパラメーター** : あらゆるアプリケーションを作成、削除、実行する権限が与えられる AD グループの一覧。 この一覧には、ユニバーサル グループまたはグローバル グループのいずれかのスコープを持つ AD グループを含めることができます。 ドメイン ローカル グループを含めることはできません。

- `security.activeDirectory.appReaders` **省略可能なパラメーター** : あらゆるアプリケーションを実行する権限を持つ AD グループの一覧。 この一覧には、ユニバーサル グループまたはグローバル グループのいずれかのスコープを持つ AD グループを含めることができます。 ドメイン ローカル グループを含めることはできません。

次の表に、アプリケーション管理用の承認モデルを示します。

|   承認済みロール   |   [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] コマンド   |
|----------------------|--------------------|
|   appOwner           | azdata app create  |
|   appOwner           | azdata app update  |
|   appOwner、appReader| azdata app list    |
|   appOwner、appReader| azdata app describe|
|   appOwner           | azdata app delete  |
|   appOwner、appReader| azdata app run     |

- `security.activeDirectory.subdomain`: **省略可能なパラメーター** このパラメーターは、同じドメインに対する複数のビッグ データ クラスターのデプロイをサポートするために SQL Server 2019 CU5 リリースで導入されました。 この設定を使用すると、デプロイされたビッグ データ クラスターごとに異なる DNS 名を指定できます。 このパラメーターの値が `control.json` ファイルの Active Directory セクションに指定されていない場合、既定で、ビッグ データ クラスター名 (Kubernetes 名前空間名と同じ) がサブドメイン設定の値を計算するために使用されます。 

  >[!NOTE]
  >サブドメイン設定を介して渡される値は、新しい AD ドメインではなく、BDC クラスターによって内部で使用される DNS ドメインだけです。

  >[!IMPORTANT]
  >これらの新機能を利用し、同じドメイン内に複数のビッグ データ クラスターをデプロイするには、SQL Server 2019 CU5 リリース以降の **[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]** の最新バージョンをインストールまたはアップグレードする必要があります。

  同じ Active Directory ドメインに複数のビッグ データクラスターをデプロイすることに関する詳細については、[概念: Active Directory モードで [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] をデプロイする](active-directory-deployment-background.md)方法に関するページを参照してください。

- `security.activeDirectory.accountPrefix`: **省略可能なパラメーター** このパラメーターは、同じドメインに対する複数のビッグ データ クラスターのデプロイをサポートするために SQL Server 2019 CU5 リリースで導入されました。 この設定により、さまざまなビッグ データ クラスター サービスに対してアカウント名の一意性が保証されます。それは 2 つのクラスター間で異なる必要があります。 アカウント プレフィックス名のカスタマイズは省略可能で、既定では、サブドメイン名がアカウント プレフィックスとして使用されます。 サブドメイン名が 12 文字より長い場合、サブドメイン名の最初の 12 文字がアカウント プレフィックスとして使用されます。  

  >[!NOTE]
  >Active Directory では、アカウント名を 20 文字までに制限する必要があります。 ポッドと StatefulSet を区別するために、BDC クラスターでは 8 文字を使用する必要があります。 これにより、アカウント プレフィックスの制限として 12 文字が残されます

[AD グループのスコープを確認](/powershell/module/addsadministration/get-adgroup)し、DomainLocal であるかどうかを確認します。

展開構成ファイルをまだ初期化していない場合、このコマンドを実行して構成のコピーを取得できます。 次の例では、`kubeadm-prod` プロファイルを使用します。これは `openshift-prod` にも当てはまります。

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

`control.json` ファイルで上記のパラメーターを設定するには、次の [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] コマンドを使用します。 これらのコマンドによって展開前に構成が置換され、独自の値が提供されます。

> [!IMPORTANT]
> SQL Server 2019 CU2 リリースでは、展開プロファイルのセキュリティ構成セクションの構造が多少変更され、Active Directory 関連の設定はすべて、`control.json` ファイル内の `security` の下にある json ツリー内の新しい `activeDirectory` 内にあります。

>[!NOTE]
> このセクションで説明されているように、サブドメインに異なる値を指定するだけでなく、同じ Kubernetes クラスターに複数の BDC をデプロイする場合は、BDC エンドポイントに異なるポート番号を使用する必要もあります。 これらのポート番号は、デプロイ時に [デプロイ構成](deployment-custom-configuration.md)プロファイルを使用して構成できます。

次の例は、SQL Server 2019 CU2 の使用に基づいています。 この例は、展開構成内の AD 関連のパラメーター値を置き換える方法を示しています。下のドメインの詳細はサンプルの値です。

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

必要に応じて SQL Server 2019 CU5 リリースを起動するだけで、`subdomain` と `accountPrefix` の設定の既定値をオーバーライドできます。

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.subdomain=[\"bdctest\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.accountPrefix=[\"bdctest\"]"
```

同様に、SQL Server 2019 CU2 以前のリリースでは、次のことを実行できます。

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

上記の情報に加え、さまざまなクラスター エンドポイントの DNS 名を指定する必要もあります。 指定した DNS 名を使用する DNS エントリは、展開時に DNS サーバーで自動的に作成されます。 これらの名前は、さまざまなクラスター エンドポイントに接続するときに使用します。 たとえば、SQL マスター インスタンスの DNS 名が `mastersql` で、サブドメインで `control.json` にクラスター名の既定値を使用することを考えている場合は、`mastersql.contoso.local,31433` または `mastersql.mssql-cluster.contoso.local,31433` (デプロイ構成ファイルでエンドポイント DNS 名に対して指定した値によって異なります) を使用して、ツールからマスター インスタンスに接続します。 

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[1].dnsName=<monitoring services DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=<SQL Master Primary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=<SQL Master Secondary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=<Gateway (Knox) DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=<app proxy DNS name>.<Domain name. e.g. contoso.local>"
```

> [!IMPORTANT]
> 任意のエンドポイント DNS 名を使用できます。ただし、これらが完全に修飾されており、同じドメインにデプロイされた任意の 2 つのビッグ データ クラスター間で競合しない場合に限ります。 必要に応じて、`subdomain` パラメーター値を使用して、クラスター間で確実に DNS 名が異なるようにすることができます。 次に例を示します。

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.<subdomain e.g. mssql-cluster>.contoso.local"
```

AD 統合を利用し、単一ノード Kubernetes クラスター (kubeadm) で SQL Server ビッグ データ クラスターを展開するサンプル スクリプトは[こちら](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm-ad)にあります。

> [!Note]
> 新しく導入された `subdomain` パラメーターに対応できないシナリオもあります。 たとえば、CU5 より前のリリースをデプロイする必要があり、 **[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]** がアップグレード済みである場合です。 これは非常にまれですが、CU5 より前の動作に戻す必要がある場合は、`control.json` の Active Directory セクションで `useSubdomain` パラメーターを `false` に設定できます。  これを実行するコマンドを次に示します。

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.useSubdomain=false"
```

これで、Active Directory 統合を使用し、BDC の展開に必要なパラメーターをすべて設定できたはずです。

[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] コマンドと kubeadm-prod デプロイ プロファイルを使用して、Active Directory と統合された BDC クラスターをデプロイできるようになりました。 [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] をデプロイする方法の完全なドキュメントについては、「[Kubernetes 上に SQL Server ビッグ データ クラスターを展開する方法](deployment-guidance.md)」を参照してください。

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>ドメイン コントローラーの逆引き DNS エントリを確認する

ドメイン コントローラー自体の逆引き DNS エントリ (PTR レコード) が DNS サーバーに登録されていることを確認します。 これは、ドメイン コントローラーでドメイン名の `nslookup` を実行し、ドメイン名がドメイン コントローラー IP アドレスで解決されるかを調べることで確認できます。

## <a name="known-issues-and-limitations"></a>既知の問題と制限事項

**SQL Server 2019 CU5 で注意すべき制限事項**

- 現在のところ、ログ検索ダッシュボードとメトリクス ダッシュボードは AD 認証に対応していません。 展開時に設定される基本ユーザー名とパスワードは、これらのダッシュボードに対する認証に使用することができます。 他のすべてのクラスター エンドポイントは、AD 認証に対応しています。

- セキュア AD モードは現在のところ、`kubeadm` および `openshift` デプロイ環境でのみ動作し、AKS または ARO では動作しません。 `kubeadm-prod` および `openshift-prod` デプロイ プロファイルには既定で、セキュリティ セクションが含まれています。

- SQL Server 2019 CU5 リリースより前は、ドメイン (Active Directory) につき BDC が 1 つしか許可されません。 CU5 リリース以降では、ドメインごとに複数の BDC を有効にすることができます。

- セキュリティ構成で指定されているどの AD グループも、DomainLocal にスコープ指定できません。 AD グループのスコープは、[この手順](/powershell/module/addsadministration/get-adgroup)に従って確認できます。

- BDC へのログインに使用できる AD アカウントは、BDC 用に構成されたのと同じドメインから許可されます。 その他の信頼される側のドメインからのログインを有効にすることはサポートされていません。

## <a name="next-steps"></a>次のステップ

[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]SQL Server ビッグ データ クラスターを接続する: Active Directory モード](active-directory-connect.md)

[SQL Server ビッグ データ クラスターの Active Directory 統合のトラブルシューティング](troubleshoot-active-directory.md)

[概念: Active Directory モードで [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] をデプロイする](active-directory-deployment-background.md)
