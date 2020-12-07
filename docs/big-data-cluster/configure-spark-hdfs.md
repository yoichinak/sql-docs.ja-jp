---
title: Apache Spark と Apache Hadoop
titleSuffix: Configure Apache Spark and Apache Hadoop in Big Data Clusters
description: SQL Server ビッグ データ クラスターでは、Spark ソリューションと HDFS ソリューションを使用できます。 これらの構成方法について説明します。
author: rajmera3
ms.author: raajmera
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1e5d0941256fbb1e167f65489e250eed9c9b895a
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257222"
---
# <a name="configure-apache-spark-and-apache-hadoop-in-big-data-clusters"></a>ビッグ データ クラスターで Apache Spark と Apache Hadoop を構成する

ビッグ データ クラスターで Apache Spark と Apache Hadoop を構成するには、展開時にクラスター プロファイルを変更する必要があります。

ビッグ データ クラスターには、次の 4 つの構成カテゴリがあります。 

- `sql` 
- `hdfs` 
- `spark` 
- `gateway` 

`sql`、`hdfs`、`spark`、`sql` がサービスです。 各サービスは同じ名前の構成カテゴリにマップされます。 すべてのゲートウェイ構成は、カテゴリ `gateway` に属します。 

たとえば、サービス `hdfs` のすべての構成は、カテゴリ `hdfs` に属します。 Hadoop (コアサイト)、HDFS、Zookeeper の構成はすべて、カテゴリ `hdfs` に属し、Livy、Spark、Yarn、Hive、メタストアの構成はすべて、カテゴリ `spark` に属すことにご注意ください。 

[サポートされている構成](reference-config-spark-hadoop.md#supported-configurations)には、SQL Server ビッグ データ クラスターの展開時に構成できる Apache Spark と Hadoop のプロパティがリストアップされています。

次のセクションでは、クラスターで変更**できない**プロパティをリストアップしています。

- [サポートされていない `spark` 構成](reference-config-spark-hadoop.md#unsupported-spark-configurations)
- [サポートされていない `hdfs` 構成](reference-config-spark-hadoop.md#unsupported-hdfs-configurations)
- [サポートされていない `gateway` 構成](reference-config-spark-hadoop.md#unsupported-gateway-configurations)


## <a name="configurations-via-cluster-profile"></a>クラスター プロファイルによる構成

クラスター プロファイルには、リソースとサービスがあります。 展開時に、次の 2 つの方法のいずれかで構成を指定することができます。 

* 1 つ目は、リソース レベルでの構成です。 

   次の例は、プロファイルの修正プログラム ファイルを示しています。 

   ```json
   { 
         "op": "add", 
         "path": "spec.resources.zookeeper.spec.settings", 
         "value": { 
           "hdfs": { 
             "zoo-cfg.syncLimit": "6" 
           } 
         } 
   }
   ```

   または: 

   ```json
   { 
         "op": "add", 
         "path": "spec.resources.gateway.spec.settings", 
         "value": { 
           "gateway": { 
             "gateway-site.gateway.httpclient.socketTimeout": "95s" 
           } 
         } 
   } 
   ```

* 2 つ目は、サービス レベルでの構成です。 複数のリソースを 1 つのサービスに割り当て、サービスに対して構成を指定します。

次は、HDFS ブロック サイズを設定するためのプロファイルの修正プログラム ファイル例です。 

   ```json
   { 
         "op": "add", 
         "path": "spec.services.hdfs.settings", 
         "value": { 
           "hdfs-site.dfs.block.size": "268435456" 
        } 
   } 
   ```

サービス `hdfs` は次のように定義されます。

```json
{ 
  "spec": { 
   "services": { 
     "hdfs": { 
        "resources": [ 
          "nmnode-0", 
          "zookeeper", 
          "storage-0", 
          "sparkhead" 
        ], 
        "settings":{ 
          "hdfs-site.dfs.block.size": "268435456" 
        } 
      } 
    } 
  } 
} 
```
 
> [!NOTE]
> リソース レベルの構成は、サービス レベルの構成をオーバーライドします。 1 つのリソースを複数のサービスに割り当てることができます。

## <a name="enable-spark-in-the-storage-pool"></a>記憶域プールで Spark を有効にする
サポートされている Apache の構成に加えて、Spark ジョブをストレージ プールで実行できるかどうかを構成する機能も用意されています。 このブール値 `includeSpark`は、`spec.resources.storage-0.spec.settings.spark` にある `bdc.json` 構成ファイル内にあります。

bdc.json の記憶域プール定義の例は次のようになることがあります。
```json
...
"storage-0": {
                "metadata": {
                    "kind": "Pool",
                    "name": "default"
                },
                "spec": {
                    "type": "Storage",
                    "replicas": 2,
                    "settings": {
                        "spark": {
                            "includeSpark": "true"
                        }
                    }
                }
            }
```


## <a name="limitations"></a>制限事項

構成は、カテゴリ レベルでのみ指定することができます。 同じサブカテゴリで複数の構成を指定するために、クラスター プロファイルで共通プレフィックスを抽出することはできません。 

```json
{ 
      "op": "add", 
      "path": "spec.services.hdfs.settings.core-site.hadoop", 
      "value": { 
        “proxyuser.xyz.users”: “*”, 
        “proxyuser.abc.users”: “*” 
     } 
} 
```

## <a name="next-steps"></a>次のステップ

- [Apache Spark と Apache Hadoop (HDFS) の構成プロパティ。](reference-config-spark-hadoop.md)
- [[!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] リファレンス](../azdata/reference/reference-azdata.md)
- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]とは](big-data-cluster-overview.md)