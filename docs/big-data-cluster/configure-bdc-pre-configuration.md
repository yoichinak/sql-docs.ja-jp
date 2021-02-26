---
title: SQL Server ビッグ データ クラスター構成 CU9 以前
titleSuffix: SQL Server big data clusters
description: ビッグ データ クラスター構成 CU9 以前
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 02/11/2021
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b00ed57288d19f08555a00eec8c9e62edc0f8cf6
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100343976"
---
# <a name="configure-a-sql-server-big-data-cluster---pre-cu9-release"></a>SQL Server ビッグ データ クラスターを構成する - CU9 リリース以前

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

> [!NOTE]
> CU9 リリースより前の構成対応クラスターのサポートでは、ビッグ データ クラスターは展開時にのみ構成できました。ただし、SQL Server マスター インスタンスは例外であり、mssql-conf を使用した場合のみ、展開後に構成できました。 BDC の CU9 以降のリリースを構成する手順については、[こちら](configure-bdc-overview.md)を参照してください。


BDC の CU8 以前のリリースでは、展開 `bdc.json` ファイルを利用し、展開時に BDC 設定を構成できます。 SQL Server マスター インスタンスは、mssql-conf を使用した場合のみ、展開後に構成できます。

## <a name="configuration-scopes"></a>構成スコープ
CU9 以前のビッグ データ クラスターの構成には、`service` と `resource` という 2 つのスコープ レベルがあります。 設定の階層も、この順序に従って、上位から下位に適用されます。 BDC コンポーネントでは、最下位のスコープで定義された設定の値が使用されます。 特定のスコープで設定が定義されていない場合は、上位の親スコープから値が継承されます。

たとえば、記憶域プールと `Sparkhead` リソースで Spark ドライバーによって利用されるコアの既定数を定義することがあります。 次の 2 つの方法で行います。

* `Spark` サービス スコープで既定のコア値を指定する 
* `storage-0` と `sparkhead` リソース スコープで既定のコア値を指定する

最初のシナリオでは、Spark サービス (記憶域プールと `Sparkhead`) のすべての下位スコープ リソースに、Spark サービスの既定値から既定のコア数が "*継承*" されます。

2 番目のシナリオでは、該当するスコープで定義された値が各リソースで使用されます。

既定の数のコアがサービスとリソースの両方のスコープで構成されている場合、リソースをスコープとする値によってサービスをスコープとする値が上書きされます。これは、特定の設定に対して **ユーザーが構成する** 最下位のスコープであるためです。

構成に関する具体的な情報については、関連記事を参照してください。

## <a name="configure-the-sql-server-master-instance"></a>SQL Server マスター インスタンスを構成する
[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] のマスター インスタンスを構成します。

展開時に SQL Server マスター インスタンスのサーバー構成設定を構成することはできません。 この記事では、SQL Server のエディションなどの設定を構成する方法、SQL Server エージェントを有効または無効にする方法、特定のトレース フラグを有効にする方法、カスタマー フィードバックを有効/無効にする方法に関する一時的な回避策について説明します。

これらのいずれかの設定を変更するには、次の手順に従います。

1. ターゲット設定を含むカスタム `mssql-custom.conf` ファイルを作成します。 次の例では、SQL エージェント、テレメトリを有効にし、Enterprise Edition の PID を設定し、トレース フラグ 1204 を有効にします。

   ```
   [sqlagent]
   enabled=true
   
   [telemetry]
   customerfeedback=true
   userRequestedLocalAuditDirectory = /tmp/audit

   [DEFAULT]
   pid = Enterprise

   [traceflag]
   traceflag0 = 1204
   ```

1. `mssql-custom.conf` ファイルを `master-0` ポッドの `mssql-server` コンテナー内の `/var/opt/mssql` にコピーします。 `<namespaceName>` をビッグ データ クラスター名に置き換えます。

   ```bash
   kubectl cp mssql-custom.conf master-0:/var/opt/mssql/mssql-custom.conf -c mssql-server -n <namespaceName>
   ```

1. SQL Server インスタンスを再起動します。  `<namespaceName>` をビッグ データ クラスター名に置き換えます。

   ```bash
   kubectl exec -it master-0  -c mssql-server -n <namespaceName> -- /bin/bash
   supervisorctl restart mssql-server
   exit
   ```

> [!IMPORTANT]
> SQL Server マスター インスタンスが可用性グループ構成内にある場合は、すべての `master` ポッドに `mssql-custom.conf` ファイルをコピーします。 再起動のたびにフェールオーバーが発生するので、このアクティビティのタイミングをダウンタイム期間中にする必要があることに注意してください。

### <a name="known-limitations"></a>既知の制限事項

- 上記の手順では、Kubernetes クラスター管理者のアクセス許可が必要です
- 展開後に、ビッグ データ クラスターの SQL Server マスター インスタンスのサーバーの照合順序を変更することはできません。

## <a name="configure-apache-spark-and-apache-hadoop"></a>Apache Spark と Apache Hadoop を構成する
ビッグ データ クラスターで Apache Spark と Apache Hadoop を構成するには、展開時にクラスター プロファイルを変更する必要があります。

ビッグ データ クラスターには、次の 4 つの構成カテゴリがあります。 

- `sql` 
- `hdfs` 
- `spark` 
- `gateway` 

`sql`、`hdfs`、`spark`、`sql` がサービスです。 各サービスは同じ名前の構成カテゴリにマップされます。 すべてのゲートウェイ構成は、カテゴリ `gateway` に属します。 

たとえば、サービス `hdfs` のすべての構成は、カテゴリ `hdfs` に属します。 Hadoop (コアサイト)、HDFS、Zookeeper の構成はすべて、カテゴリ `hdfs` に属し、Livy、Spark、Yarn、Hive、メタストアの構成はすべて、カテゴリ `spark` に属すことにご注意ください。 

[サポートされている構成](reference-config-spark-hadoop.md#supported-configurations)には、SQL Server ビッグ データ クラスターの展開時に構成できる Apache Spark と Hadoop のプロパティがリストアップされています。

次のセクションでは、クラスターで変更 **できない** プロパティをリストアップしています。

- [サポートされていない `spark` 構成](reference-config-spark-hadoop.md#unsupported-spark-configurations)
- [サポートされていない `hdfs` 構成](reference-config-spark-hadoop.md#unsupported-hdfs-configurations)
- [サポートされていない `gateway` 構成](reference-config-spark-hadoop.md#unsupported-gateway-configurations)

## <a name="next-steps"></a>次の手順

[SQL Server ビッグ データ クラスターを構成する](configure-bdc-overview.md)