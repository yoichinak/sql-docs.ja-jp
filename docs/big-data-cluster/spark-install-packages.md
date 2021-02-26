---
title: Spark ライブラリ管理
titleSuffix: SQL Server big data clusters
description: Spark ライブラリ管理
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 01/25/2021
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 70611d3f7d4ed6825911908942d9ed707dabbd2e
ms.sourcegitcommit: 8bdb5a51f87a6ff3b94360555973ca0cd0b6223f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/16/2021
ms.locfileid: "100549970"
---
# <a name="spark-library-management"></a>Spark ライブラリ管理

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

この記事では、セッションとノートブックの構成を通じて、Spark セッション用のパッケージをインポートおよびインストールする方法について説明します。

## <a name="built-in-tools"></a>組み込みツール
Spark および Hadoop の基本パッケージ Python 3.7 および Python 2.7 Pandas、Sklearn、Numpy、その他のデータ処理パッケージ。
R および MRO のパッケージ Sparklyr

## <a name="install-packages-from-a-maven-repository-onto-the-spark-cluster-at-runtime"></a>実行時に Maven リポジトリから Spark クラスターにパッケージをインストールする
Spark セッションの開始時にノートブックのセル構成を使用して、Maven パッケージを Spark クラスターにインストールできます。 Azure Data Studio で Spark セッションを開始する前に、次のコードを実行します。

```
%%configure -f \
{"conf": {"spark.jars.packages": "com.microsoft.azure:azure-eventhubs-spark_2.11:2.3.1"}}
```

## <a name="install-python-packages-at-pyspark-job-submission-time"></a>PySpark ジョブの送信時に Python パッケージをインストールする
1. インストールするパッケージの参照として使用する HDFS 内の requirements.txt ファイルへのパスを指定します。
```
%%configure -f \
{"conf": {
    "spark.pyspark.virtualenv.enabled" : "true",
    "spark.pyspark.virtualenv.type" : "conda",
    "spark.pyspark.virtualenv.requirements" : "requirements.txt",
    "spark.pyspark.virtualenv.bin.path" : "/opt/mls/python/bin/conda"
    }, 
"files": ["hdfs://nmnode-0/tmp/requirements.txt"]
}
```
2. requirements ファイルを使用せずに conda virtualenv を作成し、Spark セッション中にパッケージを動的に追加します。
```
%%configure -f \
{"conf": {
    'spark.pyspark.virtualenv.enabled' : 'true',
    'spark.pyspark.virtualenv.type' : 'conda',
    'spark.pyspark.virtualenv.bin.path' : '/opt/mls/python/bin/conda',
    'spark.pyspark.virtualenv.python_version': '3.6'
 }
 ```

 ```python
sc.install_packages("numpy==1.11.0")
import numpy as np
```

## <a name="import-jar-from-hdfs-for-use-at-runtime"></a>実行時に使用するために、HDFS から .jar をインポートする
Azure Data Studio ノートブックのセル構成を使用して、実行時に jar をインポートします。

```
%%configure -f
{"conf": {"spark.jars": "/jar/mycodeJar.jar"}}
```

### <a name="import-jar-at-runtime-through-azure-data-studio-notebook-cell-configuration"></a>Azure Data Studio ノートブックのセル構成を使用して、実行時に .jar をインポートする
```
%%configure -f
{"conf": {"spark.jars": "/jar/mycodeJar.jar"}}
```

## <a name="next-steps"></a>次の手順

SQL Server ビッグ データ クラスターと関連するシナリオの詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)」を参照してください。