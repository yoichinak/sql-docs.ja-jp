---
title: microsoftml Python パッケージ
description: microsoftml は、Microsoft が提供する Python パッケージであり、ハイパフォーマンスの機械学習アルゴリズムを備えています。 トレーニング、変換、スコアリング、テキストと画像の分析、既存のデータから値を派生させるための特徴抽出を行うための関数が含まれています。 このパッケージは、SQL Server Machine Learning Services に含まれています。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a1f7c2c49acebe30b2739115b32643b2423f91cb
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956927"
---
# <a name="microsoftml-python-package-in-sql-server-machine-learning-services"></a>microsoftml (SQL Server Machine Learning Services の Python パッケージ)
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

**microsoftml** は、Microsoft が提供する Python パッケージであり、ハイパフォーマンスの機械学習アルゴリズムを備えています。 トレーニング、変換、スコアリング、テキストと画像の分析、既存のデータから値を派生させるための特徴抽出を行うための関数が含まれています。 このパッケージは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) に含まれており、マルチコア処理を使用したビッグ データでのハイパフォーマンス、および高速データ ストリーミングをサポートしています。

## <a name="full-reference-documentation"></a>完全なリファレンス ドキュメント

**microsoftml** パッケージは、複数の Microsoft 製品で配布されていますが、このパッケージを SQL Server または別の製品のどちらで取得しても、使用方法は同じです。 これらの関数は同じであるため、[個々の microsoftml 関数のドキュメント](/machine-learning-server/python-reference/microsoftml/microsoftml-package)は Microsoft Machine Learning Server の [Python リファレンス](/machine-learning-server/python-reference/introducing-python-package-reference)の下でのみ公開されています。 製品固有の動作が存在する場合、関数のヘルプ ページにその相違点が示されます。

## <a name="versions-and-platforms"></a>バージョンとプラットフォーム

**microsoftml** モジュールは Python 3.5 に基づいており、次のいずれかの Microsoft 製品またはダウンロードをインストールした場合にのみ利用できます。

+ [SQL Server Machine Learning サービス](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 以降](/machine-learning-server/)
+ [データ サイエンス クライアント用の Python クライアント ライブラリ](setup-python-client-tools-sql.md)

> [!NOTE]
> 完全な製品リリース バージョンは、SQL Server 2017 では Windows のみです。 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md) の **microsoftml** では、Windows と Linux の両方がサポートされています。

## <a name="package-dependencies"></a>パッケージの依存関係

**microsoftml** のアルゴリズムは、次に関して [revoscalepy](ref-py-revoscalepy.md) に依存します。

+ データ ソース オブジェクト。 **microsoftml** 関数によって使用されるデータは、**revoscalepy** 関数を使用して作成されます。
+ リモート コンピューティング (関数の実行をリモート SQL Server インスタンスにシフトする)。 **revoscalepy** パッケージには、SQL Server のリモート計算コンテキストを作成およびアクティブ化するための関数が用意されています。

ほとんどの場合、**microsoftml** を使用しているときは常に、パッケージをまとめて読み込みます。

## <a name="functions-by-category"></a>カテゴリ別の関数

このセクションでは、関数をカテゴリ別に一覧表示し、それぞれの使用方法について説明します。 [目次](/machine-learning-server/python-reference/introducing-python-package-reference)を使用して関数をアルファベット順に検索することもできます。

## <a name="1-training-functions"></a>1 - トレーニング関数

| 機能 | 説明 |
|----------|-------------|
|[microsoftml.rx_ensemble](/machine-learning-server/python-reference/microsoftml/rx-ensemble) | モデルのアンサンブルをトレーニングします。 |
|[microsoftml.rx_fast_forest](/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | ランダム フォレスト。 |
|[microsoftml.rx_fast_linear](/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | 線形モデル。 確率的双対座標上昇法による。 |
|[microsoftml.rx_fast_trees](/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | ブーストされたツリー。 |
|[microsoftml.rx_logistic_regression](/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | ロジスティック回帰。 |
|[microsoftml.rx_neural_network](/machine-learning-server/python-reference/microsoftml/rx-neural-network) | ニューラル ネットワーク。 |
|[microsoftml.rx_oneclass_svm](/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | 異常検出。 |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2 - 変換関数

### <a name="categorical-variable-handling"></a>カテゴリ変数の処理

| 機能 | 説明 |
|----------|-------------|
|[microsoftml.categorical](/machine-learning-server/python-reference/microsoftml/categorical) | テキスト列をカテゴリに変換します。 |
|[microsoftml.categorical_hash](/machine-learning-server/python-reference/microsoftml/categorical-hash) | テキスト列をハッシュし、カテゴリに変換します。 |

### <a name="schema-manipulation"></a>スキーマ操作

| 機能 | 説明 |
|----------|-------------|
|[microsoftml.concat](/machine-learning-server/python-reference/microsoftml/concat) | 複数の列を連結して 1 つのベクトルにします。 |
|[microsoftml.drop_columns](/machine-learning-server/python-reference/microsoftml/drop-columns) | データセットから列を削除します。 |
|[microsoftml.select_columns](/machine-learning-server/python-reference/microsoftml/select-columns) | データセットの列を保持します。 |


### <a name="variable-selection"></a>選択、変数

| 機能 | 説明 |
|----------|-------------|
|[microsoftml.count_select](/machine-learning-server/python-reference/microsoftml/count-select) |カウントに基づく特徴の選択。 |
|[microsoftml.mutualinformation_select](/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | 相互情報に基づく特徴の選択。 |


### <a name="text-analytics"></a>テキスト分析

| 機能 | 説明 |
|----------|-------------|
|[microsoftml.featurize_text](/machine-learning-server/python-reference/microsoftml/featurize-text) | テキスト列を数的特徴に変換します。 |
|[microsoftml.get_sentiment](/machine-learning-server/python-reference/microsoftml/get-sentiment) | 感情分析。 |


### <a name="image-analytics"></a>画像分析 

| 機能 | 説明 |
|----------|-------------|
|[microsoftml.load_image](/machine-learning-server/python-reference/microsoftml/load-image) | 画像を読み込みます。 |
|[microsoftml.resize_image](/machine-learning-server/python-reference/microsoftml/resize-image) | 画像サイズを変更します。 |
|[microsoftml.extract_pixels](/machine-learning-server/python-reference/microsoftml/extract-pixels) | 画像からピクセルを抽出します。 |
|[microsoftml.featurize_image](/machine-learning-server/python-reference/microsoftml/featurize-image) | 画像を特徴に変換します。 |

### <a name="featurization-functions"></a>特徴付け関数

| 機能 | 説明 |
|----------|-------------|
|[microsoftml.rx_featurize](/machine-learning-server/python-reference/microsoftml/rx-featurize) | データ ソースのデータ変換 |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3 - スコア付け関数

| 機能 | 説明 |
|----------|-------------|
|[microsoftml.rx_predict](/machine-learning-server/python-reference/microsoftml/rx-predict) | Microsoft 機械学習アルゴリズムを使用してスコアを付けます。 |

## <a name="how-to-call-microsoftml"></a>microsoftml を呼び出す方法

**microsoftml** 内の関数は、ストアド プロシージャにカプセル化された Python コードで呼び出すことができます。 ほとんどの開発者は、**microsoftml** ソリューションをローカルでビルドし、完成した Python コードを展開の練習としてストアド プロシージャに移行します。

Python の **microsoftml** パッケージは既定でインストールされますが、**revoscalepy** とは異なり、SQL Server でインストールされる Python 実行ファイルで Python を起動したとき、既定では読み込まれません。

最初の手順として、**microsoftml** パッケージをインポートし、リモート計算コンテキスト、関連する接続またはデータ ソース オブジェクトを使用する必要がある場合は、次に **revoscalepy** をインポートします。 その後、必要な個々の関数を参照します。

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>関連項目

+ [Python のチュートリアル](../tutorials/python-tutorials.md)
+ [Python リファレンス (Microsoft Machine Learning Server)](/machine-learning-server/python-reference/introducing-python-package-reference)