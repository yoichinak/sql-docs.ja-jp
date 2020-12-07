---
title: 'レッスン 6: アプリケーションに ReportViewer コントロールを追加する | Microsoft Docs'
description: レポート ウィザードを使用して子レポートを設計した後に、Web サイト アプリケーションに ReportViewer コントロールを追加する方法について説明します。
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: f9492a97-5609-4059-ae76-0fba111d4968
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3a1874b3253136a12973a60e6619e199995b5314
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891552"
---
# <a name="lesson-6-add-a-reportviewer-control-to-the-application"></a>レッスン 6: アプリケーションに ReportViewer コントロールを追加する
レポート ウィザードを使用して子レポートを設計した後は、Web サイト アプリケーションに ReportViewer コントロールを追加します。 ASP.NET レポート Web サイトを利用している場合、ReportViewer コントロールが default.aspx ページに追加されます。   
  
### <a name="to-add-a-reportviewer-control-to-the-application"></a>アプリケーションに ReportViewer コントロールを追加するには  
  
1.  **ソリューション エクスプローラー**で、 **Default.aspx**を右クリックし、 **[ビュー デザイナー]** をクリックします。  
  
2.  default.aspx に ReportViewer コントロールが既に与えられている場合、 **手順 4**に進みます。 与えられていない場合、 **[ツールボックス]** ウィンドウの **[AJAX Extensions]** から **ScriptManager** コントロールをデザイン画面にドラッグします。  
  
3.  **[レポート]** から **ReportViewer** コントロールをデザイン画面の **ScriptManager** コントロールの下にドラッグします。  
  
4.  **ReportViewer** コントロールの右上にある矢印をクリックして、 **[ReportViewer タスク]** ウィンドウを開きます。  
  
5.  **[レポートの選択]** ボックスで、作成した親レポートを選択します。  
  
    レポートを選択すると、レポートで使用されているデータ ソースのインスタンスが自動的に作成されます。 それぞれの DataTable (とその [DataSet](/dotnet/api/system.data.dataset) コンテナーを) をインスタンス化するためのコードが生成されます。 レポートで使用されているそれぞれのデータ ソースに対応する [ObjectDataSource](/dotnet/api/system.web.ui.webcontrols.objectdatasource) コントロールがデザイン画面に追加されます。 このデータ ソース コントロールは自動的に構成されます。  
  
6.  [ビルド] メニューの [Web サイトのビルド] をクリックします。  
  
    レポートがコンパイルされ、レポート式の構文エラーなどのエラーが **[エラー一覧]** 領域に表示されます。 **[エラー一覧]** 領域を表示するには、Visual Studio ウィンドウの下部にある **[エラー一覧]** をクリックします。  
  
## <a name="next-task"></a>次の作業  
これで、Web サイト アプリケーションに ReportViewer コントロールを追加できました。 次は、親レポートにドリルスルー アクションを追加します。 「[レッスン 7: 親レポートにドリルスルー アクションを追加する](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)」を参照してください。  
