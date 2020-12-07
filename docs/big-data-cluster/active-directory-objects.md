---
title: Active Directory オブジェクト
titleSuffix: SQL Server Big Data Cluster
description: SQL Server ビッグ データ クラスター用に作成された Active Directory オブジェクトについて説明します。
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fcd045c07e7300478e811b2bbc4b9a0f5dfaab52
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892452"
---
# <a name="auto-generated-active-directory-objects"></a>自動的に生成される Active Directory のオブジェクト

この記事では、ビッグ データ クラスター (BDC) の展開の間に SQL Server によって作成される Active Directory (AD) のアカウントとグループについて説明します。

## <a name="accounts--groups"></a>アカウントとグループ

クラスターの展開の間に、指定した[組織単位 (OU)](/windows-server/identity/ad-ds/plan/reviewing-ou-design-concepts) にユーザー アカウントとグループが生成されます。

各アカウントは、BDC でのサービスを表します。 アカウントでは、各サービスに必要なサービス プリンシパル名 (SPN) が所有されています。 各アカウントによって所有されている SPN の一覧は、[setspn](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spn-setspn-syntax.aspx) コマンドを使用して表示できます。

アカウントとグループの名前は、展開によって自動的に生成されます。 SQL Server 2019 CU5 以降では、アカウントまたはグループの名前のプレフィックスは、展開の名前空間名 (BDC クラスター名) になります。 この記事に記載されている項目のクラスター名が `bdc` の場合、アカウントを識別するには `<prefix>` を `bdc` に置き換えます。

ポッドのサフィックス (-x) は、以下の変数ポッド ID を表します。 次の名前には、展開の間にユーザーが指定する変数プレフィックスは含まれません。

クラシック アカウント名は、SQL Server 2019 CU5 より前のバージョンを使用した展開と、セキュリティ構成で "useSubdomain" オプションを false に設定して行われた展開に適用されます。

| アカウント名またはグループ名|詳細情報|
|----|---|
|`<prefix>-ctrl`|[コントローラーのサービス アカウント](#controller-service-account)|
|`<prefix>-ngxm`|[監視サービス プロキシ サービス アカウント](#monitoring-service-proxy-service-account)|
|`<prefix>-ldap`|[LDAP 参照ユーザー](#ldap-lookup-user)|
|`<prefix>-sqc0-x/<prefix>-sqc0`|[コンピューティング プール SQL Server ユーザー](#compute-pool-sql-server-user)|
|`<prefix>-dmc0-x`|[コンピューティング プール Data Warehouse DMS ユーザー](#compute-pool-data-warehouse-dms-user)|
|`<prefix>-dec0-x`|[コンピューティング プール Data Warehouse エンジン ユーザー](#compute-pool-data-warehouse-engine-user)|
|`<prefix>-sqd0`|[データ プール SQL Server ユーザー](#data-pool-sql-server-user)|
|`<prefix>-sqs0`|[記憶域プール SQL Server ユーザー](#storage-pool-sql-server-user)|
|`<prefix>-ynt0-x`|[記憶域プール Yarn ノード マネージャー サービス ユーザー](#storage-pool-yarn-node-manager-service-user)|
|`<prefix>-htt0`|[記憶域プール HTTP サービス ユーザー](#storage-pool-http-service-user)|
|`<prefix>-hdt0`|[記憶域プール HDFS datanode サービス ユーザー](#storage-pool-hdfs-datanode-service-user)|
|`<prefix>-hdnn`|[HDFS 名前ノード サービス ユーザー](#hdfs-name-node-service-user)|
|`<prefix>-htnn`|[HDFS 名前ノード HTTP サービス ユーザー](#hdfs-name-node-http-service-user)|
|`<prefix>-kmnn-x`|[名前ノード KMS サービス ユーザー](#name-node-kms-service-user)|
|`<prefix>-jnzk-x`|[Zookeeper JournalNode サービス ユーザー](#zookeeper-journalnode-service-users)|
|`<prefix>-htzk`|[Zookeeper HTTP サービス ユーザー](#zookeeper-http-service-user)|
|`<prefix>-yrsh-x`|[Sparkhead Yarn リソース マネージャー サービス ユーザー](#sparkhead-yarn-resource-manager-service-user)|
|`<prefix>-htsh`|[Sparkhead HTTP ユーザー](#sparkhead-http-user)|
|`<prefix>-shsh-x`|[Sparkhead Spark 履歴サービス ユーザー](#sparkhead-spark-history-service-user)|
|`<prefix>-lvsh-x`|[Sparkhead Livy サービス ユーザー](#sparkhead-livy-service-user)|
|`<prefix>-hvsh-x`|[Sparkhead Hive サービス ユーザー](#sparkhead-hive-service-user)|
|`<prefix>-yns0-x`|[Spark プール Yarn ノード マネージャー サービス ユーザー](#spark-pool-yarn-node-manager-service-user)|
|`<prefix>-hts0`|[Spark プール Yarn ノード マネージャー HTTP ユーザー](#spark-pool-yarn-node-manager-http-user)|
|`<prefix>-knox-x`|[Knox ゲートウェイ ユーザー](#knox-gateway-user)|
|`<prefix>-htgw`|[Knox ゲートウェイ HTTP ユーザー](#knox-gateway-http-user)|
|`<prefix>-apst`|[アプリ セットアップ ユーザー](#app-setup-user)|
|`<prefix>-dmsvc`|[Data Warehouse DMS サービス グループ](#data-warehouse-dms-service-group)|
|`<prefix>-desvc`|[Data Warehouse エンジン サービス グループ](#data-warehouse-engine-service-group)|

次のセクションでは、各アカウントについて詳しく説明します。 グループの情報については、「[グループ](#groups)」に進んでください。

## <a name="controller-management--ldap-related-accounts"></a>コントローラー、管理、LDAP 関連のアカウント

### <a name="controller-service-account"></a>コントローラーのサービス アカウント

|Object|アカウント名|
|---|---|
|スケール セット名|`control`|
|ポッド名|`control-x`|
|コンテナー名|`controller`|
|[サービス名]|`controller`|
|アカウント名 (プレフィックスなし)| `ctrl`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-ctrl`|
|クラシック アカウント名|`ctrl-controller`|

### <a name="monitoring-service-proxy-service-account"></a>監視サービス プロキシ サービス アカウント

|Object|アカウント名|
|---|---|
|スケール セット名|`mgmtproxy`|
|ポッド名|`mgmtproxy-x`|
|コンテナー名|`service-proxy`|
|[サービス名]|`nginx`|
|アカウント (プレフィックスなし)| `ngxm`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-ngxm`|
|クラシック アカウント名|`nginx-mgmtproxy`|

### <a name="ldap-lookup-user"></a>LDAP 参照ユーザー

LDAP を使用してユーザーを検索するため、grafana および hadoop サービスによって使用されます。

|Object|アカウント名|
|---|---|
|スケール セット名|`metricsui`|
|ポッド名|`metricsui-x`|
|コンテナー名|`grafana`|
|[サービス名]|`grafana`|
|アカウント名 (プレフィックスなし)| `ldap`|
|アカウント名 (名前空間プレフィックスあり)|`<prefix>-ldap`|
|クラシック アカウント名|`ldap-user`|

## <a name="master-pool-accounts"></a>マスター プール アカウント

### <a name="master-pool-sql-server-user"></a>マスター プール SQL Server ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`master`|
|ポッド名|`master-x`|
|コンテナー名|`mssql-server`|
|[サービス名]|`mssql`|
|アカウント名 (プレフィックスなし)| `sqmp-x/sqmp`|
|アカウント名 (名前空間プレフィックスあり)|`<prefix>-sqmp-x/<prefix>-sqmp`|
|クラシック アカウント名|`mssql-master-x`|

### <a name="master-pool-data-warehouse-dms-user"></a>マスター プール Data Warehouse DMS ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`master`|
|ポッド名|`master-x`|
|コンテナー名|`mssql-server`|
|[サービス名]|`dwdms`|
|アカウント (プレフィックスなし)| `dmmp-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-dmmp-x`|
|クラシック アカウント名|`dwdms-master-x`|

### <a name="master-pool-data-warehouse-engine-user"></a>マスター プール Data Warehouse エンジン ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`master`|
|ポッド名|`master-x`|
|コンテナー名|`mssql-server`|
|[サービス名]|`dweng`|
|アカウント (プレフィックスなし)| `demp`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-demp-x`|
|クラシック アカウント名|`dweng-master-x`|

## <a name="compute-pool-accounts"></a>コンピューティング プール アカウント

### <a name="compute-pool-sql-server-user"></a>コンピューティング プール SQL Server ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`compute-0`|
|ポッド名|`compute-0-x`|
|コンテナー名|`mssql-server`|
|[サービス名]|`mssql`|
|アカウント (プレフィックスなし)| `sqc0-x/sqlc0`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-sqc0-x/<prefix>-sqc0`|
|クラシック アカウント名|`mssql-compute-0-x`|

### <a name="compute-pool-data-warehouse-dms-user"></a>コンピューティング プール Data Warehouse DMS ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`compute-0`|
|ポッド名|`compute-0-x`|
|コンテナー名|`mssql-server`|
|[サービス名]|`dwdms`|
|アカウント (プレフィックスなし)| `dmc0-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-dmc0-x`|
|クラシック アカウント名|`dwdms-compute-0-x`|

### <a name="compute-pool-data-warehouse-engine-user"></a>コンピューティング プール Data Warehouse エンジン ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`compute-0`|
|ポッド名|`compute-0-x`|
|コンテナー名|`mssql-server`|
|[サービス名]|`dweng`|
|アカウント (プレフィックスなし)| `dec0-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-dec0-x`|
|クラシック アカウント名|`dweng-compute-0-x`|

## <a name="data-pool-accounts"></a>データ プール アカウント

### <a name="data-pool-sql-server-user"></a>データ プール SQL Server ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`data-0`|
|ポッド名|`data-0-x`|
|コンテナー名|`mssql-server`|
|[サービス名]|`mssql`|
|アカウント (プレフィックスなし)| `sqd0`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-sqd0`|
|クラシック アカウント名|`mssql-data-0`|

## <a name="storage-pool-accounts"></a>記憶域プール アカウント

### <a name="storage-pool-sql-server-user"></a>記憶域プール SQL Server ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`storage-0`|
|ポッド名|`storage-0-x`|
|コンテナー名|`mssql-server`|
|[サービス名]|`mssql`|
|アカウント (プレフィックスなし)| `sqs0`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-sqs0`|
|クラシック アカウント名|`mssql-storage-0`|

### <a name="storage-pool-yarn-node-manager-service-user"></a>記憶域プール Yarn ノード マネージャー サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`storage-0`|
|ポッド名|`storage-0-x`|
|コンテナー名|`hadoop`|
|[サービス名]|`Yarn Node Manager`|
|アカウント (プレフィックスなし)| `ynt0-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-ynt0-x`|
|クラシック アカウント名|`yarnnm-storage-0-x`|

### <a name="storage-pool-http-service-user"></a>記憶域プール HTTP サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`storage-0`|
|ポッド名|`storage-0-x`|
|コンテナー名|`hadoop`|
|[サービス名]|`HDFS Datanode`|
|アカウント (プレフィックスなし)| `hdt0`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-hdt0`|
|クラシック アカウント名|`http-storage-0`|

### <a name="storage-pool-hdfs-datanode-service-user"></a>記憶域プール HDFS datanode サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`storage-0`|
|ポッド名|`storage-0-x`|
|コンテナー名|`hadoop`|
|[サービス名]|`HDFS Datanode`|
|アカウント (プレフィックスなし)| `hdt0`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-hdt0`|
|クラシック アカウント名|`hdfsdn-storage-0`|

## <a name="hdfs-accounts"></a>HDFS アカウント

### <a name="hdfs-name-node-service-user"></a>HDFS 名前ノード サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`nmnode-0`|
|ポッド名|`nmnode-0-x`|
|コンテナー名|`hadoop`|
|[サービス名]|`HDFS Namenode`|
|アカウント (プレフィックスなし)| `hdnn`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-hdnn`|
|クラシック アカウント名|`hdfsnn-nmnode`|

### <a name="hdfs-name-node-http-service-user"></a>HDFS 名前ノード HTTP サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`nmnode-0`|
|ポッド名|`nmnode-0-x`|
|コンテナー名|`hadoop`|
|[サービス名]|`HDFS Namenode`|
|アカウント (プレフィックスなし)| `htnn`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-htnn`|
|クラシック アカウント名|`http-nmnode`|

## <a name="kms-accounts"></a>KMS アカウント

### <a name="name-node-kms-service-user"></a>名前ノード KMS サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`nmnode-0`|
|ポッド名|`nmnode-0-x`|
|コンテナー名|`hadoop`|
|[サービス名]|`KMS`|
|アカウント (プレフィックスなし)| `kmnn-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-kmnn-x`|
|クラシック アカウント名|`kms-nmnode-x`|

## <a name="zookeeper-accounts"></a>Zookeeper アカウント

### <a name="zookeeper-journalnode-service-users"></a>Zookeeper JournalNode サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`zookeeper`|
|ポッド名|`zookeeper-x`|
|コンテナー名|`zookeeper`|
|[サービス名]|`Journal node`|
|アカウント (プレフィックスなし)| `jnzk-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-jnzk-x`|
|クラシック アカウント名|`jn-zookeeper-x`|

### <a name="zookeeper-http-service-user"></a>Zookeeper HTTP サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`zookeeper`|
|ポッド名|`zookeeper-x`|
|コンテナー名|`zookeeper`|
|[サービス名]|`Zookeeper`|
|アカウント (プレフィックスなし)| `htzk`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-htzk`|
|クラシック アカウント名|`http-zookeeper`|

## <a name="spark-related-accounts"></a>Spark 関連アカウント

### <a name="sparkhead-yarn-resource-manager-service-user"></a>Sparkhead Yarn リソース マネージャー サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`sparkhead`|
|ポッド名|`sparkhead-x`|
|コンテナー名|`hadoop-yarn-jobhistory`|
|[サービス名]|`Yarn Resource Manager`|
|アカウント (プレフィックスなし)| `yrsh-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-yrsh-x`|
|クラシック アカウント名|`yarnrm-sparkhead-x`|

### <a name="sparkhead-http-user"></a>Sparkhead HTTP ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`sparkhead`|
|ポッド名|`sparkhead-x`|
|コンテナー名|`*`|
|[サービス名]|`*`|
|アカウント (プレフィックスなし)| `htsh`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-htsh`|
|クラシック アカウント名|`http-sparkhead`|

### <a name="sparkhead-spark-history-service-user"></a>Sparkhead Spark 履歴サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`sparkhead`|
|ポッド名|`sparkhead-x`|
|コンテナー名|`hadoop-livy-sparkhistory`|
|[サービス名]|`Spark History Server`|
|アカウント (プレフィックスなし)| `shsh-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-shsh-x`|
|クラシック アカウント名|`sph-sparkhead-x`|

### <a name="sparkhead-livy-service-user"></a>Sparkhead Livy サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`sparkhead`|
|ポッド名|`sparkhead-x`|
|コンテナー名|`hadoop-livy-sparkhistory`|
|[サービス名]|`Livy`|
|アカウント (プレフィックスなし)| `lvsh-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-lvsh-x`|
|クラシック アカウント名|`livy-sparkhead-x`|

### <a name="sparkhead-hive-service-user"></a>Sparkhead Hive サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`sparkhead`|
|ポッド名|`sparkhead-x`|
|コンテナー名|`hadoop-hivemetastore`|
|[サービス名]|`Hive Metastore`|
|アカウント (プレフィックスなし)| `hvsh-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-hvsh-x`|
|クラシック アカウント名|`hive-sparkhead-x`|

### <a name="spark-pool-yarn-node-manager-service-user"></a>Spark プール Yarn ノード マネージャー サービス ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`spark-0`|
|ポッド名|`spark-0-x`|
|コンテナー名|`hadoop`|
|[サービス名]|`Yarn Node Manager`|
|アカウント (プレフィックスなし)| `yns0-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-yns0-x`|
|クラシック アカウント名|`yarnnm-spark-0-x`|

### <a name="spark-pool-yarn-node-manager-http-user"></a>Spark プール Yarn ノード マネージャー HTTP ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`spark-0`|
|ポッド名|`spark-0-x`|
|コンテナー名|`hadoop`|
|[サービス名]|`Yarn Node Manager`|
|アカウント (プレフィックスなし)| `hts0`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-hts0`|
|クラシック アカウント名|`http-spark-0`|

## <a name="knox-accounts"></a>Knox アカウント

### <a name="knox-gateway-user"></a>Knox ゲートウェイ ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`gateway`|
|ポッド名|`gateway-x`|
|コンテナー名|`knox`|
|[サービス名]|`Knox`|
|アカウント (プレフィックスなし)| `knox-x`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-knox-x`|
|クラシック アカウント名|`knox-gateway-x`|

### <a name="knox-gateway-http-user"></a>Knox ゲートウェイ HTTP ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`gateway`|
|ポッド名|`gateway-x`|
|コンテナー名|`knox`|
|[サービス名]|`Knox`|
|アカウント (プレフィックスなし)| `htgw`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-htgw`|
|クラシック アカウント名|`http-gateway`|

## <a name="app-accounts"></a>アプリ アカウント

### <a name="app-setup-user"></a>アプリ セットアップ ユーザー

|Object|アカウント名|
|---|---|
|スケール セット名|`appproxy`|
|ポッド名|`appproxy-x`|
|コンテナー名|`App Service Proxy`|
|[サービス名]|`nginx`|
|アカウント (プレフィックスなし)| `apst`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-apst`|
|クラシック アカウント名|`app-setup`|

## <a name="groups"></a>グループ

次のグループは、ユーザーによって提供された OU に作成されます。 グループのメンバーは、対応するサービスに対して上で作成されたユーザーです。

### <a name="data-warehouse-dms-service-group"></a>Data Warehouse DMS サービス グループ

|Object|グループ名|
|---|---|
|スケール セット名|`master/compute-0`|
|ポッド名|`master-x/compute-0-x`|
|コンテナー名|`mssql-server`|
|[サービス名]|`dwdms`|
|グループ (プレフィックスなし)| `dmsvc`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-dmsvc`|
|クラシック アカウント名|`dwdms-service`|

### <a name="data-warehouse-engine-service-group"></a>Data Warehouse エンジン サービス グループ

|Object|グループ名|
|---|---|
|スケール セット名|`master/compute-0`|
|ポッド名|`master-x/compute-0-x`|
|コンテナー名|`mssql-server`|
|[サービス名]|`dweng`|
|グループ (プレフィックスなし)| `desvc`|
|アカウント (名前空間プレフィックスあり)|`<prefix>-desvc`|
|クラシック アカウント名|`desvc`|

## <a name="next-steps"></a>次のステップ

[Active Directory モードで [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を展開する](active-directory-deploy.md)

[同じ Active Directory ドメインに複数の [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]を展開する](active-directory-deployment-background.md)
