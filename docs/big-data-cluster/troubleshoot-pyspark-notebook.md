---
title: '`pyspark` ノートブックのトラブルシューティング'
titleSuffix: SQL Server Big Data Cluster
description: '`pyspark` ノートブックのトラブルシューティング'
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mikeray
ms.date: 06/01/2020
ms.topic: how-to
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d631a74bc71c814a70ef0ecfa33485ee4631ccd4
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257078"
---
# <a name="troubleshoot-pyspark-notebook"></a>`pyspark` ノートブックのトラブルシューティング

この記事では、失敗した `pyspark` ノートブックのトラブルシューティング方法について説明します。

## <a name="architecture-of-a-pyspark-job-under-azure-data-studio"></a>Azure Data Studio での PySpark ジョブのアーキテクチャ

Azure Data Studio は、SQL Server BDC 上の `livy` エンドポイントと通信します。 

`livy` エンドポイントから BDC クラスター内で `spark-submit` コマンドが発行されます。 各 `spark-submit` コマンドには、クラスターのリソース マネージャーとして YARN を指定するパラメーターがあります。

PySpark セッションを効率的にトラブルシューティングするには、各レイヤー内のログを収集して確認します (Livy、YARN、Spark)。

このトラブルシューティング手順では、以下が必要です。

1. [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] がインストールされ、構成がクラスターに正しく設定されていること。
2. Linux コマンドの実行に関する知識とログのトラブルシューティング スキル。

## <a name="troubleshooting-steps"></a>トラブルシューティングの手順

1. `pyspark` のスタックとエラー メッセージを確認します。

   ノートブックの最初のセルからアプリケーション ID を取得します。 このアプリケーション ID を使用して、`livy`、YARN、および Spark のログを調査します。 `SparkContext` には、この YARN アプリケーション ID が使用されます。

   :::image type="content" source="../big-data-cluster/media/troubleshoot-pyspark-notebook/1-failed-cell.png" alt-text="失敗したセル":::

1. ログを取得します。

   `azdata bdc debug copy-logs` を使用して調査します

   次の例では、ビッグ データ クラスター エンドポイントを接続してログをコピーします。 実行する前に、例の次の値を更新します。
   - `<ip_address>`:ビッグ データ クラスターのエンドポイント
   - `<username>`:ビッグ データ クラスターのユーザー名
   - `<namespace>`:クラスターの Kubernetes 名前空間
   - `<folder_to_copy_logs>`:ログをコピーする先のローカル フォルダーのパス

   ```console
   azdata login --auth basic --username <username> --endpoint https://<ip_address>:30080
   azdata bdc debug copy-logs -n <namespace> -d <folder_to_copy_logs>
   ```

   出力例

   ```output
   <user>@<server>:~$ azdata bdc debug copy-logs -n <namespace> -d copy_logs
   Collecting the logs for cluster '<namespace>'.
   Collecting logs for containers...
   Creating an archive from logs-tmp/<namespace>.
   Log files are archived in /home/<user>/copy_logs/debuglogs-<namespace>-YYYYMMDD-HHMMSS.tar.gz.
   Creating an archive from logs-tmp/dumps.
   Log files are archived in /home/<user>/copy_logs/debuglogs-<namespace>-YYYYMMDD-HHMMSS-dumps.tar.gz.
   Collecting the logs for cluster 'kube-system'.
   Collecting logs for containers...
   Creating an archive from logs-tmp/kube-system.
   Log files are archived in /home/<user>/copy_logs/debuglogs-kube-system-YYYYMMDD-HHMMSS.tar.gz.
   Creating an archive from logs-tmp/dumps.
   Log files are archived in /home/<user>/copy_logs/debuglogs-kube-system-YYYYMMDD-HHMMSS-dumps.tar.gz.
   ```

1. Livy ログを確認します。 Livy のログは `<namespace>\sparkhead-0\hadoop-livy-sparkhistory\supervisor\log` にあります。

   - pyspark ノートブックの最初のセルから YARN アプリケーション ID を検索します。
   - `ERR` 状態を検索します。
   
   状態が `YARN ACCEPTED` の Livy ログの例。 Livy から yarn アプリケーションが送信されました。

   ```output
   HH:MM:SS INFO utils.LineBufferedStream: YYY-MM-DD HH:MM:SS INFO impl.YarnClientImpl: Submitted application application_<application_id>
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream: YYY-MM-DD HH:MM:SS INFO yarn.Client: Application report for application_<application_id> (state: ACCEPTED)
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream: YYY-MM-DD HH:MM:SS INFO yarn.Client: 
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      client token: N/A
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      diagnostics: N/A
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      ApplicationMaster host: N/A
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      ApplicationMaster RPC port: -1
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      queue: default
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      start time: ############
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      final status: UNDEFINED
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      tracking URL: https://sparkhead-1.fnbm.corp:8090/proxy/application_<application_id>/
   YY/MM/DD HH:MM:SS INFO utils.LineBufferedStream:      user: <account>
   ```

1. YARN UI を確認する

   Azure Data Studio ビッグ データ クラスター管理ダッシュボードから YARN エンドポイント URL を取得するか、`azdata bdc endpoint list –o table` を実行します。

   次に例を示します。

   ```console
   azdata bdc endpoint list -o table
   ```

   戻り値

   ```output
   Description                                             Endpoint                                                          Name                        Protocol
   ------------------------------------------------------  ----------------------------------------------------------------  --------------------------  ----------
   Gateway to access HDFS files, Spark                     https://knox.<namespace-value>.local:30443                               gateway                     https
   Spark Jobs Management and Monitoring Dashboard          https://knox.<namespace-value>.local:30443/gateway/default/sparkhistory  spark-history               https
   Spark Diagnostics and Monitoring Dashboard              https://knox.<namespace-value>.local:30443/gateway/default/yarn          yarn-ui                     https
   Application Proxy                                       https://proxy.<namespace-value>.local:30778                              app-proxy                   https
   Management Proxy                                        https://bdcmon.<namespace-value>.local:30777                             mgmtproxy                   https
   Log Search Dashboard                                    https://bdcmon.<namespace-value>.local:30777/kibana                      logsui                      https
   Metrics Dashboard                                       https://bdcmon.<namespace-value>.local:30777/grafana                     metricsui                   https
   Cluster Management Service                              https://bdcctl.<namespace-value>.local:30080                             controller                  https
   SQL Server Master Instance Front-End                    sqlmaster.<namespace-value>.local,31433                                  sql-server-master           tds
   SQL Server Master Readable Secondary Replicas           sqlsecondary.<namespace-value>.local,31436                               sql-server-master-readonly  tds
   HDFS File System Proxy                                  https://knox.<namespace-value>.local:30443/gateway/default/webhdfs/v1    webhdfs                     https
   Proxy for running Spark statements, jobs, applications  https://knox.<namespace-value>.local:30443/gateway/default/livy/v1       livy                        https
   ```

1. アプリケーション ID と、個々の application_master とコンテナーのログを確認します。

   :::image type="content" source="media/troubleshoot-pyspark-notebook/15-hadoop-dashboard.png" alt-text="失敗したセル":::

1. YARN アプリケーション ログを確認します。

   アプリのアプリケーション ログを取得します。 `kubectl` を使用して `sparkhead-0` ポッドに接続します。次に例を示します。
   
   ```console
   kubectl exec -it sparkhead-0 -- /bin/bash
   ```
      
   そして、適切な `application_id` を使用して、そのシェル内でこのコマンドを実行します。

   ```console
   yarn logs -applicationId application_<application_id>
   ```

1. エラーまたはスタックを探します。

   hdfs に対するアクセス許可エラーの例。 Java スタックで `Caused by:` を探します

   ```output
   YYYY-MM-DD HH:MM:SS,MMM ERROR spark.SparkContext: Error initializing SparkContext.
   org.apache.hadoop.security.AccessControlException: Permission denied: user=<account>, access=WRITE, inode="/system/spark-events":sph:<bdc-admin>:drwxr-xr-x
        at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.check(FSPermissionChecker.java:399)
        at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:255)
        at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:193)
        at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1852)
        at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1836)
        at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkAncestorAccess(FSDirectory.java:1795)
        at org.apache.hadoop.hdfs.server.namenode.FSDirWriteFileOp.resolvePathForStartFile(FSDirWriteFileOp.java:324)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.startFileInt(FSNamesystem.java:2504)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.startFileChecked(FSNamesystem.java:2448)
   
   Caused by: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.security.AccessControlException): Permission denied: user=<account>, access=WRITE, inode="/system/spark-events":sph:<bdc-admin>:drwxr-xr-x
   ```

1. SPARK UI を確認します。

   :::image type="content" source="media/troubleshoot-pyspark-notebook/30-spark-ui.png" alt-text="失敗したセル":::

   ステージ タスクまでドリルダウンしてエラーを探します。

## <a name="next-steps"></a>次のステップ

[SQL Server ビッグ データ クラスターの Active Directory 統合のトラブルシューティング](troubleshoot-active-directory.md)