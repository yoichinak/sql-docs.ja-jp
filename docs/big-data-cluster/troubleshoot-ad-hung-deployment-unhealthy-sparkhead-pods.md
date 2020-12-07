---
title: AD モードの展開がハングする - 異常な `sparkhead` ポッド
titleSuffix: SQL Server Big Data Cluster
description: 異常な `sparkhead` ポッドにより、Active Directory ドメインの SQL Server ビッグ データ クラスターの展開が応答しないことに対するトラブルシューティング。
author: macarv-ms
ms.author: macarv
ms.reviewer: mikeray
ms.date: 08/20/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e23d45f9083e8acf1f8e889cda845b36eef087ee
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364504"
---
# <a name="ad-mode-deployment-hangs---unhealthy-sparkhead-pods"></a>AD モードの展開がハングする - 異常な `sparkhead` ポッド

Active Directory (AD) モードの展開がフリーズします。 症状を確認して、クラスター ノードの異なるネットワーク上にドメイン コントローラーの逆引き参照ゾーン エントリが見つからないことが原因であるかどうかを確認します。

## <a name="symptom"></a>症状

AD モードで BDC の展開を開始しましたが、展開がスタックし、処理が進みません。

bash シェルの展開結果の例を次に示します。

```output
Starting cluster deployment.
Waiting for cluster controller to start.
Waiting for cluster controller to start.
Waiting for cluster controller to start.
Waiting for cluster controller to start.
Waiting for cluster controller to start.
Cluster controller endpoint is available at bdc-control.corpnet.contoso.com:30080, 10.166.6.77:30080.
Waiting for control plane to be ready after 5 minutes.
Cluster control plane is ready.
Cluster is not ready after 15 minutes. Check controller logs for more details.
Data pool is ready.
Storage pool is ready.
Compute pool is ready.
Master pool is ready.
Cluster is not ready after 30 minutes. Check controller logs for more details.
...
...
```

現在展開されているポッドを確認します。

```bash
kubectl get pods -n mssql-cluster
```

結果には、すべてのポッドが展開されていることが示されていますが、展開が成功したことが報告されていません。

```output
NAME              READY   STATUS    RESTARTS   AGE 
appproxy-c7f2l    2/2     Running   0          3d13h 
compute-0-0       3/3     Running   0          3d13h 
control-88dgt     3/3     Running   0          3d13h 
controldb-0       2/2     Running   0          3d13h 
controlwd-zzkxz   1/1     Running   0          3d13h 
data-0-0          3/3     Running   0          3d13h 
data-0-1          3/3     Running   0          3d13h 
dns-xkdhh         2/2     Running   0          3d13h 
gateway-0         2/2     Running   0          3d13h 
logsdb-0          1/1     Running   0          3d13h 
logsui-qz8qq      1/1     Running   0          3d13h 
master-0          4/4     Running   0          3d13h 
master-1          4/4     Running   0          3d13h 
master-2          4/4     Running   0          3d13h 
metricsdb-0       1/1     Running   0          3d13h 
metricsdc-xezf7   1/1     Running   0          3d13h 
metricsdc-qdjkh   1/1     Running   0          3d13h 
metricsui-mr34w   1/1     Running   0          3d13h 
mgmtproxy-kz5gg   2/2     Running   0          3d13h 
nmnode-0-0        2/2     Running   1          3d13h 
nmnode-0-1        2/2     Running   0          3d13h 
operator-42ffv    1/1     Running   0          3d13h 
sparkhead-0       4/4     Running   0          3d13h 
sparkhead-1       4/4     Running   0          3d13h 
storage-0-0       4/4     Running   0          3d13h 
storage-0-1       4/4     Running   0          3d13h 
storage-0-2       4/4     Running   0          3d13h 
zookeeper-0       2/2     Running   0          3d13h 
zookeeper-1       2/2     Running   0          3d13h 
zookeeper-2       2/2     Running   0          3d13h 
```

HDFS および Spark のサービスの正常性を検査します。 `sparkhead` ポッド エラーを探します。

## <a name="check-the-hdfs-and-spark-services"></a>HDFS および Spark のサービスを確認する 

Azure Data Studio (ADS) からコントローラーに接続し、ビッグ データ クラスター ダッシュボードを表示します。 HDFS と Spark の両方のサービスに異常な `sparkhead` ポッドがあるかどうかを確認します。

![HDFS Spark サービスの異常な ' sparkhead ' ポッド](./media/troubleshoot-ad-hung-deployment-unhealthy-sparkhead-pods/hdfs_spark_unhealthy_sparkhead_pods.png)

ログを抽出して見つけます。

`\mssql-cluster\control-<identifier>\controller\control-<identifier>-controller-stdout.log`.

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

`<folderOfDebugCopyLog>\debuglogs-mssql-cluster-YYYYMMDD-HHMMSS\<namespace>\control-<identifier>\controller\control-<identifier>-controller-stdout.log`

```output
StatefulSet sparkhead is not healthy: 
{{Pod sparkhead-0 is unhealthy: 
{Container hadoop-yarn-jobhistory is unhealthy: 
{Found error properties: 
{Property: jobhistoryserver.readiness, Details: 'Health module returned error state. error: Head https://sparkhead-0.corpnet.contoso.com:19888/ws/v1/history: dial tcp 10.244.2.33:19888: connect: connection refused'}}} 
{Container hadoop-livy-sparkhistory is unhealthy: 
{Found error properties: 
{Property: sparkhistory.readiness, Details: 'Health module returned error state. error: Head https://sparkhead-0.corpnet.contoso.com:18480: dial tcp 10.244.2.33:18480: connect: connection refused'}}}, 
{Container hadoop-hivemetastore is unhealthy: 
{Found error properties: 
{Property: hivemetastorehttp.readiness, Details: 'Health module returned error state. error: Post https://sparkhead-0.corpnet.contoso.com:9084/api/hms: dial tcp 10.244.2.33:9084: connect: connection refused'}}}}}, 
  
{{Pod sparkhead-1 is unhealthy: 
{Container hadoop-yarn-jobhistory is unhealthy: 
{Found error properties: 
{Property: jobhistoryserver.readiness, Details: 'Health module returned error state. error: Head https://sparkhead-1.corpnet.contoso.com:19888/ws/v1/history: dial tcp 10.244.1.24:19888: connect: connection refused'}}}, 
{Container hadoop-livy-sparkhistory is unhealthy: 
{Found error properties: 
{Property: sparkhistory.readiness, Details: 'Health module returned error state. error: Head https://sparkhead-1.corpnet.contoso.com:18480: dial tcp 10.244.1.24:18480: connect: connection refused'}}}, 
{Container hadoop-hivemetastore is unhealthy: 
{Found error properties: 
{Property: hivemetastorehttp.readiness, Details: 'Health module returned error state. error: Post https://sparkhead-1.corpnet.contoso.com:9084/api/hms: dial tcp 10.244.1.24:9084: connect: connection refused'}}}}} 
```

コンテナー ログに注意して、`sparkhead` ポッドを調べます。 この例では、`sparkhead-0` を確認します。

```output
sparkhead-0\hadoop-hivemetastore\supervisor\log\hivemetastorehttp-stderr---supervisor-pZ1gdb 
  
YYYY-MM-DD HH:MM:SS.ms INFO retry.RetryInvocationHandler: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.ipc.StandbyException): Operation category READ is not supported in state standby. Visit https://s.apache.org/sbnn-error 
at org.apache.hadoop.hdfs.server.namenode.ha.StandbyState.checkOperation(StandbyState.java:98) 
at org.apache.hadoop.hdfs.server.namenode.NameNode$NameNodeHAContext.checkOperation(NameNode.java:1998) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkOperation(FSNamesystem.java:1502) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getFileInfo(FSNamesystem.java:3227) 
at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.getFileInfo(NameNodeRpcServer.java:1158) 
at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.getFileInfo(ClientNamenodeProtocolServerSideTranslatorPB.java:983) 
at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java) 
at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:527) 
at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:1036) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:978) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:906) 
at java.security.AccessController.doPrivileged(Native Method) 
at javax.security.auth.Subject.doAs(Subject.java:422) 
at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1729) 
at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2876) 
, while invoking ClientNamenodeProtocolTranslatorPB.getFileInfo over nmnode-0-0.corpnet.contoso.com/10.244.2.36:9000 after 8 failover attempts. Trying to failover after sleeping for 13518ms. 
  
sparkhead-0\hadoop-yarn-jobhistory\supervisor\log\jobhistoryserver-stderr---supervisor-GvebR8 
  
YYYY-MM-DD HH:MM:SS.ms INFO retry.RetryInvocationHandler: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.ipc.StandbyException): Operation category READ is not supported in state standby. Visit https://s.apache.org/sbnn-error 
at org.apache.hadoop.hdfs.server.namenode.ha.StandbyState.checkOperation(StandbyState.java:98) 
at org.apache.hadoop.hdfs.server.namenode.NameNode$NameNodeHAContext.checkOperation(NameNode.java:1998) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkOperation(FSNamesystem.java:1502) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getFileInfo(FSNamesystem.java:3227) 
at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.getFileInfo(NameNodeRpcServer.java:1158) 
at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.getFileInfo(ClientNamenodeProtocolServerSideTranslatorPB.java:983) 
at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java) 
at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:527) 
at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:1036) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:978) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:906) 
at java.security.AccessController.doPrivileged(Native Method) 
at javax.security.auth.Subject.doAs(Subject.java:422) 
at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1729) 
at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2876) 
, while invoking ClientNamenodeProtocolTranslatorPB.getFileInfo over nmnode-0-1.corpnet.contoso.com/10.244.1.30:9000 after 5 failover attempts. Trying to failover after sleeping for 11416ms. 
  
sparkhead-0\hadoop-livy-sparkhistory\supervisor\log\livy-stderr---supervisor-XiHB1w 
  
YYYY-MM-DD HH:MM:SS.ms INFO retry.RetryInvocationHandler: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.ipc.StandbyException): Operation category READ is not supported in state standby. Visit https://s.apache.org/sbnn-error 
at org.apache.hadoop.hdfs.server.namenode.ha.StandbyState.checkOperation(StandbyState.java:98) 
at org.apache.hadoop.hdfs.server.namenode.NameNode$NameNodeHAContext.checkOperation(NameNode.java:1998) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkOperation(FSNamesystem.java:1502) 
at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getFileInfo(FSNamesystem.java:3227) 
at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.getFileInfo(NameNodeRpcServer.java:1158) 
at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.getFileInfo(ClientNamenodeProtocolServerSideTranslatorPB.java:983) 
at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java) 
at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:527) 
at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:1036) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:978) 
at org.apache.hadoop.ipc.Server$RpcCall.run(Server.java:906) 
at java.security.AccessController.doPrivileged(Native Method) 
at javax.security.auth.Subject.doAs(Subject.java:422) 
at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1729) 
at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2876) 
, while invoking ClientNamenodeProtocolTranslatorPB.getFileInfo over nmnode-0-1.corpnet.contoso.com/10.244.1.30:9000 after 1 failover attempts. Trying to failover after sleeping for 1401ms. 
```

## <a name="cause"></a>原因

Kubernetes ネットワークの DC の DNS サーバーにドメイン コントローラーの逆引き参照ゾーン エントリが見つかりません。 この例では、見つからないエントリは `cni0 10.244` でした。 `sparkhead` ポッド コンテナーが IP アドレス 10.244.1.30: 9000 を使用して nnnode-0-1 に到達しようとしましたが、DNS がそれを解決できませんでした。

:::image type="content" source="media/troubleshoot-ad-hung-deployment-unhealthy-sparkhead-pods/missing_reverse_lookup_zone_entry_for_domain_controller.png" alt-text="ドメイン コントローラーの逆引き参照ゾーン エントリが見つからない":::

## <a name="resolution"></a>解像度

ログで参照されているゾーンに対して、見つからない逆引き DNS エントリ (PTR レコード) を追加します。 この例では、244.10 を追加しました。

:::image type="content" source="media/troubleshoot-ad-hung-deployment-unhealthy-sparkhead-pods/missing_reverse_lookup_zone_entry_for_domain_controller_add.png" alt-text="ドメイン コントローラーの見つからない逆引き参照ゾーン エントリを追加する":::

> [!NOTE]
> クラスター ノードのすべての異なるネットワークの DNS サーバーに、ドメイン コントローラー自体の逆引き DNS エントリ (PTR レコード) が登録されていることを確認します。

## <a name="next-steps"></a>次のステップ

[ドメイン コントローラーの逆引き DNS エントリ (PTR レコード) を検証します](deploy-active-directory.md#verify-reverse-dns-entry-for-domain-controller)。