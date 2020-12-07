---
title: AD モードの展開が停止する - DC の逆引き参照ゾーン エントリが見つからない
titleSuffix: SQL Server Big Data Cluster
description: ドメイン コントローラーの DNS サーバーにドメイン コントローラーの逆引き参照ゾーン エントリが見つからないため、AD モードを使用した BDC の展開がスタックしています。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 04/21/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 63086a762e8c55109a43a32e39868b65808108f9
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257092"
---
# <a name="ad-mode-deployment-stopped---missing-reverse-lookup-zone-entry-for-dc"></a>AD モードの展開が停止する - DC の逆引き参照ゾーン エントリが見つからない

Active Directory (AD) モードの展開がフリーズします。 現象を調べて、ドメイン コントローラーの DNS サーバーに逆引き参照ゾーン エントリが見つからないことが原因かどうかを確認します。 

## <a name="symptom"></a>症状

AD モードで BDC の展開を開始しましたが、展開がスタックし、処理が進みません。

bash シェルの展開結果の例を次に示します。

```
The privacy statement can be viewed at:
https://go.microsoft.com/fwlink/?LinkId=853010
 
The license terms for SQL Server Big Data Cluster can be viewed at:
Enterprise: https://go.microsoft.com/fwlink/?linkid=2104292
Standard: https://go.microsoft.com/fwlink/?linkid=2104294
Developer: https://go.microsoft.com/fwlink/?linkid=2104079
 
Cluster deployment documentation can be viewed at:
https://aka.ms/bdc-deploy
 
NOTE: Cluster creation can take a significant amount of time depending on
configuration, network speed, and the number of nodes in the cluster.
 
Starting cluster deployment.
Cluster controller endpoint is available at bdc-control.contoso.com:30080, 193.168.5.14:30080.
Waiting for control plane to be ready after 5 minutes.
Waiting for control plane to be ready after 10 minutes.
Waiting for control plane to be ready after 15 minutes.
Waiting for control plane to be ready after 20 minutes.
Waiting for control plane to be ready after 25 minutes.
```

現在展開されているポッドを確認します。

```bash
kubectl get pods -n mssql-cluster
```

以下の結果は、コントローラーに属するポッドのみが展開されていることを示しています。 コンピューティング、データ、またはストレージのポッドが作成されていません。

```
NAME              READY   STATUS    RESTARTS   AGE
control-rts5t     3/3     Running   0          18m
controldb-0       2/2     Running   0          18m
controlwd-csgst   1/1     Running   0          16m
dns-7kfnz         2/2     Running   0          16m
logsdb-0          1/1     Running   0          16m
logsui-2pc29      1/1     Running   0          16m
metricsdb-0       1/1     Running   0          16m
metricsdc-4rtm4   1/1     Running   0          16m
metricsdc-6lr2t   1/1     Running   0          16m
metricsdc-ftx9m   1/1     Running   0          16m
metricsdc-h59jb   1/1     Running   0          16m
metricsui-lvdpt   1/1     Running   0          16m
mgmtproxy-mkmxp   2/2     Running   0          16m
```

セキュリティ サポート コンテナーのログを調べます。 LDAP エラーを探します。 

## <a name="check-security-support-container"></a>セキュリティ サポート コンテナーを確認する 

セキュリティ サポート コンテナーのログを確認します。

次のコマンドでは、名前空間 `mssql-cluster` にあるクラスターのセキュリティ サポート ログを収集します。

```bash
azdata bdc debug copy-logs -n mssql-cluster -c security-support
```

ログを抽出し、`\mssql-cluster\control-<identifier>\controller\control-rts5t-controller-stdout.log` を見つけます。

> [!TIP]
> ログを収集するには、複数の方法があります。 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] を使用してログをコピーする代わりに、Azure Data Studio でノートブックを使用できます。
> Azure Data Studio で Kubernetes クラスターに接続し、適切なトラブルシューティング ノートブックを実行します。 ノートブックの例を次に示します。
>
> - TSG027 - クラスターのデプロイを観察する
> - TSG061 - BDC 名前空間内にあるポッドのすべてのコンテナー ログの末尾を取得する
> - TSG001 - `azdata copy-logs` を実行する
>

## <a name="inspect-the-logs"></a>ログを調べる

ログを見つけます。 次の例はコントローラー展開ログを示しています。 

`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-YYYYMMDD-HHMMSS\<namespace>\control-<identifier>\controller\control-<identifier>-controller-stdout.log`"

```
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'cntrl-controller'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=cntrl-controller,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'ldap-user'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=ldap-user,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
YYYY-MM-DD HH:MM:SS.ms | ERROR | Failed to create AD user account 'nginx-mgmtproxy'. Error code: 53. Message: Failed to create user object: Failed to add object 'CN=nginx-mgmtproxy,OU=bdc, DC=CONTOSO, DC=com' to 'CONTOSO.COM': Server is unwilling to perform. 
```

## <a name="cause"></a>原因

ドメイン コントローラーの DNS エントリにドメイン コントローラーの逆引き参照ゾーン エントリが見つかりません。 

## <a name="resolution"></a>解決方法

次の PowerShell スクリプトを実行して、逆引き DNS エントリ (PTR レコード) が構成されているかどうかを確認します。

```powershell
#Domain Controller FQDN 'DCserver01.contoso.local'
$Domain_controller_FQDN = 'DCserver01.contoso.local'

#Performing Domain Controller DNS record, reverse PTR Checks...
$DcControllerDnsPtr_Result = New-Object System.Collections.ArrayList
try {
    $Domain_controller_DNS_Record = Resolve-DnsName $Domain_controller_FQDN -Type A -Server $Domain_DNS_IP_address -ErrorAction Stop
    foreach ($ip in $Domain_controller_DNS_Record.IPAddress) {
        #resolving hostname by IP address to make sure we have reverse PTR record 
        if ((Resolve-DnsName $ip).NameHost -eq $Domain_controller_FQDN) {
            [void]$DcControllerDnsPtr_Result.add("OK - $Domain_controller_FQDN has an A record with an IP $ip, Reverse PTR record is in place") 
        }
        else {
            [void]$DcControllerDnsPtr_Result.add("Missing - $Domain_controller_FQDN has an A record with an IP $ip, But no reverse PTR record was found for the host")
        }
    }
}
catch {
    [void]$DcControllerDnsPtr_Result.add("Error - " + $_.exception.message)
}

#show the results 
$DcControllerDnsPtr_Result
```

## <a name="next-steps"></a>次のステップ

[ドメイン コントローラーの逆引き DNS エントリ (PTR レコード) を検証します](active-directory-deploy.md#verify-reverse-dns-entry-for-domain-controller)。
