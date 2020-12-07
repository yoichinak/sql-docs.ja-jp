---
title: AD モード ログインに失敗しました - 信頼されていないドメイン
titleSuffix: SQL Server Big Data Cluster
description: 動作を修正する - エンドポイントの DNS エントリがエイリアス名を指す CNAME として構成されている場合、クライアントでは認証に失敗します。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 05/01/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 669d8f050c3dd86d733c33741eb6fc846245aff2
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891042"
---
# <a name="symptom-ad-mode-login-fails---untrusted-domain-big-data-clusters"></a>症状:AD モード ログインに失敗しました - 信頼されていないドメイン (ビッグ データ クラスター)

Active Directory モードの SQL Server ビッグ データ クラスター (BDC) では、接続試行に失敗する可能性があり、接続試行で次のエラーが返されます。

`Login failed. The login is from an untrusted domain and cannot be used with Integrated authentication.`

これは、トラフィックを Kubernetes ノードに分散するリバース プロキシのエイリアス名を指す CNAME として、DNS エントリを構成した場合に発生する可能性があります。

## <a name="root-cause"></a>根本原因

エンドポイントが DNS エントリで構成されており、その CNAME が Kubernetes ノードにトラフィックを分散するリバース プロキシのエイリアス名を指す場合:

- Kerberos 認証プロセスでは、CNAME のエントリと一致するサービス プリンシパル名 (SPN) を探します。これは、アクティブ ディレクトリの BDC に登録されている実際の SPN ではありません
- 認証に失敗します 

## <a name="confirm-root-cause"></a>根本原因を確認する

認証に失敗した後、Kerberos チケットのキャッシュを確認します。 

チケットのキャッシュを確認するには、`klist` コマンドを使用します。 

接続しようとしたエンドポイントに一致する SPN を持つチケットを探します。

そこに予期されるチケットはありません。

この例では、マスター エンドポイントの、`bdc-sql` DNS レコードは、CNAME が `ServerReverseProxy` という名前のリバース プロキシに設定されている CNAME です

```PowerShell
Resolve-DnsName bdc-sql
```

次のセクションでは、前のコマンドの結果を示します。

```
Name                           Type   TTL   Section    NameHost
----                           ----   ---   -------    --------
bdc-sql.mydomain.com           CNAME  3600  Answer     ReverseProxyServer.mydomain.com

Name       : ReverseProxyServer.mydomain.com
QueryType  : A
TTL        : 3600
Section    : Answer
IP4Address : 193.168.5.10
```

>[!NOTE]
>以降のセクションでは、[`tshark`](https://www.wireshark.org/docs/man-pages/tshark.html) を参照します。 `tshark` は、[Wireshark](https://www.wireshark.org/docs/) (ネットワーク トレース ユーティリティ) の一部としてインストールされたコマンド ライン ユーティリティです。

Active Directory から要求された SPN を表示するには、`tshark` を使用します。 次のコマンドでは、ネットワーク トレースのキャプチャを Kerberos プロトコル通信に制限し、`krb-error (30)` メッセージのみを表示します。 これらのメッセージには、失敗した SPN 要求メッセージが含まれているはずです。

```bash
tshark -Y "kerberos && kerberos.msg_type == 30" -T fields -e kerberos.error_code -e kerberos.SNameString
```

別のコマンド シェルから、マスター ポッドに接続してみます。

```bash
klist purge

sqlcmd -S bdc-sql.mydomain.com,31433 -E
```

次の出力例を参照してください。

```bash
klist purge

Current LogonId is 0:0xf6b58
        Deleting all tickets:
        Ticket(s) purged!

sqlcmd -S bdc-sql.mydomain.com,31433 -E
sqlcmd: Error: Microsoft ODBC Driver 17 for SQL Server : Login failed. The login is from an untrusted domain and cannot be used with Integrated authentication.
```

`tshark` 出力を確認します。 

```bash
Capturing on 'Ethernet 3'
25      krbtgt,RLAZURE.COM
7       MSSQLSvc,ReverseProxyServer.mydomain.com:31433
2 packets captured
```

クライアントで、存在しない `SPN MSSQLSvc,ReverseProxyServer.mydomain.com:31433` が要求されていることに注意してください。 接続試行は最終的にエラー 7 で失敗します。 エラー 7 は `KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN Server not found in Kerberos database` を意味します。

正しい構成では、クライアントで、BDC によって登録されている SPN が要求されます。 この例では、正しい SPN は `MSSQLSvc,bdc-sql.mydomain.com:31433` となります。

>[!NOTE]
>エラー 25 は、`KDC_ERR_PREAUTH_REQUIRED` (追加の事前認証が必要) を意味します。 これは無視してかまいません。 最初の Kerberos AD 要求に対して、`KDC_ERR_PREAUTH_REQUIRED` が返されます。 既定では、Windows Kerberos クライアントのこの最初の要求には事前認証情報が含まれません。

マスター エンドポイント用に BDC によって登録された SPN の一覧を表示するには、`setspn -L mssql-master` を実行します。 

次の出力例を参照してください。

```bash
Registered ServicePrincipalNames for CN=mssql-master,OU=bdc,DC=mydomain,DC=com:
        MSSQLSvc/bdc-sqlread.mydomain.com:31436
        MSSQLSvc/-sqlread:31436
        MSSQLSvc/bdc-sqlread.mydomain.com
        MSSQLSvc/bdc-sqlread
        MSSQLSvc/bdc-sql.mydomain.com:31433
        MSSQLSvc/bdc-sql:31433
        MSSQLSvc/bdc-sql.mydomain.com
        MSSQLSvc/bdc-sql
        MSSQLSvc/master-p-svc.mydomain.com:1533
        MSSQLSvc/master-p-svc:1533
        MSSQLSvc/master-p-svc.mydomain.com:1433
        MSSQLSvc/master-p-svc:1433
        MSSQLSvc/master-p-svc.mydomain.com
        MSSQLSvc/master-p-svc
        MSSQLSvc/master-svc.mydomain.com:1533
        MSSQLSvc/master-svc:1533
        MSSQLSvc/master-svc.mydomain.com:1433
        MSSQLSvc/master-svc:1433
        MSSQLSvc/master-svc.mydomain.com
        MSSQLSvc/master-svc
```

上記の結果では、リバース プロキシ アドレスを登録することはできません。

## <a name="resolve"></a>解決

このセクションでは、この問題を解決する 2 つの方法を示します。 適切な変更を行った後、クライアントで `ipconfig -flushdns` と `klist purge` を実行します。 その後、もう一度接続してみます。

### <a name="option-1"></a>方法 1

DNS 内の各 BDC エンドポイントの CNAME レコードを削除して、複数のマスターがある場合は各 Kubernetes ノードまたは各 Kubernetes マスターを指す複数の `A` レコードに置き換えます。

>[!TIP]
>以下で説明するスクリプトでは、PowerShell を使用します。 詳細については、「[Linux への PowerShell のインストール](/powershell/scripting/install/installing-powershell-core-on-linux)」を参照してください。

次の PowerShell スクリプトを使用して、DNS エンドポイント レコードを更新できます。 同じドメインに接続されている任意のコンピューターからスクリプトを実行します。

```powershell
#Specify the DNS server, example contoso.local
$Domain_DNS_name=mydomain.com'

#DNS records for bdc endpoints
$Controller_DNS_name = 'bdc-control'
$Managment_proxy_DNS_name= 'bdc-proxy'
$Master_Primary_DNS_name = 'bdc-sql'
$Master_Secondary_DNS_name = 'bdc-sqlread'
$Gateway_DNS_name = 'bdc-gateway'
$AppProxy_DNS_name = 'bdc-appproxy'

#Performing Endpoint DNS records Checks..

#Build array of endpoints 
$BdcEndpointsDns = New-Object System.Collections.ArrayList

[void]$BdcEndpointsDns.Add($Controller_DNS_name)
[void]$BdcEndpointsDns.Add($Managment_proxy_DNS_name)
[void]$BdcEndpointsDns.Add($Master_Primary_DNS_name)
[void]$BdcEndpointsDns.Add($Master_Secondary_DNS_name)
[void]$BdcEndpointsDns.Add($Gateway_DNS_name)
[void]$BdcEndpointsDns.Add($AppProxy_DNS_name)

#Build arrary for results 
$BdcEndpointsDns_Result = New-Object System.Collections.ArrayList

foreach ($DnsName in $BdcEndpointsDns) {
    try {
        $endpoint_DNS_record = Resolve-DnsName $DnsName -Type A -Server $Domain_DNS_IP_address -ErrorAction Stop 
        foreach ($ip in $endpoint_DNS_record.IPAddress) {
            [void]$BdcEndpointsDns_Result.Add("OK - $DnsName is an A record with an IP $ip")
        }
    }
    catch {
        [void]$BdcEndpointsDns_Result.Add("MisConfiguration - $DnsName is not an A record or does not exists")
    }  
}

#show the results 
$BdcEndpointsDns_Result
```

### <a name="option-2"></a>方法 2

リバース プロキシの名前ではなく、リバース プロキシの IP アドレスを指すように CNAME を変更することで、問題を回避することもできます。

## <a name="confirm-resolution"></a>解決策を確認する

上記のオプションのいずれかを使用する解決策が決まったら、Active Directory でビッグ データ クラスターに接続し、その解決策を確認します。

## <a name="next-steps"></a>次のステップ

[ドメイン コントローラーの逆引き DNS エントリ (PTR レコード) を検証します](active-directory-deploy.md#verify-reverse-dns-entry-for-domain-controller)。
