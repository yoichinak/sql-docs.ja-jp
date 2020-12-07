---
title: Active Directory ドメインに複数をデプロイする
titleSuffix: SQL Server Big Data Cluster
description: 単一の Active Directory ドメインに複数の SQL Server ビッグ データ クラスターをデプロイする方法について説明します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 144b769ce42b192099678cda4cfe6fb2935c1c2f
ms.sourcegitcommit: af663bdca0df8a1f34a14667390662f6f0e17766
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/19/2020
ms.locfileid: "94924169"
---
# <a name="deploy-multiple-big-data-clusters-2019-in-the-same-active-directory-domain"></a>同じ Active Directory ドメインに複数の [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]をデプロイする

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

この記事では、SQL Server 2019 CU5 への更新について説明します。これにより、複数の SQL Server 2019 ビッグ データ クラスターを同じ Active Directory ドメインにデプロイして統合できるようになります。

SQL 2019 CU5 より前は、2 つの問題のため、1 つの AD ドメインに複数の BDC をデプロイできませんでした。

- サービス プリンシパル名と DNS ドメインの名前の競合
- ドメイン アカウント プリンシパル名

## <a name="object-name-collisions"></a>オブジェクト名の競合

### <a name="service-principal-names-spn-and-dns-domain-naming-conflict"></a>サービス プリンシパル名 (SPN) と DNS ドメインの名前の競合

デプロイ時に指定されたドメイン名は AD DNS ドメインとして使用されます。 これは、この DNS ドメインを使用して、内部ネットワークでポッドを相互に接続できることを意味します。 さらに、ユーザーはこの DNS ドメインを使用して、BDC エンドポイントに接続します。 その結果、BDC 内のサービスに対して作成されたサービス プリンシパル名 (SPN) の場合、Kubernetes ポッド、サービス、またはエンドポイントの名前がこの AD DNS ドメインで修飾されることになります。 ユーザーがドメインに 2 番目のクラスターをデプロイする場合、生成される SPN の FQDN は同じになります。これは、2 つのクラスターでポッド名と DNS ドメイン名が同じであるためです。 たとえば、AD DNS ドメインが `contoso.local` であるとします。 ポッド `master-0` のマスター プールの SQL Server 用に生成される SPN の 1 つは、`MSSQLSvc/master-0.contoso.local:1433` です。 ユーザーがデプロイしようとしている 2 番目のクラスターでは、`master-0` のポッド名は同じであり、ユーザーは同じ AD DNS ドメイン (``contoso.local``) を指定するため、SPN 文字列が同じになります。 2 番目のクラスターのデプロイの失敗につながる、競合する SPN の作成は、Active Directory によって禁止されます。

### <a name="domain-account-principal-names"></a>ドメイン アカウント プリンシパル名

Active Directory ドメインを使用する BDC のデプロイ時に、BDC 内で実行されているサービスに対して複数のアカウント プリンシパルが生成されます。 これらは基本的には AD ユーザー アカウントです。 SQL 2019 CU5 より前は、これらのアカウントの名前はクラスター間で一意ではありませんでした。 これは、2 つの異なるクラスター内の BDC の特定のサービスに対して、同じユーザー アカウント名を作成しようとする場合に発生します。 2 番目にデプロイされるクラスターでは、AD で競合が発生し、そのアカウントを作成することはできません。

## <a name="resolution-for-collisions"></a>競合の解決

### <a name="solution-to-solve-the-problem-with-spns-and-dns-domain---sql-2019-cu5"></a>SPN と DNS ドメインに関する問題を解決するための解決策 - SQL 2019 CU5

2 つのクラスターで SPN は異なる必要があるため、デプロイ時に渡される DNS ドメイン名は異なる必要があります。 展開構成ファイルで新しく導入された設定 (`subdomain`) を使用して、異なる DNS 名を指定することができます。 2 つのクラスターでサブドメインが異なり、このサブドメインを介して内部通信が行われる可能性がある場合、必要な一意性を実現するサブドメインが SPN に含まれます。

>[!NOTE]
>サブドメイン設定を介して渡される値は、新しい AD ドメインではなく、内部で使用される DNS ドメインです。

引き続き、例として、マスター プールの SQL Server SPN の場合を考えてみます。 サブドメインが `bdc` である場合、前述の SPN が `MSSQLSvc/master-0.bdc.contoso.local:1433` に変わります。  

Active Directory 構成仕様で新しく導入されたサブドメイン パラメーターの値をカスタマイズすることは、省略できます。 既定では、BDC クラスター名または名前空間名は、サブドメイン設定の値を計算するために使用されます。 ユーザーがサブドメイン名をオーバーライドする場合、Active Directory 構成仕様で導入される新しいサブドメイン パラメーターを使用して行うことができます。

### <a name="solution-to-solve-the-problem-regarding-account-names-uniqueness"></a>アカウント名の一意性に関する問題を解決するためのソリューション

一意性を保証するスキームにアカウント名を更新するために、アカウント プレフィックスの概念が導入されました。 アカウント プレフィックスは、任意の 2 つのクラスター間で一意であるアカウント名の一部です。 アカウント名の残りの部分は、特定のサービスに対して一定となります。 アカウント名の新しい形式は、`<prefix>-<name>-<podId>` のようになります。 

>[!NOTE]
>Active Directory では、アカウント名を 20 文字までに制限する必要があります。 ポッドと StatefulSet を区別するために、BDC クラスターでは 8 文字を使用する必要があります。 これにより、アカウント プレフィックスの制限として 12 文字が残されます

アカウント名のカスタマイズは省略可能です。 Active Directory 構成仕様では `accountPrefix` パラメーターを使用します。SQL Server 2019 CU5 では、構成仕様に `accountPrefix` が導入されています。既定では、サブドメイン名はアカウント プレフィックスとして使用されます。 サブドメイン名が 12 文字より長い場合、サブドメイン名の最初の 12 文字の substring がアカウント プレフィックスとして使用されます。

サブドメインは DNS にのみ適用されます。 そのため、新しい LDAP ユーザー アカウント名は `bdc-ldap@contoso.local` となります。 アカウント名は `bdc-ldap@bdc.contoso.local` にはなりません。

## <a name="semantics"></a>セマンティクス

まとめると、1 つのドメイン内の複数のクラスター用に SQL 2019 CU5 で追加されたパラメーターのセマンティクスは次のとおりです。

### `subdomain`

- 省略可能なフィールド
- データ型: 文字列
- 定義:この BDC クラスターに使用する一意の DNS サブドメイン。 この値は、Active Directory ドメインにデプロイされるクラスターごとに異なる必要があります。  
- 既定値:指定されていない場合、既定値としてクラスター名が使用されます
- 最大長: 1 ラベルあたり 63 文字 (各文字列がドットで区切られたラベル)。
- 解説:エンドポイントの DNS 名の場合、FQDN でサブドメインを使用する必要があります。

### `accountPrefix`

- 省略可能なフィールド
- データ型: 文字列
- 定義: BDC クラスターによって生成される、AD アカウントの一意のプレフィックス。 この値は、Active Directory ドメインにデプロイされるクラスターごとに異なる必要があります。
- 既定値:指定されていない場合は、既定値としてサブドメイン名が使用されます。 サブドメインが指定されていない場合、クラスター名がサブドメイン名として使用されるため、クラスター名は accountPrefix としても継承されます。 サブドメインが指定されており、(1 つまたは複数のドットが含まれる) マルチパート名である場合、ユーザーは accountPrefix を指定する必要があります。 
- 最大長: 12 文字 

## <a name="impact-on-ad-domain-and-dns-server"></a>AD ドメインと DNS サーバーへの影響 

同じ Active Directory ドメインに対する複数の BDC のデプロイに対応するために、AD ドメインまたはドメイン コントローラーを変更する必要はありません。 DNS サブドメインは、外部エンドポイントの DNS 名を登録するときに、DNS サーバーに自動的に作成されます。 

## <a name="impact-on-setting-up-the-deployment-configuration-file-used-for-the-bdc-deployment"></a>BDC のデプロイに使用される展開構成ファイルの設定に対する影響 

コントロール プレーン構成 *control.json* の *activeDirectory* セクションには、`subdomain` と `accountPrefix` という 2 つの新しい省略可能なパラメーターがあります。 既定の動作 (それぞれにクラスター名を使用する) をオーバーライドする場合は、これらの設定の値のみを指定します。 クラスター名は名前空間名と同じです。

さらに、任意のエンドポイント DNS 名を使用できます。ただし、これらが完全に修飾されており、同じドメインにデプロイされた任意の 2 つのビッグ データ クラスター間で競合しない場合に限ります。 必要に応じて、サブドメインのパラメーター値を使用して、クラスター間で確実に DNS 名が異なるようにすることができます。  例として、ゲートウェイ エンドポイントについて考えてみましょう。 エンドポイントに `gateway` という名前を使用して、それを BDC のデプロイの一環として自動的に DNS サーバーに登録する場合は、DNS 名として `gateway.bdc1.contoso.local` を使用します。 `bdc1` がサブドメインで、`contoso.local` が AD DNS ドメイン名である場合があります。 使用できるその他の値は、`gateway-bdc1.contoso.local` または単に `gateway.contoso.local` です。

## <a name="examples"></a>例

サブドメインと accountPrefix をオーバーライドする場合の、Active Directory のセキュリティ構成の例を以下に示します。 

```json
    "security": { 
        "activeDirectory": { 
            "ouDistinguishedName":"OU=contosoou,DC=contoso,DC=local", 
            "dnsIpAddresses": [ "10.10.10.10" ], 
            "domainControllerFullyQualifiedDns": [ "contoso-win2016-dc.contoso.local" ], 
            "domainDnsName":"contoso.local", 
            "subdomain": "bdc", 
            "accountPrefix": "myprefix", 
            "clusterAdmins": [ "contosoadmins" ], 
            "clusterUsers": [ "contosousers1", "contosousers2" ] 
        } 
    } 
  
```

以下は、コントロール プレーン エンドポイントのエンドポイント仕様の例です。 DNS 名が一意であり、完全に修飾されている限り、それらに任意の値を使用できます。
  
```json
        "endpoints": [ 
            { 
                "serviceType": "NodePort", 
                "port": 30080, 
                "name": "Controller", 
                "dnsName": "control-bdc1.contoso.local" 
            }, 
            { 
                "serviceType": "NodePort", 
                "port": 30777, 
                "name": "ServiceProxy", 
                "dnsName": "monitor-bdc1.contoso.local" 
            } 
        ] 
  
```

## <a name="questions"></a>疑問がある場合

### <a name="do-you-need-to-create-separate-ous-for-different-clusters"></a>異なるクラスターに個別の OU を作成する必要はありますか?

必須ではありませんが、お勧めします。 個別のクラスターに個別の OU を指定すると、生成されるユーザー アカウントを管理するのに役立ちます。

### <a name="how-to-revert-back-to-the-pre-cu5-behavior-in-sql-2019"></a>SQL 2019 で CU5 より前の動作に戻すにはどうすればよいですか?

新しく導入された `subdomain` パラメーターに対応できないシナリオもあります。 たとえば、CU5 より前のリリースをデプロイする必要があり、[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] がアップグレード済みである場合です。 これは非常にまれですが、CU5 より前の動作に戻す必要がある場合は、`control.json` の Active Directory セクションで `useSubdomain` パラメーターを `false` に設定できます。

次の例では、このシナリオで `useSubdomain` を `false` に設定します。

```console
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.useSubdomain=false" 
```

## <a name="next-steps"></a>次のステップ

[SQL Server ビッグ データ クラスターの Active Directory 統合のトラブルシューティング](troubleshoot-active-directory.md)
