---
title: Active Directory ドメイン グループ スコープのトラブルシューティング
titleSuffix: SQL Server Big Data Cluster
description: Active Directory ドメインの SQL Server ビッグ データ クラスターの展開に関するトラブルシューティングを行います。
author: rl-msft
ms.author: rafidl
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 269e886708ec82211a4e29ac8b1e492d9f69cc98
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891072"
---
# <a name="troubleshoot-sql-server-big-data-cluster-active-directory-integration"></a>SQL Server ビッグ データ クラスターの Active Directory 統合のトラブルシューティング

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

この記事では、Active Directory モードでの SQL Server ビッグ データ クラスターの展開に関するトラブルシューティングについて説明します。

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

次の一覧は、コントローラーに属するポッドのみが展開されていることを示しています。 コンピューティング、データ、またはストレージ プール ポッドは作成されていません。

```
NAME              READY   STATUS    RESTARTS   AGE
appproxy-6q4rm    2/2     Running   0          32m
compute-0-0       3/3     Running   0          32m
control-n8jqh     3/3     Running   0          35m
controldb-0       2/2     Running   0          35m
controlwd-fgpj8   1/1     Running   0          34m
data-0-0          3/3     Running   0          32m
data-0-1          3/3     Running   0          32m
dns-fjp7n         2/2     Running   0          34m
gateway-0         2/2     Running   0          32m
logsdb-0          1/1     Running   0          34m
logsui-d26c5      1/1     Running   0          34m
master-0          3/4     Running   0          32m
master-1          3/4     Running   0          32m
master-2          3/4     Running   0          32m
metricsdb-0       1/1     Running   0          34m
metricsdc-c2kbh   1/1     Running   0          34m
metricsdc-lmqzx   1/1     Running   0          34m
metricsdc-r6499   1/1     Running   0          34m
metricsdc-tj99w   1/1     Running   0          34m
metricsui-dg8rz   1/1     Running   0          34m
mgmtproxy-dvzpc   2/2     Running   0          34m
nmnode-0-0        2/2     Running   0          32m
nmnode-0-1        2/2     Running   0          32m
operator-27gt9    1/1     Running   0          32m
sparkhead-0       4/4     Running   0          31m
sparkhead-1       4/4     Running   0          31m
storage-0-0       4/4     Running   0          31m
storage-0-1       4/4     Running   0          31m
storage-0-2       4/4     Running   0          31m
zookeeper-0       2/2     Running   0          32m
zookeeper-1       2/2     Running   0          32m
zookeeper-2       2/2     Running   0          32m
```

### <a name="check-logs"></a>ログを確認する

コンピューティング、データ、またはストレージ ポッドを作成せずに展開が終了する理由を特定するには、次のログを確認します。 

- `controller.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\control-<suffix>\controller\controller\<date>\controller.log`) を確認します。 次のエントリを探します。

  `WARN | StatefulSet master is not ready with 0 ready pods and 3 unready pods `

- `master-0` `provisioner.log` (`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-20200219-093941\mssql-cluster\master-0\mssql-server\provisioner\provisioner.log`) を確認します。

  ```
  ERROR | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
    Traceback (most recent call last):
      File "/opt/provisioner/bin/scripts/provisioningpool.py", line 214, in executeNonQueries
        connection.execute_non_query(command)
      File "src/_mssql.pyx", line 1033, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1061, in _mssql.MSSQLConnection.execute_non_query
      File "src/_mssql.pyx", line 1634, in _mssql.check_and_raise
      File "src/_mssql.pyx", line 1683, in _mssql.maybe_raise_MSSQLDatabaseException
    _mssql.MSSQLDatabaseException: (15401, b"Windows NT user or group '<domain>.<top-level-domain>\\<domain-group>' not found. Check the name again.DB-Lib error message 20018, severity 16:\nGeneral SQL Server error: Check messages from the SQL Server\n")
  WARNING | [3/3] Provisioning exception occurred during provisioning step: ProvisioningMasterPool.
  WARNING | Failed to create sql login for domain user [<domain>.<top-level-domain>\<domain-group>]
  WARNING | Retrying.
  ```

## <a name="cause"></a>原因

上の例では、ドメイン グループのスコープがドメイン ローカルなので、ドメイン ユーザーのログインが作成されずに展開は失敗します。 スコープがグローバルまたはユニバーサルのグループを使用します。 「[Active Directory モードで [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を展開する](active-directory-deploy.md)」では、AD グループのスコープ要件について説明されています。

## <a name="verify"></a>確認

ドメイン グループのスコープ (<`domain-group`>) を確認します。 [get-adgroup](/powershell/module/addsadministration/get-adgroup/) を使用します。

`<domain-group>` グループのスコープがドメイン ローカル (`DomainLocal`) の場合、展開は失敗します。 

次の PowerShell スクリプトでは、`bdcadmins` および `bdcusers` という名前の 2 つの AD グループのスコープを確認します。 名前をグループの名前に置き換えます。 

```powershell
#Administrators and users AD groups
$Cluster_admins_group='bdcadmins'
$Cluster_users_group='bdcusers'

#Performing AD Group Checks...

#AD admin group Check
$ClusterAdminGroupScope_Result = New-Object System.Collections.ArrayList
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_admins_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterAdminGroupScope_Result.Add("Misconfiguration - $Cluster_admins_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal") 
    }
    else {
        [void]$ClusterAdminGroupScope_Result.Add("OK - $Cluster_admins_group Group scope is $GroupScope")
    }
}
catch {
    [void]$ClusterAdminGroupScope_Result.Add("Error - " + $_.exception.message)
}
#Ad users group check
$ClusterUsersGroupScope_Result = New-Object System.Collections.ArrayList
$GroupScope = ''
try {
    $GroupScope = Get-ADgroup -Identity $Cluster_users_group | Select-Object -ExpandProperty GroupScope
    
    if ($GroupScope -eq 'DomainLocal') {
        [void]$ClusterUsersGroupScope_Result.Add("Misconfiguration - $Cluster_users_group Group scope is $GroupScope, this scope is not supported, Please change group scope to either Global or Univesal")
    } 
    else 
    { [void]$ClusterUsersGroupScope_Result.Add("OK - $Cluster_users_group Group scope is $GroupScope") }
}
catch {
    [void]$ClusterUsersGroupScope_Result.Add("Error - " + $_.exception.message)
}

#Display the results
$ClusterUsersGroupScope_Result
```

## <a name="resolution"></a>解決方法

この問題を解決するには、ユニバーサル スコープまたはグローバル スコープで AD グループを作成し、展開を再実行します。

