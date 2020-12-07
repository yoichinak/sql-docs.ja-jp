---
title: レポート データセット | Microsoft Docs
description: レポート データセットについて説明します。たとえば、データセットには、データ ソースから特定のデータを取得するために必要な情報が含まれています。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: f2e42303-e355-4c1f-bb3b-3338fbdd230d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7360e1490edc769d75299cdbf8d21aa98a56245a
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891672"
---
# <a name="report-datasets-ssrs"></a>レポート データセット (SSRS)
  データをレポートに追加するには、データセットを作成します。 各データセットは、データ ソースに対するクエリ コマンドの実行によって取得された結果セットを表します。 結果セットの列はフィールド コレクションです。 結果セット内の行がデータです。 データセットに実際のデータは格納されていません。 データセットには、データ ソースから特定のデータを取得するために必要な情報が含まれています。  
  
 データセットには、埋め込みと共有の 2 種類があります。 埋め込みデータセットは、レポート内で定義され、そのレポートでのみ使用されます。 共有データセットはレポート サーバーまたは SharePoint サイトで定義され、複数のレポートで使用できます。 レポート ビルダーでは、共有データセット モードで共有データセット、レポート デザイナー モードで埋め込みデータセットを作成できます。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のレポート デザイナーでは、共有データセットをプロジェクトの一部として、埋め込みデータセットをレポートの一部として作成できます。  
  
-   **埋め込みデータセット:** ワークシート内で直接データを操作する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel などのアプリケーションとは異なり、レポート ビルダーやレポート デザイナーでは、レポートの処理時に取得されるデータを表すメタデータを操作します。 埋め込みデータセットを作成するには、データ ソースを選択し、クエリを指定します。 データセットを作成した後、レポート データ ペインを使用してフィールド コレクションを表示します。 データセットのデータは、テーブルやグラフのようなデータ領域内に表示できます。 各データ領域内で、グループ化、フィルター処理、および並べ替えを行ってデータを編成できます。 レポートのレイアウトをデザインしたら、レポートを実行して実際のデータを表示します。  
  
     次の図では、レポート データ ペインに、 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]という名前のデータ ソース、DataSet1 という名前のデータセット、およびデータセット フィールド コレクション内の 5 つのフィールドが表示されています。 レイアウト ペインには、一番上の行が列ヘッダーであり、一番下の行にテキストを含むテーブル セルが含まれるテーブルが表示されています。 プレースホルダー テキスト [Name] は、フィールド名のメタデータです。 レポートを実行すると、プレースホルダー テキストは実際のデータ値に置き換えられます。 テーブルは、すべてのデータを表示するために、必要に応じて拡張されます。  
  
     ![rs_DataDesignandPreview](../../reporting-services/report-data/media/rs-datadesignandpreview.gif "rs_DataDesignandPreview")  
  
-   **共有データセット:** 複数のレポートで同じデータセットを使用する場合は、共有データセットを作成します。 共有データセットを作成してレポート サーバーまたは SharePoint サイトに保存するには、レポート ビルダーの共有データセット デザイン ビューを使用します。 サーバーまたはサイトに配置できるプロジェクトの一部として共有データセットを作成するには、レポート デザイナーを使用します。  
  
     次の図は、レポート ビルダーの共有データセット デザイン ビューを示しています。 データ接続、データセット プロパティ、クエリ、およびフィルターを選択または変更し、必要に応じてフィルターをパラメーターとしてマークして、クエリ結果を表示できます。 変更内容は、サーバーまたはサイトに再び保存します。  
  
     ![rs_SharedDatasetDesignMode](../../reporting-services/report-builder/media/rs-shareddatasetdesignmode.gif "rs_SharedDatasetDesignMode")  
  
 詳細については、「[埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/embedded-and-shared-datasets-report-builder-and-ssrs.md)」および「[埋め込みおよび共有のデータ接続またはデータ ソース &#40;レポート ビルダーおよび SSRS&#41;](./data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」を参照してください。  
  
 また、レポート パーツ (レポート パーツが依存するデータセットが含まれています) を追加することによって、データセットをレポートに追加することもできます。 [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータを表示するレポートの作成方法については、「[チュートリアル: 基本的な表レポートの作成 &#40;レポート ビルダー&#41;](../../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md)」を参照してください。 独自のデータが含まれたレポートの作成方法については、「[チュートリアル:オフラインでのクイック グラフ レポートの作成 &#40;レポート ビルダー&#41;](../../reporting-services/report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="adding-report-data"></a><a name="Methods"></a> レポート データの追加  
 レポート ビルダーでは、次の方法でレポート データを追加できます。  
  
-   レポート パーツをレポート サーバーからレポートに追加します。 各レポート パーツは自己完結型で、依存データセットを含んでいます。 データセットは事前に定義されています。  
  
-   テーブル/マトリックス、グラフ、マップの各種ウィザードを使用します。 ウィザードからは、共有データ ソースと共有データセットを選択するか、新しいデータセットを作成し、レポートのデザインを続行できます。  
  
-   レポート サーバーから共有データセットを追加します。 共有データセットは事前に定義されており、事前に定義されたデータ ソースから使用するデータを指定します。 共有データセットをレポートに追加すると、共有データセット定義を参照するデータセット参照が追加されます。  
  
 レポート ビルダーまたはレポート デザイナーでは、次の方法でデータを追加できます。  
  
-   共有データ ソースに基づいた埋め込みデータセットを追加する。  
  
-   埋め込みデータ ソースに基づいた埋め込みデータセットを追加する。  
  
> [!NOTE]  
>  レポート サーバーでは、共有アイテムは、個別に、またはパブリッシュされるフォルダーから権限を継承することによって、セキュリティで保護されます。 保存した共有データセットに他のユーザーがアクセスできるようにするには、権限を付与する方法を理解する必要があります。 詳細については、「[セキュリティ (レポート ビルダー)](../../reporting-services/report-builder/security-report-builder.md)」または「[共有データセット アイテムをセキュリティで保護する](../../reporting-services/security/secure-shared-dataset-items.md)」を参照してください。  
  
 レポートにデータを追加した後、データ領域に基づくレポート ページのデータの編成、レポート パーツの変更、および他のユーザーとの変更内容の共有を行うことができます。また、レポートに表示されるデータの制限または並べ替えをユーザーが行うことができるように設定できます。 詳細については、次の関連項目を参照してください。  
  
-   [テーブル、マトリックス、および一覧 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
-   [グラフ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
-   [スパークラインとデータ バー (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
-   [インジケーター &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
-   [レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [レポート パーツ &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)  
  
-   [データのフィルター、グループ化、および並べ替え &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
##  <a name="adding-data-with-report-parts"></a><a name="QuickStart"></a> レポート パーツによるデータの追加  
 レポート パーツには、そのレポート パーツが依存するデータセットが含まれています。 これらのデータセットは、レポート サーバーで使用可能な共有データ ソースに基づいて構築されます。 レポート ビルダーでレポート パーツをレポートに追加すると、手動で追加した場合と同様に、依存データセットもレポートに追加されます。 たとえば、事前に定義されたグラフにデータセットが含まれているとします。 データを表示するには、レポートをプレビューします。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
 レポート パーツ、共有データ ソース、および共有データセットは事前に定義され、レポート サーバーに保存されます。 これらにアクセスするには、レポート サーバーに接続して、サーバー モードでレポート ビルダーを開く必要があります。 レポート サーバーに対する書き込み権限を持っている場合は、これらを使用して独自の新しいバージョンを作成できます。  
  
-   詳細については、「[レポート パーツ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)」および「[レポート デザイナーでのレポート パーツ (SSRS)](../../reporting-services/report-design/report-parts-in-report-designer-ssrs.md)」を参照してください。  
  
  
##  <a name="queries-and-query-designers"></a><a name="Queries"></a> クエリとクエリ デザイナー  
 データ ソースからどのデータを使用するかを指定するには、クエリ コマンドを作成します。 データ ソースの種類ごとに、クエリの作成に役立つ *クエリ デザイナー* が関連付けられています。 クエリ デザイナーには、グラフィカルなものとテキスト ベースのものがあります。 グラフィカル クエリ デザイナーでは、外部データ ソースのデータを表すメタデータを表示し、フィールドやエンティティをクエリ デザイン領域にドラッグしてクエリを対話的に構築します。 テキスト ベースのクエリ デザイナーでは、外部データ ソースによってサポートされるクエリ構文でクエリを書き込んだりインポートしたりします。  
  
 クエリ デザイナーで、サンプル データを表示し、クエリ コマンド構文を検証するクエリを実行できます。 結果セットの列名は、レポート データ ペインに表示されるフィールド名になります。 結果セットは、データの各行の値の数と同じ数の列と行を持つ、1 つの行セットです。 1 つのクエリからの複数の結果セットはサポートされていません。 一定の数の列を含まず、各行で異なる数のデータ値を生成する可能性がある不規則階層は、サポートされていません。  
  
 クエリを実行するには、デザイン時の資格情報が必要です。 詳細については、「[レポート データ ソースに関する資格情報と接続情報を指定する](specify-credential-and-connection-information-for-report-data-sources.md)」または「[データ接続文字列を作成する - レポート ビルダーおよび SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」を参照してください。  
  
 データ拡張機能と外部データ ソースの間の通信は、データ プロバイダーによって処理されます。 サポートされているクエリ コマンド構文、クエリ パラメーター、結果セット内の値のデータ型は、各データ プロバイダーによって決まります。 詳細については、データ拡張機能の特定の型についてのトピックと、「[クエリ デザイン ツール &#40;SSRS&#41;](query-design-tools-ssrs.md)」をご覧ください。  
  
  
##  <a name="how-to-topics"></a><a name="HowTo"></a> 操作方法に関するトピック  
 [データ接続を追加および確認する (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [共有データセットまたは埋め込みデータセットの作成 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [レポート データ ペインでのフィールドの追加、編集、更新 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
 [リレーショナル クエリ デザイナーでのクエリの作成 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)  
  
 [多次元データのパラメーター値の非表示データセットの表示 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md)  
  
 [データセットへのフィルターの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
 [データ領域にデータがないことを示すメッセージの設定 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [クエリ パラメーターのレポート パラメーターへの関連付け &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md)  
  
 [Analysis Services の MDX クエリ デザイナーでのパラメーターの定義 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md)  
  
  
##  <a name="in-this-section"></a><a name="Section"></a> トピックの内容  
 [レポート ビルダーのレポート パーツおよびデータセット](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)  
  
 [データ接続文字列を作成する - レポート ビルダーおよび SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
 [レポート データ ソースに関する資格情報と接続情報を指定する](specify-credential-and-connection-information-for-report-data-sources.md)  
  
 [レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
 [データセット フィールド コレクション (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
## <a name="see-also"></a>参照  
 [レポート デザイン ビュー (レポート ビルダー)](../../reporting-services/report-builder/report-design-view-report-builder.md)   
 [Reporting Services の概念 (SSRS)](../reporting-services-concepts-ssrs.md)
  
