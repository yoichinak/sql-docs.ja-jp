---
title: レッスン 1:レポート サーバー プロジェクトを作成する | Microsoft Docs
description: このレッスンでは、レポート デザイナーを使用して、レポート サーバー プロジェクトとレポート定義 (.rdl) ファイルを作成します。
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ac84fb8cf355103b28fbac8f5411943aa4ee51a8
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2020
ms.locfileid: "92679053"
---
# <a name="lesson-1-create-a-report-server-project-reporting-services"></a>レッスン 1:レポート サーバー プロジェクトを作成する (Reporting Services)

このレッスンでは、 *レポート デザイナー* を使用して、 *レポート サーバー プロジェクト* と *レポート定義 (.rdl)* ファイルを作成します。

> [!NOTE]
> [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] は、ビジネス インテリジェンス ソリューションを作成するための [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 環境です。 SSDT は、レポート デザイナー作成環境を標準装備しています。この環境では、 [!INCLUDE[ssrsnoversion_md](../includes/ssrsnoversion-md.md)] のページ分割されたレポート定義、共有データ ソース、共有データセット、およびレポート パーツを開けるほか、変更、プレビュー、保存、配置ができます。

レポート デザイナーを使用してレポートを作成すると、レポート ファイルと、レポートで使用されるその他のリソース ファイルを含むレポート サーバー プロジェクトが作成されます。

## <a name="to-create-a-report-server-project"></a>レポート サーバー プロジェクトを作成するには
  
1. **[ファイル]** メニューから、 **[新規]**  >  **[プロジェクト]** の順に選択します。  

    ![Visual Studio のスクリーンショット。[ファイル] > [新規] > [プロジェクト] の順に選択されています。](../reporting-services/media/ssrs-ssdt-file-01-new-project.png)
  
2. 左端の列の **[インストール済み]** の下で、 **[Reporting Services]** を選択します。 場合によっては、 **[Business Intelligence]** の下にあることもあります。

    ![[新しいプロジェクト] ダイアログ ボックスのスクリーンショット。[Reporting Services] が選択され、レポート サーバー プロジェクト テンプレートが強調表示されています。](../reporting-services/media/lesson-1-creating-a-report-server-project-reporting-services/select-report-server-project-template.png)

    > [!IMPORTANT]
    > VS の場合、左の列に [Reporting Services] が表示されていない場合は、SSDT ワークロードをインストールしてレポート デザイナーを追加します。 **[ツール]** メニューから **[ツールと機能を取得]** を選択し、表示されたワークロードから **[SQL Server Data Tools]** を選択します。 中央の列に [Reporting Services] オブジェクトが表示されていない場合は、Reporting Services 拡張機能を追加します。 **[ツール]** メニューから、 **[拡張機能と更新プログラム]**  >  **[オンライン]** の順に選択します。 中央の列で、表示された拡張機能から **[Microsoft Reporting Services Projects]**  >  **[ダウンロード]** を選択します。 SSDT については、[SQL Server Data Tools (SSDT) のダウンロード](../ssdt/download-sql-server-data-tools-ssdt.md)に関する記事を参照してください。 Visual Studio 2019 で、これまでの手順がうまくいかなかった場合は、[Microsoft Reporting Service Project 拡張機能](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftReportProjectsforVisualStudio)をインストールしてみてください。


3. **[新しいプロジェクト]** ダイアログ ボックスの中央の列で、 **[レポート サーバー プロジェクト]** アイコン &nbsp;&nbsp;![ssrs_ssdt_report_server_project](media/ssrs-ssdt-report-server-project.png)&nbsp;&nbsp; を選択します。

4. **[名前]** ボックスに、プロジェクトの名前として「Tutorial」を入力します。 既定では、 **[場所]** ボックスに "Documents\Visual Studio 20xx\Projects\" フォルダーへのパスが表示されます。 レポート デザイナーにより Tutorial という名前のフォルダーがこのパスの下に作成され、このフォルダー内に Tutorial プロジェクトが作成されます。 プロジェクトが VS ソシューションに属していない場合は、VS によりソリューション ファイル (.sln) も作成されます。

5. **[OK]** を選択すると、プロジェクトが作成されます。 Tutorial プロジェクトが右側の **[ソリューション エクスプローラー]** ウィンドウに表示されます。
  
## <a name="creating-a-report-definition-file-rdl"></a>レポート定義ファイル (RDL) を作成する  
  
1. **[ソリューション エクスプローラー]** ウィンドウで、 **[レポート]** フォルダーを右クリックします。 **[ソリューション エクスプローラー]** ウィンドウが表示されない場合は、 **[表示]** メニュー > **[ソリューション エクスプローラー]** の順に選択します。

2. **[追加]**  >  **[新しい項目]** の順に選択します。

    ![ソリューション エクスプローラーのスクリーンショット。[レポート] > [追加] > [新しい項目] の順に選択されています。](../reporting-services/media/ssrs-ssdt-add-report.png)

3. **[新しい項目の追加]** ウィンドウで、 **[レポート]** アイコンを選択します。

4. **[名前]** ボックスに「Sales Orders.rdl」と入力します。

5. **[新しい項目の追加]** ダイアログ ボックスの右下にある **[追加] ボタン** を選択して、処理を完了します。 レポート デザイナーが開き、デザイン ビューで Sales Orders レポート ファイルが表示されます。

    ![Visual Studio のスクリーンショット。デザイン ビューでレポート デザイナーと Sales Orders レポートが表示されています。](media/ssrs-ssdt-01-new-report-designer.png)

## <a name="next-steps"></a>次のステップ

これまで、Tutorial レポート プロジェクトと Sales Orders レポートを作成しました。 残りのレッスンでは、次の方法について学習します。

- レポートのデータ ソースを構成する。
- データ ソースからデータセットを作成する。
- レポートのレイアウトをデザインし書式を設定する。

「[レッスン 2: 接続情報の指定 &#40;Reporting Services&#41;](../reporting-services/lesson-2-specifying-connection-information-reporting-services.md)」に進みます。
