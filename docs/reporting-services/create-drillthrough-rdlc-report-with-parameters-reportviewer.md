---
title: パラメーターを含む詳細 (RDLC) レポートを作成する - ReportViewer | Microsoft Docs
description: ローカル モード レポートでパラメーターとクエリを使用してドリルスルー (RDLC) レポートを作成する方法について説明します。
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7f6e6e631b32aa7eab8d6c56c8b6f9e2cf03752f
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891202"
---
# <a name="create-drillthrough-rdlc-report-with-parameters---reportviewer"></a>パラメーターを含む詳細 (RDLC) レポートを作成する - ReportViewer
[詳細](./report-design/drillthrough-reports-report-builder-and-ssrs.md) レポートは、ユーザーが別のレポート内のリンクをクリックすることで開かれるレポートのことです。 詳細レポートには、通常、元の要約レポートに含まれるアイテムについての詳細が含まれています。 このチュートリアルでは、次のレッスンを通じて、[ローカル モード レポート](report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)でパラメーターとクエリを使用した詳細レポートを作成します。  
  
## <a name="requirements"></a>必要条件  
このチュートリアルを使用するには、 **AdventureWorks2014** サンプル データベースへのアクセス権が必要です。 **AdventureWorks2014** サンプル データベースの取得方法の詳細については、「[AdventureWorks sample databases](https://github.com/Microsoft/sql-server-samples/releases)」 (AdventureWorks のサンプル データベース) を参照してください。  
  
このチュートリアルでは、Transaction-SQL クエリおよび ADO.NET [DataSet](/dotnet/api/system.data.dataset) および [DataTable](/dotnet/api/system.data.datatable) オブジェクトを理解していることを前提とします。  
  
Visual Studio 2015 と ASP.NET Web アプリケーションを使用して、ReportViewer コントロールを含む ASP.NET Web ページを作成します。 このコントロールは、ここで作成するレポートを表示するように構成されています。 このチュートリアルでは、Microsoft Visual C# でアプリケーションを作成します。  
  
## <a name="tasks"></a>タスク  
[レッスン 1:新しい Web サイトを作成する](../reporting-services/lesson-1-create-a-new-web-site.md)  
[レッスン 2:親レポートのデータ接続とデータ テーブルを定義する](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)  
[レッスン 3:レポート ウィザードを使用して親レポートを設計する](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)  
[レッスン 4:子レポートのデータ接続とデータ テーブルを定義する](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)  
[レッスン 5: レポート ウィザードを使用して子レポートを設計する](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)  
[レッスン 6:アプリケーションに ReportViewer コントロールを追加する](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)  
[レッスン 7: 親レポートにドリルスルー アクションを追加する](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)  
[レッスン 8: データ フィルターを作成する](../reporting-services/lesson-8-create-a-data-filter.md)  
[レッスン 9: アプリケーションをビルドして実行する](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>参照  
[Reporting Services チュートリアル &#40;SSRS&#41;](../reporting-services/reporting-services-tutorials-ssrs.md)  
[レポート デザイナーを使用してレポートをデザインする &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
