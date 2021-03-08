---
title: Spark ライブラリ管理
titleSuffix: SQL Server big data clusters
description: Spark ライブラリ管理
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 02/25/2021
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bed687cb003bfc7748aefa3c98ae5e19089f9685
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101837059"
---
# <a name="spark-library-management"></a>Spark ライブラリ管理

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

この記事では、セッションとノートブックの構成を通じて、Spark セッション用のパッケージをインポートおよびインストールする方法について説明します。

## <a name="built-in-tools"></a>組み込みツール

Scala Spark (Scala 2.11) と Hadoop 基本パッケージ。 

PySpark (Python 3.7)。 Pandas、Sklearn、Numpy、その他のデータ処理および機械学習パッケージ。

MRO 3.5.2 パッケージ。 R Spark ワークロード用の Sparklyr と SparkR。

## <a name="install-packages-from-a-maven-repository-onto-the-spark-cluster-at-runtime"></a>実行時に Maven リポジトリから Spark クラスターにパッケージをインストールする

Spark セッションの開始時にノートブックのセル構成を使用して、Maven パッケージを Spark クラスターにインストールできます。 Azure Data Studio で Spark セッションを開始する前に、次のコードを実行します。

```python
%%configure -f \
{"conf": {"spark.jars.packages": "com.microsoft.azure:azure-eventhubs-spark_2.11:2.3.1"}}
```

## <a name="install-python-packages-at-pyspark-at-runtime"></a>実行時に PySpark に Python パッケージをインストールする

セッションおよびジョブ レベルのパッケージ管理により、ライブラリの一貫性と分離が保証されます。 この構成は、Livy セッションに適用できる Spark 標準ライブラリ構成です。 __azdata spark__ では、これらの構成がサポートされています。 次の例は、PySpark カーネルを使用してクラスターにアタッチした後で実行する必要がある __Azure Data Studio Notebooks__ の構成セルとして提供されています。

__"spark.pyspark.virtualenv.enabled" : "true"__ の構成が設定されていない場合は、クラスターの既定の Python とインストールされているライブラリが、セッションで使用されます。

### <a name="sessionjob-configuration-with-requirementstxt"></a>requirements.txt でのセッションとジョブの構成

インストールするパッケージの参照として使用する HDFS 内の requirements.txt ファイルへのパスを指定する場合。

```python
%%configure -f \
{
    "conf": {
        "spark.pyspark.virtualenv.enabled" : "true",
        "spark.pyspark.virtualenv.python_version": "3.7",
        "spark.pyspark.virtualenv.requirements" : "hdfs://user/project-A/requirements.txt"
    }
}
```

### <a name="sessionjob-configuration-with-different-python-versions"></a>さまざまな Python バージョンでのセッションとジョブの構成

requirements ファイルを使用せずに conda virtualenv を作成し、Spark セッション中にパッケージを動的に追加します。

```python
%%configure -f \
{
    "conf": {
        "spark.pyspark.virtualenv.enabled" : "true",
        "spark.pyspark.virtualenv.python_version": "3.6"
    }
}
```

### <a name="library-installation"></a>ライブラリのインストール

ライブラリをセッションに動的にインストールするには、__sc.install_packages__ を実行します。 ライブラリは、ドライバーと、すべての Executor のノードにインストールされます。

 ```python
sc.install_packages("numpy==1.11.0")
import numpy as np
```

配列を使用して、同じコマンドで複数のライブラリをインストールすることもできます。

 ```python
sc.install_packages(["numpy==1.11.0", "xgboost"])
import numpy as np
import xgboost as xgb
```

## <a name="import-jar-from-hdfs-for-use-at-runtime"></a>実行時に使用するために、HDFS から .jar をインポートする
Azure Data Studio ノートブックのセル構成を使用して、実行時に jar をインポートします。

```python
%%configure -f
{"conf": {"spark.jars": "/jar/mycodeJar.jar"}}
```

### <a name="import-jar-at-runtime-through-azure-data-studio-notebook-cell-configuration"></a>Azure Data Studio ノートブックのセル構成を使用して、実行時に .jar をインポートする

```python
%%configure -f
{"conf": {"spark.jars": "/jar/mycodeJar.jar"}}
```

## <a name="next-steps"></a>次の手順

SQL Server ビッグ データ クラスターと関連するシナリオの詳細については、「[[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md)」を参照してください。