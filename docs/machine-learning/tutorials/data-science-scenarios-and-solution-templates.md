---
title: データ サイエンス ソリューション テンプレート
description: この記事では、機械学習ソリューションを実装する際に役立つベスト プラクティスと構成要素を提供する業界固有のテンプレートについて説明します。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 82c949647cf670c0e335b2c4446c248fea86581d
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196327"
---
# <a name="data-science-scenarios-and-solution-templates"></a>データ サイエンスのシナリオとソリューション テンプレート
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

この記事では、さまざまな SQL Server 機械学習ソリューション テンプレートについて説明します。 これらのテンプレートにはベスト プラクティスが示されており、機械学習ソリューションを短時間で実装する際に役立つ構成要素が提供されます。 各テンプレートは、特定の業種または業界に固有のデータ サイエンスに関する問題を解決するように設計されています。
各テンプレートのタスクは、データ準備や機能エンジニアリングから、モデルのトレーニングとスコアリングまで、多岐にわたります。 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
これらのテンプレートを使用して、[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] のしくみを学習します。 その後で、独自のシナリオに合わせてテンプレートをカスタマイズし、カスタム ソリューションを構築できます。
::: moniker-end

::: moniker range=">=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions"
これらのテンプレートを使用して、SQL Server Machine Learning Services のしくみを学習します。 その後で、独自のシナリオに合わせてテンプレートをカスタマイズし、カスタム ソリューションを構築できます。
::: moniker-end

各ソリューションには、サンプル データ、R コードまたは Python コード、SQL ストアド プロシージャ (該当する場合) が含まれています。 このコードは、SQL Server で計算を実行することで、任意の R または Python 開発環境で実行できます。 場合によっては、T-SQL と SQL クライアント ツール (SQL Server Management Studio など) を使用してコードを直接実行できます。

> [!TIP]
> 
> ほとんどのテンプレートは、オンプレミスとクラウドの両方のプラットフォームで機械学習をサポートする複数のバージョンを用意しています。 たとえば、SQL Server のみを使用してソリューションをビルドしたり、Microsoft R Server または Azure Machine Learning でソリューションをビルドしたりできます。

+ ダウンロードとセットアップの手順については、「[テンプレートの使用方法](#bkmk_HowTo)」を参照してください。

## <a name="fraud-detection"></a>不正行為の検出

[オンライン不正行為検出テンプレート (SQL Server R Services)](https://github.com/Microsoft/r-server-fraud-detection)

**問題:** オンライン ビジネスでは、不正なトランザクションを検出する機能が重要です。 チャージバックの損失を減らすために、企業は、盗まれた支払い方法または資格情報を使用して実行されたトランザクションを迅速に特定する必要があります。 不正な取引が検出された場合、通常、それ以上の損失を防ぐために、できるだけ早く特定のアカウントをブロックする措置を取ります。 このシナリオでは、オンライン購入取引のデータを使用して、不正行為の可能性が高い取引を特定する方法について説明します。

**方法:** 不正行為の検出は、二項分類問題として解決されます。 このテンプレートに使用する手法は、他のドメインの不正行為の検出にも簡単に適用できます。


## <a name="campaign-optimization"></a>キャンペーンの最適化

[潜在顧客に連絡する方法とタイミングを予測する](https://microsoft.github.io/r-server-campaign-optimization/)

**問題:** このソリューションでは、保険業界データを使用して、人口統計、応答履歴データ、および製品固有の詳細に基づいて潜在顧客を予測します。  購入行動を促すためのユーザーへのアプローチに最適なチャネルとタイミングを示すために推奨事項も生成されます。

**方法:** このソリューションでは、複数のモデルを作成して比較します。 このソリューションでは、ストアド プロシージャを使用した自動化されたデータ統合とデータ準備についても説明します。 並列サンプルは、データベース、Azure、および HDInsight Spark の SQL Server 用に用意されています。 

## <a name="health-care-predict-length-of-stay-in-hospital"></a>医療: 予想される入院期間 

[予想される入院期間](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**問題:** どの患者が長期入院を必要とするかを正確に予測することは、治療と計画の両方の重要な部分です。 管理者は、より多くのリソースを必要とする施設を特定できる必要があり、介護者は、患者のニーズを満たすことができることを保証する必要があります。

**方法:** このソリューションは、Data Science Virtual Machine を使用し、機械学習が有効になっている SQL Server のインスタンスを含みます。 また、デプロイ済みモデルとの対話に使用できる一連の Power BI レポートも含まれています。

## <a name="customer-churn"></a>顧客離反

[顧客離反予測テンプレート (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/README.md)顧客離反

**問題:** 顧客離反の分析と予測は、顧客離反を管理し、防ぐ必要がある業界で重要です。たとえば、銀行、電気通信、小売店などです。 顧客離れ分析の目標は、離れる可能性が高い顧客を特定し、そのような顧客が離れないようにして、ビジネスを維持することです。

**方法:** このテンプレートは、顧客離反の問題を**二項分類**問題として数式化します。 顧客層と顧客トランザクションという 2 つのソースからサンプル データを使用し、顧客離れを起こす可能性が高い顧客と低い顧客を分類します。
  
## <a name="predictive-maintenance"></a>予測的なメンテナンス

[予測メンテナンス テンプレート (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/README.md)

**問題:** 予測メンテナンスの目的は、過去のエラーをキャプチャし、その情報を使用してデバイスでエラーが発生するタイミングと場合を予測するメンテナンス タスクの効率を向上することです。 デバイスの陳腐化を予測する機能は、分散データまたはセンサーに依存するアプリケーションで特に重要です。 この方法は、IoT (モノのインターネット) デバイスのエラーを監視または予測するためにも適用できます。

**方法:** このソリューションでは、"稼働中のコンピューターでエラーが発生するのはいつか" という問題の答えに重点を置いています。 入力データは、航空機のエンジン用にシミュレートされているセンサーの測定値を示します。 現在の動作サイクル、設定、センサーの測定値など、エンジンの現在の動作条件を監視して取得したデータは、次の 3 種類の予測モデルの作成に使用されます。

-   **回帰モデル**: エンジンにエラーが発生するまでの時間を予測します。 サンプル モデルでは、メトリックの "残存耐用年数" (RUL) ("故障までの時間" (TTF) とも呼ばれます) を予測します。
  
-   **分類モデル**: エンジンのエラーが発生する確率が高いかどうかを予測します。
  
    **二項分類モデル**は、一定期間内にエンジンのエラーが発生するかどうかを予測します。

    **多項分類モデル**は、特定のエンジンにエラーが発生するかどうかを予測し、エラーが発生する可能性がある期間を提供します。 たとえば、特定の日について、指定した日、または指定した日から何日後に任意のデバイスでエラーが発生する可能性が高いかどうかを予測できます。

## <a name="energy-demand-forecasting"></a>エネルギー需要予測

[SQL Server R Services を使用したエネルギー需要予測テンプレート](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast-Template-with-SQL-Server-R-Services-1)

**問題:** 需要予測は、エネルギー、小売、サービスなど、さまざまな分野で重要な問題です。 正確な需要予測は、企業が運用計画、リソース割り当てを改善し、その他の重要なビジネス上の意思決定を行うのに役立ちます。 エネルギー セクターでは、エネルギー貯蔵コストを削減し、需要と供給のバランスを取るために需要予測が不可欠です。

**方法:** このテンプレートは、SQL Server R Services を使用して電力需要を予測します。 予測に使用されるモデルは、Microsoft R Server に含まれる高パフォーマンス機械学習アルゴリズムである **rxDForest**に基づくランダム フォレスト回帰モデルです。 このソリューションには、需要シミュレーター、モデルのトレーニングに必要なすべての R コードと T-SQL コード、予測の生成とレポートに使用できるストアド プロシージャが含まれています。 


## <a name="how-to-use-the-templates"></a><a name="bkmk_HowTo"></a>テンプレートの使用方法

各テンプレートに含まれるファイルをダウンロードするには、GitHub コマンドを使用するか、リンクを開いて **[Download Zip (Zip ファイルをダウンロード)]** をクリックし、すべてのファイルをコンピューターに保存します。  通常、ダウンロードしたソリューションには次のフォルダーが含まれています。
  
-   **Data**:各アプリケーションのサンプル データが含まれています。
  
-   **R**:このソリューションに必要なすべての R 開発コードが含まれています。 このソリューションには、Microsoft R Server に含まれるライブラリが必要ですが、任意の R IDE で開き、編集することができます。 この R コードは、SQL Server インスタンスに対する計算コンテキストを設定し、計算が "データベース内で" 実行されるように最適化されています。
  
-   **SQLR**:[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] などの SQL 環境で実行して、データ処理、機能エンジニアリング、モデル デプロイなど、関連するタスクを実行するストアド プロシージャを作成できる複数の .sql ファイルが含まれています。
  
    このフォルダーには、すべてのスクリプトを呼び出し、包括的な環境を作成できる PowerShell スクリプトも含まれています。 スクリプトは、必ず実際の環境似合わせて編集してください。

## <a name="next-steps"></a>次のステップ

+ [Python のチュートリアル](./python-tutorials.md)
+ [R のチュートリアル](./r-tutorials.md)