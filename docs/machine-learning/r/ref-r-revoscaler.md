---
title: RevoScaleR R パッケージ
description: RevoScaleR は Microsoft が提供する R パッケージであり、分散コンピューティング、リモート計算コンテキスト、ハイパフォーマンス データ サイエンス アルゴリズムをサポートしています。 また、データ インポート、データ変換、概要作成、視覚化、分析もサポートしています。 このパッケージは、SQL Server Machine Learning Services と SQL Server 2016 R Services に含まれています。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0095984a9358f742147e84e69847ab32781cab07
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956887"
---
# <a name="revoscaler-r-package-in-sql-server-machine-learning-services"></a>RevoScaleR (SQL Server Machine Learning Services の R パッケージ)

[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

**RevoScaleR** は Microsoft が提供する R パッケージであり、分散コンピューティング、リモート計算コンテキスト、ハイパフォーマンス データ サイエンス アルゴリズムをサポートしています。 また、データ インポート、データ変換、概要作成、視覚化、分析もサポートしています。 このパッケージは、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) と [SQL Server 2016 R Services](sql-server-r-services.md) に含まれています。

基本の R 関数とは異なり、RevoScaleR の演算は、大規模なデータセットに対しての実行、並列での実行、分散ファイル システムでの実行が可能です。 関数は、チャンクを使用し、演算の完了時、結果を再び組み立てることで、メモリに収まらないデータセットに対して実行できます。

RevoScaleR 関数には、rx** または **Rx** というプレフィックスが付いており、簡単に識別できるようになっています。

RevoScaleR は、分散データ サイエンスのプラットフォームとして機能します。 たとえば、[MicrosoftML](/machine-learning-server/r/concept-what-is-the-microsoftml-package) の最新式アルゴリズムと共に RevoScaleR の計算コンテキストと変換を使用できます。 [rxExec](/machine-learning-server/r-reference/revoscaler/rxexec) を使用し、基本の R 関数を並列実行することもできます。

## <a name="full-reference-documentation"></a>完全なリファレンス ドキュメント

**RevoScaleR** パッケージは、複数の Microsoft 製品で配布されていますが、このパッケージを SQL Server または別の製品のどちらで取得しても、使用方法は同じです。 これらの関数は同じであるため、[個々の RevoScaleR 関数のドキュメント](/machine-learning-server/r-reference/revoscaler/revoscaler)は Microsoft Machine Learning Server の [R リファレンス](/machine-learning-server/r-reference/introducing-r-server-r-package-reference)の下でのみ公開されています。 製品固有の動作が存在する場合、関数のヘルプ ページにその相違点が示されます。

## <a name="versions-and-platforms"></a>バージョンとプラットフォーム

**RevoScaleR** パッケージは R 3.4.3 に基づいており、次のいずれかの Microsoft 製品またはダウンロードをインストールした場合にのみ利用できます。

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server Machine Learning サービス](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 以降](/machine-learning-server/)
+ [Microsoft R Client](set-up-a-data-science-client.md)

> [!NOTE]
> 完全な製品リリース バージョンは、SQL Server 2017 では Windows のみです。 [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md) の **RevoScaleR** では、Windows と Linux の両方がサポートされています。

## <a name="functions-by-category"></a>カテゴリ別の関数

このセクションでは、関数をカテゴリ別に一覧表示し、それぞれの使用方法について説明します。 [目次](/machine-learning-server/r-reference/introducing-r-server-r-package-reference)を使用して関数をアルファベット順に検索することもできます。

## <a name="1-data-source-and-compute"></a>1 - データ ソースと計算

**RevoScaleR** には、データ ソースを作成したり、場所、つまり、計算が実行される場所である*計算コンテキスト*を設定したりするための関数が含まれています。 データ ソース オブジェクトは、接続文字列と一緒に必要な一連のデータを指定するコンテナーです。テーブル、ビュー、またはクエリとして定義されます。 ストアド プロシージャの呼び出しはサポートされていません。 SQL Server シナリオに関連する関数を次の表に示します。

SQL Server と R では、場合によっては異なるデータ型が使用されます。 SQL のデータ型と R のデータ型の対応表が必要であれば、[R と SQL のデータ型マッピング](r-libraries-and-data-types.md) ページを参照してください。

| 機能| 説明|
| ------- | ---------- |
| [RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver) |  SQL Server 計算コンテキスト オブジェクトを作成し、リモート インスタンスに計算をプッシュします。 一部の **RevoScaleR** 関数では、計算コンテキストが引数として受け取られます。 |
|[rxGetComputeContext / rxSetComputeContext](/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) | アクティブな計算コンテキストを取得または設定します。 |
| [RxSqlServerData](/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) | SQL Server クエリまたはテーブルに基づいてデータ オブジェクトを作成します。 |
| [RxOdbcData](/machine-learning-server/r-reference/revoscaler/rxodbcdata) | ODBC 接続に基づいてデータ ソースを作成します。 |
| [RxXdfData](/machine-learning-server/r-reference/revoscaler/rxxdfdata) | ローカル XDF ファイルに基づいてデータ ソースを作成します。 XDF ファイルはしばしば、メモリ内データをディスクにオフロードするために使用されます。 XDF ファイルが役立つのは、扱うデータ容量がデータベースから 1 回で転送できない場合や、メモリに収まりきらない場合です。 たとえば、大容量データを定期的にデータベースからローカル ワークステーションに移す場合、R 操作ごとにデータベースに対してクエリを繰り返し実行する代わりに、XDF ファイルを一種のキャッシュとして使用してデータをローカルに保存し、R ワークスペースでそのデータを処理できます。|

> [!TIP]
> データ ソースまたは計算コンテキストの概念を初めて使用する場合、Microsoft Machine Learning Server ドキュメントで[分散コンピューティング](/machine-learning-server/r/how-to-revoscaler-distributed-computing)から始めることをお勧めします。

### <a name="perform-ddl-statements"></a>DDL ステートメントの実行

インスタンスとデータベースに対する必要なアクセス許可がある場合は、DDL ステートメントを R から実行できます。 次の関数では、ODBC 呼び出しを使用し、DDL ステートメントを実行したり、データベース スキーマを取得したりします。

| 機能| 説明|
| ------- | ---------- |
| [rxSqlServerTableExists と rxSqlServerDropTable](/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) | [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] テーブルを削除するか、データベース テーブルまたはオブジェクトの存在を確認します。 |
| [rxExecuteSQLDDL](/machine-learning-server/r-reference/revoscaler/rxexecutesqlddl) | データベース オブジェクトを定義または操作するデータ定義言語 (DDL) コマンドを実行します。 この関数ではデータを返すことができず、オブジェクト スキーマまたはメタデータを取得または変更する目的でのみ使用されます。|

## <a name="2-data-manipulation-etl"></a>2 - データ操作 (ETL)

データ ソース オブジェクトを作成したら、そのオブジェクトを使用し、それにデータを読み込んだり、データを変換したり、指定の宛先に新しいデータを書き込んだりできます。 ソースのデータのサイズによりますが、データ ソースの一部としてバッチ サイズを定義し、データをチャンク単位で動かすことができます。

| 機能 | 説明 |
|----------|-------------|
| [rxOpen-methods](/machine-learning-server/r-reference/revoscaler/rxopen-methods) | データ ソースを利用できるかどうかを確認します。データ ソースを開いたり、閉じたりします。ソースからデータを読み取ります。ターゲットにデータを書き込みます。データ ソースを閉じます。|
| [rxImport](/machine-learning-server/r-reference/revoscaler/rximport) | データ ソースからファイル ストレージまたはデータ フレームにデータを移動します。|
| [rxDataStep](/machine-learning-server/r-reference/revoscaler/rxdatastep) | データをデータ ソース間で移動させるとき、データを変換します。|

<a name="graphing-functions"></a>

## <a name="3-graphing-functions"></a>3 - グラフ作成関数

| 関数名 | 説明 |
|---------------|-------------|
|[rxHistogram](/machine-learning-server/r-reference/revoscaler/rxhistogram)  |データからヒストグラムを作成します。 | 
|[rxLinePlot](/machine-learning-server/r-reference/revoscaler/rxlineplot) |データから折れ線グラフを作成します。 | 
|[rxLorenz](/machine-learning-server/r-reference/revoscaler/rxlorenz)  |プロットできるローレンツ曲線を計算します。 | 
|[rxRocCurve](/machine-learning-server/r-reference/revoscaler/rxroc)  |実際のデータと予測されたデータから ROC 曲線を計算し、プロットします。 | 

<a name="statistics-functions"></a>

## <a name="4-descriptive-statistics"></a>4 - 説明的統計

| 関数名 | 説明 |
|---------------|-------------|
|[rxQuantile](/machine-learning-server/r-reference/revoscaler/rxquantile) <sup>*</sup> |並べ替えなしで、.xdf ファイルとデータ フレームのおおよその変位値を計算します。 | 
|[rxSummary](/machine-learning-server/r-reference/revoscaler/rxsummary) <sup>*</sup> |グループごとの計算を含む、データの基本概要統計。 .xdf ファイルにグループ別の計算を書き込むことはできません。 | 
|[rxCrossTabs](/machine-learning-server/r-reference/revoscaler/rxcrosstabs) <sup>*</sup> |数式に基づくデータのクロス集計。 | 
|[rxCube](/machine-learning-server/r-reference/revoscaler/rxcube) <sup>*</sup> |キューブの結果を返す効率的な表現のために設計された数式ベースの代替クロス集計。 .xdf ファイルに出力を書き込むことはできません。 | 
|[rxMarginals](/machine-learning-server/r-reference/revoscaler/rxmarginals)  |クロス集計のマージナル概要。 | 
|[as.xtabs](/machine-learning-server/r-reference/revoscaler/as.xtabs)  |クロス集計結果を xtab オブジェクトに変換します。 | 
|[rxChiSquaredTest](/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |xtabs オブジェクトに対してカイ 2 乗検定を実行します。 小規模のデータ セットと共に使用し、データをチャンクしません。 | 
|[rxFisherTest](/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |xtab オブジェクトに対してフィッシャーの正確確率検定を実行します。 小規模のデータ セットと共に使用し、データをチャンクしません。 | 
|[rxKendallCor](/machine-learning-server/r-reference/revoscaler/rxchisquaredtest)  |xtabs オブジェクトを使用してケンドールの順位相関係数を計算します。 | 
|[rxPairwiseCrossTab](/machine-learning-server/r-reference/revoscaler/rxpairwisecrosstab)  |xtab オブジェクトの行と列のペアの組み合わせに関数を適用します。 | 
|[rxRiskRatio](/machine-learning-server/r-reference/revoscaler/rxriskratio)  |2 つずつの xtab オブジェクトに対する相対的リスクを計算します。 | 
|[rxOddsRatio](/machine-learning-server/r-reference/revoscaler/rxriskratio)  |2 つずつの xtab オブジェクトに対するオッズ比を計算します。 | 

<sup>*</sup> このカテゴリで最もよく使われる関数を示します。

<a name="prediction-functions"></a>

## <a name="5-prediction-functions"></a>5 - 予測関数

| 関数名 | 説明 |
|---------------|-------------|
|[rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod) <sup>*</sup> |線形モデルをデータに適合させます。 | 
|[rxLogit](/machine-learning-server/r-reference/revoscaler/rxlogit) <sup>*</sup> |ロジスティック回帰モデルをデータに適合させます。 | 
|[rxGlm](/machine-learning-server/r-reference/revoscaler/rxglm) <sup>*</sup> |一般化線形モデルをデータに適合させます。 | 
|[rxCovCor](/machine-learning-server/r-reference/revoscaler/rxcovcor) <sup>*</sup> |一連の変数の共分散、相関、平方和/クロス積のマトリックスを計算します。 | 
|[rxDTree](/machine-learning-server/r-reference/revoscaler/rxdtree) <sup>*</sup> |分類ツリーまたは回帰ツリーをデータに適合させます。 | 
|[rxBTrees](/machine-learning-server/r-reference/revoscaler/rxbtrees) <sup>*</sup> |確率勾配ブースティング アルゴリズムを使用し、分類または回帰のデシジョン フォレストをデータに合わせます。 | 
|[rxDForest](/machine-learning-server/r-reference/revoscaler/rxdforest) <sup>*</sup> |分類または回帰のデシジョン ツリーをデータに合わせます。 | 
|[rxPredict](/machine-learning-server/r-reference/revoscaler/rxPredict) <sup>*</sup> |適合モデルの予測を計算します。 出力は XDF データ ソースにする必要があります。 | 
|[rxKmeans](/machine-learning-server/r-reference/revoscaler/rxkmeans) <sup>*</sup> |K-Means クラスタリングを実行します。 | 
|[rxNaiveBayes](/machine-learning-server/r-reference/revoscaler/rxnaivebayes) <sup>*</sup> |単純ベイズ分類を実行します。 | 
|[rxCov](/machine-learning-server/r-reference/revoscaler/rxcovcor) |一連の変数の共分散マトリックスを計算します。 | 
|[rxCor](/machine-learning-server/r-reference/revoscaler/rxcovcor)  |一連の変数の相関マトリックスを計算します。 | 
|[rxSSCP](/machine-learning-server/r-reference/revoscaler/rxcovcor)  |一連の変数の平方和/クロス積マトリックスを計算します。 | 
|[rxRoc](/machine-learning-server/r-reference/revoscaler/rxroc)  |二項分類器システムの実際の値と予測値を使用した受信者操作特性 (ROC) 計算。 | 

<sup>*</sup> このカテゴリで最もよく使われる関数を示します。


## <a name="how-to-work-with-revoscaler"></a>RevoScaleR の使用方法

**RevoScaleR** 内の関数は、ストアド プロシージャにカプセル化された R コードで呼び出すことができます。 ほとんどの開発者は、**RevoScaleR** ソリューションをローカルでビルドし、完成した R コードを展開の練習としてストアド プロシージャに移行します。

ローカルで実行するとき、通常、コマンド ラインまたは R 開発環境から R スクリプトを実行し、いずれかの **RevoScaleR** 関数で SQL Server 計算コンテキストを指定します。 コード全体または個々の関数に対してリモート計算コンテキストを使用できます。 たとえば、最新のデータを使用してデータの移動を回避するために、モデルのトレーニングをサーバーにオフロードすることがあります。

R スクリプトをストアド プロシージャ [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 内にカプセル化する準備ができたら、入力と出力が明確に定義された 1 つの関数としてコードを書き直すことをお勧めします。 

## <a name="see-also"></a>関連項目

+ [R のチュートリアル](../tutorials/r-tutorials.md)
+ [計算コンテキストの使用方法](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [SQL 開発者向け R:モデルのトレーニングと運用化](../tutorials/r-taxi-classification-introduction.md)
+ [GitHub 上の Microsoft 製品サンプル](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [R リファレンス (Microsoft Machine Learning Server)](/machine-learning-server/r-reference/introducing-r-server-r-package-reference)