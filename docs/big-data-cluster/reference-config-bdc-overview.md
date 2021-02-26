---
title: SQL Server ビッグ データ クラスターの構成プロパティ
titleSuffix: SQL Server big data clusters
description: ビッグ データ クラスターの構成プロパティに関するリファレンス記事
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 02/11/2021
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ecaba704d9c08619f42c5cdf8d726917ccc61b9c
ms.sourcegitcommit: 8dc7e0ececf15f3438c05ef2c9daccaac1bbff78
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2021
ms.locfileid: "100343543"
---
# <a name="sql-server-big-data-clusters-configuration-properties"></a>SQL Server ビッグ データ クラスターの構成プロパティ

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

ビッグ データ クラスターの構成設定は、`cluster`、`service`、`resource` のスコープで定義できます。 設定の階層も、この順序に従って、上位から下位に適用されます。 BDC コンポーネントでは、最下位のスコープで定義された設定の値が使用されます。 特定のスコープで設定が定義されていない場合は、上位の親スコープから値が継承されます。 さまざまなスコープで BDC の各コンポーネントに使用できる設定の一覧を以下に示します。 BDC の構成可能な設定は、azdata を使用して見ることもできます。

## <a name="bdc-cluster-scope-settings"></a>BDC のクラスター スコープの設定
次の設定は、クラスター スコープで構成できます。

|プロパティ|オプション|
| --- | --- |
|`mssql.telemetry`|`customerfeedback = { true | false }` |
|`mssql.traceflag`|`traceflag<#> = <####>` |

## <a name="sql-service-scope-settings"></a>SQL のサービス スコープの設定
次の設定は、SQL サービス スコープで構成できます。

|プロパティ|オプション|
| --- | --- |
|`mssql.language`|`lcid = <language_identifier>` |

## <a name="spark-service-scope-settings"></a>Spark のサービス スコープの設定
すべてのサポートされている設定とサポートされていない設定については、[Apache Spark および Apache Hadoop の構成に関する記事](reference-config-spark-hadoop.md)を参照してください。

## <a name="hdfs-service-scope-settings"></a>HDFS のサービス スコープの設定
すべてのサポートされている設定とサポートされていない設定については、[Apache Spark および Apache Hadoop の構成に関する記事](reference-config-spark-hadoop.md)を参照してください。

## <a name="gateway-service-scope-settings"></a>ゲートウェイのサービス スコープの設定
構成可能なゲートウェイのサービス スコープの設定はありません。 ゲートウェイのリソース スコープで設定を構成します。

## <a name="app-service-scope-settings"></a>アプリのサービス スコープの設定
使用できるものはありません

## <a name="master-pool-resource-scope-settings"></a>マスター プールのリソース スコープの設定
|プロパティ|オプション|
| --- | --- |
|`mssql.sqlagent`|`enabled = { true | false }` |
|`mssql.licensing`|`pid = { Enterprise | Developer }` |
<!-- |`mssql.collation`|`x = <language_identifier>` | -->

> [!NOTE]
> SQL Server のインスタンスに対する既定の照合順序の変更は、複雑な操作です。 `mssql.collation` の設定を変更するだけでなく、ユーザー データベースとその中のすべてのオブジェクトを作成し直すことが必要になる場合があります。 それを行う方法については、[サーバーの照合順序の設定または変更](../relational-databases/collations/set-or-change-the-server-collation.md#changing-the-server-collation-in-sql-server)に関するページを参照してください

## <a name="storage-pool-resource-scope-settings"></a>記憶域プールのリソース スコープの設定
記憶域プールは、SQL、Spark、HDFS の各コンポーネントで構成されています。

### <a name="available-sql-configurations"></a>使用可能な SQL の構成
|プロパティ|オプション|
| --- | --- |
|`mssql.degreeOfParallelism`| |
|`mssql.minServerMemory`| |
|`mssql.maxServerMemory`| |
|`mssql.network.tlscert`| |
|`mssql.network.tlskey`| |
|`mssql.numberOfCpus`| |
|`mssql.storagePoolCacheSize`| |
|`mssql.storagePoolMaxCacheSize`| |
|`mssql.storagePoolCacheAutogrowth`| |
|`mssql.tempdb.autogrowthPerDataFile`| |
|`mssql.tempdb.autogrowthPerLogFile`| |
|`mssql.tempdb.dataFileSize`| |
|`mssql.tempdb.dataFileMaxSize`| |
|`mssql.tempdb.logFileMaxSize`| |
|`mssql.tempdb.numberOfDataFiles`| |
|`mssql.traceflag`|`traceflag<#> = <####>` |


### <a name="available-apache-spark-and-hadoop-configurations"></a>使用可能な Apache Spark と Hadoop の構成
すべてのサポートされている設定とサポートされていない設定については、[Apache Spark および Apache Hadoop の構成に関する記事](reference-config-spark-hadoop.md)を参照してください。

## <a name="data-pool-resource-scope-settings"></a>データ プールのリソース スコープの設定
|プロパティ|オプション|
| --- | --- |
|`mssql.degreeOfParallelism`| |
|`mssql.minServerMemory`| |
|`mssql.maxServerMemory`| |
|`mssql.network.tlscert`| |
|`mssql.network.tlskey`| |
|`mssql.numberOfCpus`| |
|`mssql.tempdb.autogrowthPerDataFile`| |
|`mssql.tempdb.autogrowthPerLogFile`| |
|`mssql.tempdb.dataFileSize`| |
|`mssql.tempdb.dataFileMaxSize`| |
|`mssql.tempdb.logFileMaxSize`| |
|`mssql.tempdb.numberOfDataFiles`| |
|`mssql.traceflag`|`traceflag<#> = <####>` |

## <a name="compute-pool-resource-scope-settings"></a>コンピューティング プールのリソース スコープの設定
|プロパティ|オプション|
| --- | --- |
|`mssql.degreeOfParallelism`| |
|`mssql.minServerMemory`| |
|`mssql.maxServerMemory`| |
|`mssql.network.tlscert`| |
|`mssql.network.tlskey`| |
|`mssql.numberOfCpus`| |
|`mssql.tempdb.autogrowthPerDataFile`| |
|`mssql.tempdb.autogrowthPerLogFile`| |
|`mssql.tempdb.dataFileSize`| |
|`mssql.tempdb.dataFileMaxSize`| |
|`mssql.tempdb.logFileMaxSize`| |
|`mssql.tempdb.numberOfDataFiles`| |
|`mssql.traceflag`|`traceflag<#> = <####>` |

## <a name="spark-pool-resource-scope-settings"></a>Spark プールのリソース スコープの設定
すべてのサポートされている設定とサポートされていない設定については、[Apache Spark および Apache Hadoop の構成に関する記事](reference-config-spark-hadoop.md)を参照してください。

## <a name="gateway-resource-scope-settings"></a>ゲートウェイのリソース スコープの設定
すべてのサポートされている設定とサポートされていない設定については、[Apache Spark および Apache Hadoop の構成に関する記事](reference-config-spark-hadoop.md)を参照してください。

## <a name="sparkhead-resource-scope-settings"></a>`Sparkhead` のリソース スコープの設定
すべてのサポートされている設定とサポートされていない設定については、[Apache Spark および Apache Hadoop の構成に関する記事](reference-config-spark-hadoop.md)を参照してください。

## <a name="zookeeper-resource-scope-settings"></a>Zookeeper のリソース スコープの設定
すべてのサポートされている設定とサポートされていない設定については、[Apache Spark および Apache Hadoop の構成に関する記事](reference-config-spark-hadoop.md)を参照してください。

## <a name="namenode-resource-scope-settings"></a>Namenode のリソース スコープの設定
すべてのサポートされている設定とサポートされていない設定については、[Apache Spark および Apache Hadoop の構成に関する記事](reference-config-spark-hadoop.md)を参照してください。

## <a name="app-proxy-resource-scope-settings"></a>アプリ プロキシのリソース スコープの設定
使用できるものはありません

## <a name="next-steps"></a>次の手順

[SQL Server ビッグ データ クラスターを構成する](configure-bdc-overview.md)