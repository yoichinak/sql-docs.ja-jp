---
title: Python のチュートリアル
titleSuffix: SQL machine learning
description: この記事では、SQL 機械学習用の Python チュートリアルについて説明します。 スクリプトを実行して機械学習モデルを構築する方法をご確認ください。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: f417a92a00b290f06326433b24b73137a0a424fa
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178549"
---
# <a name="python-tutorials-for-sql-machine-learning"></a>SQL 機械学習用の Python チュートリアル
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
この記事では、[SQL Server 上の Machine Learning Services](../sql-server-machine-learning-services.md) および [ビッグ データ クラスター](../../big-data-cluster/machine-learning-services.md)用の Python のチュートリアルおよびクイックスタートについて説明します。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
この記事では、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 用の Python のチュートリアルおよびクイックスタートについて説明します。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
この記事では、[Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) 用の Python のチュートリアルおよびクイックスタートについて説明します。
::: moniker-end

<a name="bkmk_pythontutorials"></a>

## <a name="python-tutorials"></a>Python のチュートリアル

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
| チュートリアル | 説明 |
|-|-|
| [線形回帰によるスキー レンタルの予測](python-ski-rental-linear-regression.md) | Python と線形回帰を使用して、スキー レンタル数を予測します。 Azure Data Studio のノートブックを使用してデータの準備とモデルのトレーニングを行い、T-SQL を使用してモデルを展開します。 |
| [K-Means クラスタリングを使用した顧客の分類](python-clustering-model.md) | Python を使用して、顧客を分類するための K-Means クラスタリング モデルを開発および展開します。 Azure Data Studio のノートブックを使用してデータの準備とモデルのトレーニングを行い、T-SQL を使用してモデルを展開します。 |
| [revoscalepy を使用したモデルの作成](use-python-revoscalepy-to-create-model.md) | SQL Server を計算コンテキストとして使用してリモートの Python クライアントからコードを実行する方法を示します。 このチュートリアルでは、**revoscalepy** ライブラリの **rxLinMod** を使用してモデルを作成します。 |
| [SQL 開発者向けの Python データ分析](python-taxi-classification-introduction.md) | このエンドツーエンド チュートリアルでは、T-SQL を使用して完全な Python ソリューションを構築するプロセスについて説明します。 |
::: moniker-end
::: moniker range="=azuresqldb-mi-current"
| チュートリアル | 説明 |
|-|-|
| [線形回帰によるスキー レンタルの予測](python-ski-rental-linear-regression.md) | Python と線形回帰を使用して、スキー レンタル数を予測します。 Azure Data Studio のノートブックを使用してデータの準備とモデルのトレーニングを行い、T-SQL を使用してモデルを展開します。 |
| [K-Means クラスタリングを使用した顧客の分類](python-clustering-model.md) | Python を使用して、顧客を分類するための K-Means クラスタリング モデルを開発および展開します。 Azure Data Studio のノートブックを使用してデータの準備とモデルのトレーニングを行い、T-SQL を使用してモデルを展開します。 |
::: moniker-end

## <a name="python-quickstarts"></a>Python のクイックスタート

SQL 機械学習を初めて使用する場合は、Python のクイックスタートを試すこともできます。

| クイック スタート | 説明 |
|-|-|
| [単純な Python スクリプトを実行する](quickstart-python-create-script.md) | [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)を使用して T-SQL で Python を呼び出す方法の基本を説明します。 |
| [Python を使用したデータ構造とオブジェクト](quickstart-python-data-structures.md) | SQL で Python pandas パッケージを使用してデータ構造を処理する方法について説明します。 |
| [Python での予測モデルの作成とスコア付け](quickstart-python-train-score-model.md) | Python モデルを作成、トレーニング、および使用して新しいデータから予測を行う方法について説明します。 |

## <a name="next-steps"></a>次のステップ

+ [SQL Server の Python 拡張機能](../concepts/extension-python.md)
