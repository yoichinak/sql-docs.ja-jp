---
title: SharePoint ライブラリへの共有データ ソースのパブリッシュ | Microsoft Docs
description: SharePoint 統合モードで実行されているレポート サーバーに共有データ ソースをパブリッシュする方法について説明します。
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], publishing to a SharePoint library
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 966ed425-3ce2-4e76-8237-3c1c977954ae
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0a60966d6ba73a7669562d406b460f749303ca56
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988604"
---
# <a name="publish-a-shared-data-source-to-a-sharepoint-library"></a>SharePoint ライブラリへの共有データ ソースのパブリッシュ
  SharePoint 統合モードで実行されているレポート サーバーに共有データ ソースをパブリッシュするには、レポート デザイナーでレポート プロジェクトのプロパティを設定する必要があります。 プロジェクトのプロパティでは、サーバー、レポート、および共有データ ソースへの参照はすべて、完全修飾 URL で指定する必要があります。  
  
 また、SharePoint サイトの **メンバー** 権限または **所有者** 権限が必要です。 詳細については、「 [SharePoint モードのレポート サーバー上のパブリッシュされたレポート アイテムの URL の例 &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)」を参照してください。  
  
### <a name="to-publish-a-shared-data-source-to-a-sharepoint-site"></a>SharePoint サイトに共有データ ソースをパブリッシュするには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、既存または新規のレポート サーバー プロジェクトを開きます。  
  
2.  **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 _\<project>_ **[プロパティ ページ]** ダイアログ ボックスが開きます。  
  
3.  SharePoint サイトへのパブリッシュに使用する **[構成]** を選択します。  
  
4.  プロジェクトの共有データ ソースをパブリッシュし、以前にパブリッシュされた共有データ ソースを上書きするには、 **[OverwriteDataSources]** を **[True]** に設定します。  
  
5.  (省略可) **[TargetDataSourceFolder]** には、SharePoint ライブラリまたはライブラリ フォルダーへの URL を入力します。 たとえば、「 `https://TestServer/TestSite/Documents/DataSources` 」のように入力します。  
  
     値を指定しない場合は、 **[TargetReportFolder]** の値が使用されます。  
  
6.  **[TargetReportFolder]** に、ライブラリまたはライブラリ フォルダーの URL を入力します。 たとえば、「 `https://TestServer/TestSite/Documents/Reports` 」のように入力します。  
  
7.  **[TargetServerURL]** に、SharePoint トップレベル サイトまたはサブサイトの URL を入力します。 サイトを指定しなかった場合は、既定のトップレベル サイトが使用されます。 たとえば、「`https://servername`」、「`https://servername/site`」、「`https://servername/site/subsite`」のように指定します。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. ソリューション エクスプローラーで、パブリッシュする共有データ ソースを右クリックし、 **[配置]** をクリックします。 これで、 **[TargetDataSourceFolder]** で指定した場所にデータ ソースがパブリッシュされます。 配置エラーは出力ウィンドウに表示されます。  
  
    > [!NOTE]  
    >  共有データ ソースを SharePoint サイトにパブリッシュすると、ファイル名拡張子が .rsds に変更されます。 共有データ ソースの編集と管理は、SharePoint サイト上で直接行うことができます。 詳細については、「[共有データ ソースを作成および管理する &#40;Reporting Services の SharePoint 統合モード&#41;](/previous-versions/sql/)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SharePoint ライブラリへのレポートのパブリッシュ](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [SharePoint モードのレポート サーバー上のパブリッシュされたレポート アイテムの URL の例 &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [[プロパティ ページ] ダイアログ ボックス](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [配置プロパティを設定する (Reporting Services)](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [レポート サーバーへのレポートのパブリッシュ](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [レポートで Office Data Connection &#40;.odc&#41; を使用する &#40;Reporting Services の SharePoint 統合モード&#41;](../../reporting-services/report-data/use-an-office-data-connection-odc-with-reports.md)  
  
