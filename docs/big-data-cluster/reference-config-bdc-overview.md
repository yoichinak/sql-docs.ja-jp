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
ms.openlocfilehash: c7cfe84e9b301ee75d1a031231824e50b0de6b9c
ms.sourcegitcommit: 765262cdc6352a5325148afc22fa4f1499fe1aa3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2021
ms.locfileid: "102514879"
---
# <a name="sql-server-big-data-clusters-configuration-properties"></a>SQL Server ビッグ データ クラスターの構成プロパティ

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

ビッグ データ クラスターの構成設定は、`cluster`、`service`、`resource` のスコープで定義できます。 設定の階層も、この順序に従って、上位から下位に適用されます。 BDC コンポーネントでは、最下位のスコープで定義された設定の値が使用されます。 特定のスコープで設定が定義されていない場合は、上位の親スコープから値が継承されます。 さまざまなスコープで BDC の各コンポーネントに使用できる設定の一覧を以下に示します。 BDC の構成可能な設定は、azdata を使用して見ることもできます。

## <a name="bdc-cluster-scope-settings"></a>BDC のクラスター スコープの設定
次の設定は、クラスター スコープで構成できます。

| 設定名                                             | 説明                                                                                                                                                                                                                                                                                                             | Type   | 既定値          | デプロイ時のみ | 
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ---------------------------- | --------- | 
| bdc.telemetry.customerFeedback                              | このクラスターが、製品の使用状況と診断データを Microsoft に送信するカスタマー エクスペリエンス向上プログラム (CEIP) に参加するかどうかを制御します。 | boolean | true                    |           | 

## <a name="sql-service-scope-settings"></a>SQL のサービス スコープの設定
次の設定は、SQL サービス スコープで構成できます。

| 設定名                                             | 説明                                                                                                                                                                                                                                                                                                             | Type   | 既定値          | デプロイ時のみ | 
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ---------------------------- | --------- | 
| mssql.language.lcid                              | SQL Server のロケールが、サポートされているいずれかの言語識別子 (LCID) に変更されます。                                                                                                                                                                                                                                              | INT    | 1033                         |           | 

## <a name="spark-service-scope-settings"></a>Spark のサービス スコープの設定
すべてのサポートされている設定とサポートされていない設定については、[Apache Spark および Apache Hadoop の構成に関する記事](reference-config-spark-hadoop.md)を参照してください。

## <a name="hdfs-service-scope-settings"></a>HDFS のサービス スコープの設定
すべてのサポートされている設定とサポートされていない設定については、[Apache Spark および Apache Hadoop の構成に関する記事](reference-config-spark-hadoop.md)を参照してください。

## <a name="gateway-service-scope-settings"></a>ゲートウェイのサービス スコープの設定
構成可能なゲートウェイのサービス スコープの設定はありません。 ゲートウェイのリソース スコープで設定を構成します。

## <a name="app-service-scope-settings"></a>アプリのサービス スコープの設定
使用できるものはありません

## <a name="master-pool-resource-scope-settings"></a>マスター プールのリソース スコープの設定
| 設定名                                             | 説明                                                                                                                                                                                                                                                                                                             | Type   | 既定値          | デプロイ時のみ | 
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ---------------------------- | --------- | 
| mssql.licensing.pid                              | SQL Server のエディション。                                                                                                                                                                                                                                                                                                     | string | 開発者                    |           | 
| mssql.sqlagent.enabled                           | SQL Server エージェントを有効にします。                                                                                                                                                                                                                                                                                               | [bool]   | false                        |           | 
| mssql.collation                                  | SQL Server の照合順序を、サポートされているいずれかの照合順序に変更します。                                                                                                                                                                                                                                                    | string | SQL_Latin1_General_CP1_CI_AS | true      | 
| hadr.enabled                                     | SQL Server マスター プールの可用性グループを有効にするためのブール値。                                                                                                                                                                                                                                                    | [bool]   | false                        | true      | 
| hadr.leaseDurationInSeconds                      | HA エージェントのリース有効期限のタイムアウト。                                                                                                                                                                                                                                                                                  | INT    | 30                           |           | 
| hadr.externalLeasePollingEnabled                 | 外部リース ポーリング API を有効にするためのブール値。                                                                                                                                                                                                                                                                        | bool   | true                         | true      | 
| mssql.telemetry.userRequestedLocalAuditDirectory | SQL Server のローカル監査を有効にし、'ローカル監査' ログが作成されるディレクトリを設定できるようになります。 ディレクトリは '/var/opt/mssql/audit' の下になければなりません。                                                                                                                                                            | string |                              |           | 

## <a name="storage-pool-resource-scope-settings"></a>記憶域プールのリソース スコープの設定
記憶域プールは、SQL、Spark、HDFS の各コンポーネントで構成されています。

### <a name="available-sql-configurations"></a>使用可能な SQL の構成
| 設定名                                             | 説明                                                                                                                                                                                                                                                                                                             | Type   | 既定値          | デプロイ時のみ | 
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ---------------------------- | --------- | 
| mssql.degreeOfParallelism                        | 並列処理の次数に基づいて、SQL インスタンスごとに 1 つのステートメントを実行するために使用されるプロセッサの数が設定されます。                                                                                                                                                                                                        | INT    | 0                            |           | 
| mssql.maxServerMemory                            | SQL Server のインスタンスで使用される SQL Server プロセス用の最大メモリ量 (MB)。                                                                                                                                                                                                                 | INT    | 2147483647                   |           | 
| mssql.minServerMemory                            | SQL Server のインスタンスで使用される SQL Server プロセス用の最小メモリ量 (MB)。                                                                                                                                                                                                                 | INT    | 0                            |           | 
| mssql.numberOfCpus                    | 指定された範囲内の個々の CPU に SQL Server のワーカー スレッドを配分します。 指定された範囲外の CPU にはスレッドの割り当ては行われません。 AUTO の場合は、0 を指定します。 | string | AUTO                         |           | 
| mssql.storagePoolCacheSize                       | 記憶域プール内の各 SQL インスタンスのキャッシュのサイズ (MB)。                                                                                                                                                                                                                                             | INT    | 8                            |           | 
| mssql.storagePoolMaxCacheSize                    | 記憶域プール内の各 SQL インスタンスのキャッシュの最大サイズ (MB)。                                                                                                                                                                                                                                     | INT    | 16384                        |           | 
| mssql.storagePoolCacheAutogrowth                 | 記憶域プール キャッシュの自動拡張係数 (MB)。                                                                                                                                                                                                                                                                  | INT    | 256                          |           | 
| mssql.tempdb.autogrowthPerDataFile               | 各 TempDB データ ファイルの自動拡張 (MB)。                                                                                                                                                                                                                                                                          | INT    | 64                           |           | 
| mssql.tempdb.autogrowthPerLogFile                | 各 TempDB ログ ファイルの自動拡張 (MB)。                                                                                                                                                                                                                                                                           | INT    | 64                           |           | 
| mssql.tempdb.dataFileSize                        | 各 TempDB データ ファイルのファイル サイズ (MB)。                                                                                                                                                                                                                                                                           | INT    | 8                            |           | 
| mssql.tempdb.dataFileMaxSize                     | 各 TempDB データ ファイルの最大ファイル サイズ (MB)。                                                                                                                                                                                                                                                                   | INT    | 16777215                     |           | 
| mssql.tempdb.logFileSize                         | 各 TempDB ログ ファイルのファイル サイズ (MB)。                                                                                                                                                                                                                                                                            | INT    | 8                            |           | 
| mssql.tempdb.logFileMaxSize                      | 各 TempDB ログ ファイルの最大ファイル サイズ (MB)。                                                                                                                                                                                                                                                                    | INT    | 2097151                      |           | 
| mssql.tempdb.numberOfDataFiles                   | TempDB のデータ ファイルの数。                                                                                                                                                                                                                                                                                        | INT    | 8                            |           | 
| mssql.traceflags                                 | SQL Server サービスを起動するためのトレースフラグを有効または無効にします。 適用するトレースフラグのスペース区切りリストを指定してください。                                                                                                                                                                                        | string | 3614                         |           | 


### <a name="available-apache-spark-and-hadoop-configurations"></a>使用可能な Apache Spark と Hadoop の構成
すべてのサポートされている設定とサポートされていない設定については、[Apache Spark および Apache Hadoop の構成に関する記事](reference-config-spark-hadoop.md)を参照してください。

## <a name="data-pool-resource-scope-settings"></a>データ プールのリソース スコープの設定
| 設定名                                             | 説明                                                                                                                                                                                                                                                                                                             | Type   | 既定値          | デプロイ時のみ | 
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ---------------------------- | --------- | 
| mssql.degreeOfParallelism                        | 並列処理の次数に基づいて、SQL インスタンスごとに 1 つのステートメントを実行するために使用されるプロセッサの数が設定されます。                                                                                                                                                                                                        | INT    | 0                            |           | 
| mssql.maxServerMemory                            | SQL Server のインスタンスで使用される SQL Server プロセス用の最大メモリ量 (MB)。                                                                                                                                                                                                                 | INT    | 2147483647                   |           | 
| mssql.minServerMemory                            | SQL Server のインスタンスで使用される SQL Server プロセス用の最小メモリ量 (MB)。                                                                                                                                                                                                                 | INT    | 0                            |           | 
| mssql.numberOfCpus                    | 指定された範囲内の個々の CPU に SQL Server のワーカー スレッドを配分します。 指定された範囲外の CPU にはスレッドの割り当ては行われません。 AUTO の場合は、0 を指定します。 | string | AUTO                         |           | 
| mssql.tempdb.autogrowthPerDataFile               | 各 TempDB データ ファイルの自動拡張 (MB)。                                                                                                                                                                                                                                                                          | INT    | 64                           |           | 
| mssql.tempdb.autogrowthPerLogFile                | 各 TempDB ログ ファイルの自動拡張 (MB)。                                                                                                                                                                                                                                                                           | INT    | 64                           |           | 
| mssql.tempdb.dataFileSize                        | 各 TempDB データ ファイルのファイル サイズ (MB)。                                                                                                                                                                                                                                                                           | INT    | 8                            |           | 
| mssql.tempdb.dataFileMaxSize                     | 各 TempDB データ ファイルの最大ファイル サイズ (MB)。                                                                                                                                                                                                                                                                   | INT    | 16777215                     |           | 
| mssql.tempdb.logFileSize                         | 各 TempDB ログ ファイルのファイル サイズ (MB)。                                                                                                                                                                                                                                                                            | INT    | 8                            |           | 
| mssql.tempdb.logFileMaxSize                      | 各 TempDB ログ ファイルの最大ファイル サイズ (MB)。                                                                                                                                                                                                                                                                    | INT    | 2097151                      |           | 
| mssql.tempdb.numberOfDataFiles                   | TempDB のデータ ファイルの数。                                                                                                                                                                                                                                                                                        | INT    | 8                            |           | 
| mssql.traceflags                                 | SQL Server サービスを起動するためのトレースフラグを有効または無効にします。 適用するトレースフラグのスペース区切りリストを指定してください。                                                                                                                                                                                        | string | 3614                         |           | 

## <a name="compute-pool-resource-scope-settings"></a>コンピューティング プールのリソース スコープの設定
| 設定名                                             | 説明                                                                                                                                                                                                                                                                                                             | Type   | 既定値          | デプロイ時のみ | 
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | ---------------------------- | --------- | 
| mssql.degreeOfParallelism                        | 並列処理の次数に基づいて、SQL インスタンスごとに 1 つのステートメントを実行するために使用されるプロセッサの数が設定されます。                                                                                                                                                                                                        | INT    | 0                            |           | 
| mssql.maxServerMemory                            | SQL Server のインスタンスで使用される SQL Server プロセス用の最大メモリ量 (MB)。                                                                                                                                                                                                                 | INT    | 2147483647                   |           | 
| mssql.minServerMemory                            | SQL Server のインスタンスで使用される SQL Server プロセス用の最小メモリ量 (MB)。                                                                                                                                                                                                                 | INT    | 0                            |           | 
| mssql.numberOfCpus                    | 指定された範囲内の個々の CPU に SQL Server のワーカー スレッドを配分します。 指定された範囲外の CPU にはスレッドの割り当ては行われません。 AUTO の場合は、0 を指定します。 | string | AUTO                         |           | 
| mssql.tempdb.autogrowthPerDataFile               | 各 TempDB データ ファイルの自動拡張 (MB)。                                                                                                                                                                                                                                                                          | INT    | 64                           |           | 
| mssql.tempdb.autogrowthPerLogFile                | 各 TempDB ログ ファイルの自動拡張 (MB)。                                                                                                                                                                                                                                                                           | INT    | 64                           |           | 
| mssql.tempdb.dataFileSize                        | 各 TempDB データ ファイルのファイル サイズ (MB)。                                                                                                                                                                                                                                                                           | INT    | 8                            |           | 
| mssql.tempdb.dataFileMaxSize                     | 各 TempDB データ ファイルの最大ファイル サイズ (MB)。                                                                                                                                                                                                                                                                   | INT    | 16777215                     |           | 
| mssql.tempdb.logFileSize                         | 各 TempDB ログ ファイルのファイル サイズ (MB)。                                                                                                                                                                                                                                                                            | INT    | 8                            |           | 
| mssql.tempdb.logFileMaxSize                      | 各 TempDB ログ ファイルの最大ファイル サイズ (MB)。                                                                                                                                                                                                                                                                    | INT    | 2097151                      |           | 
| mssql.tempdb.numberOfDataFiles                   | TempDB のデータ ファイルの数。                                                                                                                                                                                                                                                                                        | INT    | 8                            |           | 
| mssql.traceflags                                 | SQL Server サービスを起動するためのトレースフラグを有効または無効にします。 適用するトレースフラグのスペース区切りリストを指定してください。                                                                                                                                                                                        | string | 3614                         |           | 

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