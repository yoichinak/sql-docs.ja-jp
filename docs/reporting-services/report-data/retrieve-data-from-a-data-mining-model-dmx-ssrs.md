---
title: データ マイニング モデル (DMX) からデータを取得する | Microsoft Docs
description: SQL Server Analysis Services (SSAS) データ マイニング モデルのデータをレポートで使用する方法について説明します。
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- retrieving report data
- datasets [Reporting Services], with DMX queries
- datasets [Reporting Services], Analysis Services
- queries [Reporting Services], data mining prediction
ms.assetid: d9cd3624-1594-4707-8887-55437dd7e07c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8e8e6d382e1041e4b15b089d3d6f0ef2a2bfbf6c
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890832"
---
# <a name="retrieve-data-from-a-data-mining-model-dmx-ssrs"></a>データ マイニング モデル (DMX) からデータを取得する (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ マイニング モデルのデータをレポートで使用するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースと 1 つ以上のレポート データセットを定義する必要があります。 データ ソース定義を作成する場合、クライアント コンピューターからデータ ソースにアクセスできるように接続文字列と資格情報を指定する必要があります。  
  
 単一のレポートで使用するように埋め込みデータ ソースの定義を作成することも、複数のレポートで使用できる共有データ ソースの定義を作成することもできます。 このトピックでは、埋め込みデータ ソースを作成する手順について説明します。 共有データ ソースの詳細については、「[埋め込みデータ接続/データ ソースおよび共有データ接続/データ ソース (レポート ビルダーおよび SSRS)](./data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)」および「[共有データ ソースを作成、変更、および削除する (SSRS)](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースを作成したら、1 つ以上のデータセットを作成できます。 データセットごとに、データ マイニング予測式 (DMX) クエリ デザイナーを使用して、フィールド コレクションを指定する DMX クエリを作成します。 詳細については、「 [Analysis Services の DMX クエリ デザイナーのユーザー インターフェイス](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)」をご覧ください。  
  
 データセットを作成すると、そのデータセットの名前がデータ ソースの下のノードとしてレポート データ ペインに表示されます。  
  
 レポートをパブリッシュした後、レポートをレポート サーバーで実行するときに、データを取得するための権限が有効な状態になるように、データ ソースの資格情報を変更する必要が生じる場合があります。  
  
### <a name="to-create-an-embedded-microsoft-sql-server-analysis-services-data-source"></a>埋め込み Microsoft SQL Server Analysis Services データ ソースを作成するには  
  
1.  ツール バーのレポート データ ペインで、 **[新規作成]** 、 **[データ ソース]** の順にクリックします。  
  
2.  **[データ ソースのプロパティ]** ダイアログ ボックスの **[名前]** ボックスに名前を入力するか、既定の名前をそのまま使用します。  
  
3.  **[埋め込み接続]** が選択されていることを確認します。  
  
4.  **[種類]** ボックスで、 **[Microsoft SQL Server Analysis Services]** を選択します。  
  
5.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースに使用する接続文字列を指定します。  
  
     データ ソースへの接続に使用する接続情報および資格情報については、データベース管理者に問い合わせてください。 ローカル クライアント上のサンプル [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)] データベースを指定する接続文字列の例を次に示します。  
  
    ```  
    Data Source=localhost;Initial Catalog=AdventureWorksDW2012  
    ```  
  
6.  **[資格情報]** をクリックします。  
  
     データ ソースへの接続に使用する資格情報を設定します。 詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)」をご覧ください。  
  
    > [!NOTE]  
    >  データ ソース接続をテストするには、 **[編集]** をクリックします。 **[接続プロパティ]** ダイアログ ボックスで、 **[接続テスト]** をクリックします。 テストが成功すると "接続テストに成功しました。" というメッセージが表示されます。 テストが失敗すると、その原因に関する詳しい情報を記載した警告メッセージが表示されます。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     データ ソースがレポート データ ペインに表示されます。  
  
### <a name="to-create-a-dataset-for-a-microsoft-sql-server-analysis-services"></a>Microsoft SQL Server Analysis Services のデータセットを作成するには  
  
1.  **[レポート データ]** ペインで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースに接続するデータ ソースの名前を右クリックし、 **[データセットの追加]** をクリックします。  
  
2.  **[データセットのプロパティ]** ダイアログ ボックスで、 **[名前]** ボックスに名前を入力します。  
  
3.  **[データ ソース]** ボックスに表示された名前が、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データ ソースに接続するデータ ソースの名前であることを確認します。  
  
4.  **[クエリ デザイナー]** をクリックしてグラフィカル クエリ デザイナーを開き、クエリを対話形式で作成します。 クエリ デザイナーが MDX モードで開いた場合は、ツール バーの **[コマンドの種類 DMX]** (![DMX クエリ言語ビューに変更](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "DMX クエリ言語ビューへの変更")) をクリックして、データ マイニング クエリ デザイナーに切り替えます。 詳細については、「 [Analysis Services の DMX クエリ デザイナーのユーザー インターフェイス](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)」をご覧ください。  
  
     代わりに、既存の DMX クエリを別のレポートからインポートするには、 **[インポート]** をクリックし、DMX クエリを使用して .rdl ファイルに移動します。 .dmx ファイルからクエリをインポートすることはできません。  
  
5.  クエリを作成して実行した後、サンプルの結果を表示するには **[OK]** をクリックします。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     データセットとそのフィールド コレクションがレポート データ ペインのデータ ソース ノードの下に表示されます。  
  
## <a name="see-also"></a>参照  
 [DMX のための Analysis Services の接続の種類 &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)   
 [データ接続文字列を作成する - レポート ビルダーおよび SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [データセット フィールド コレクション &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [レポート埋め込みデータセットと共有データセット (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
