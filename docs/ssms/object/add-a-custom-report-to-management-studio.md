---
description: Management Studio へのカスタム レポートの追加
title: Management Studio へのカスタム レポートの追加
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 3cf8d726-0a90-4f80-98d0-352a2a59be0f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: aa920b620cfa0045228fcdb5675c1e88bc7ab035
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480170"
---
# <a name="add-a-custom-report-to-management-studio"></a>Management Studio へのカスタム レポートの追加
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
ここでは、簡単な [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポートを作成し、.rdl ファイルとして保存した後、そのファイルを [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] にカスタム レポートとして追加する方法について説明します。 [!INCLUDE[ssRS](../../includes/ssrs.md)] では、さまざまな高度なレポートを作成できます。 このトピックを使用してレポートを作成するには、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] がコンピューターにインストールされている必要があります。 [!INCLUDE[ssRS](../../includes/ssrs.md)] を使用してカスタム レポートを実行する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]をインストールする必要はありません。  
  
 
### <a name="to-create-a-simple-report-saved-as-an-rdl-file"></a>簡単なレポートを作成し、.rdl ファイルとして保存するには  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]**、 **[Microsoft SQL Server]** の順にポイントし、 **[SQL Server データ ツール]** をクリックします。  
  
2.  **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。  
  
3.  **[プロジェクトの種類]** ボックスの一覧で、 **[ビジネス インテリジェンス プロジェクト]** をクリックします。  
  
4.  **[テンプレート]** ボックスの一覧で、 **[レポート サーバー プロジェクト ウィザード]** をクリックします。  
  
5.  **[名前]** に **「ConnectionsReport**」と入力して、 **[OK]** をクリックします。  
  
6.  **レポート ウィザード** の最初のページで、 **[次へ]** をクリックします。  
  
7.  **[データ ソースを選択します]** ページの [名前] ボックスに、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]への接続で使用する名前を入力し、 **[編集]** をクリックします。  
  
8.  **[接続プロパティ]** ダイアログ ボックスの **[サーバー名]** ボックスに、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]インスタンスの名前を入力します。  
  
9. **[データベース名の選択または入力]** ボックスに、任意の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースの名前 (「 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]」など) を入力して、 **[OK]** をクリックします。  
  
10. **[データ ソースを選択します]** ページで、 **[次へ]** をクリックします。  
  
11. **[クエリのデザイン]** ページの **[クエリ文字列]** ボックスに、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを入力して、 [!INCLUDE[ssDE](../../includes/ssde_md.md)][次へ] **をクリックします。これは**への現在の接続一覧を表示するステートメントです。 レポート ウィザードの [クエリ文字列] ボックスにレポート パラメーターは使用できません。 複雑なカスタム レポートは、手動で作成する必要があります。  
  
    **SELECT session_id, net_transport FROM sys.dm_exec_connections;**  
  
12. **[レポートの種類を選択します]** ページで **[テーブル]** を選択して、 **[完了]** をクリックします。  
  
13. **[ウィザードの完了]** ページの **[レポート名]** ボックスに「 **ConnectionsReport**」と入力し、 **[完了]** をクリックすると、レポートが作成され、保存されます。  
  
14. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]を終了します。  
  
15. データベース サーバー上でカスタム レポート用に作成したフォルダーに、 **ConnectionsReport.rdl** をコピーします。  
  
### <a name="to-add-a-report-to-management-studio"></a>レポートを Management Studio に追加するには  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]のオブジェクト エクスプローラーでノードを右クリックし、 **[レポート]** をポイントして、 **[カスタム レポート]** をクリックします。 **[ファイルを開く]** ダイアログ ボックスで、カスタム レポート フォルダーに移動し、 **ConnectionsReport.rdl** ファイルを選択して、 **[開く]** をクリックします。  
  
    新しいカスタム レポートは、初めてオブジェクト エクスプローラーのノードから開いたときに、最近使用した一覧に追加されます。この一覧はノードのショートカット メニューの **[カスタム レポート]** の下に表示されます。 標準レポートも、初めて開いたときに **[カスタム レポート]** の下の最近使用した一覧に表示されます。 カスタム レポート ファイルを削除した場合は、次にそのアイテムを選択したときに、最近使用した一覧からアイテムを削除するというプロンプトが表示されます。  
  
    1.  最近使用した一覧の表示ファイル数を変更するには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[環境]** フォルダーを展開して **[全般]** をクリックします。  
  
    2.  **[最近使用したファイルの一覧]** の数を調整します。  
  
## <a name="see-also"></a>参照  
[Management Studio におけるカスタム レポート](../../ssms/object/custom-reports-in-management-studio.md)  
[カスタム レポートでのオブジェクト エクスプローラー ノード プロパティの使用](../../ssms/object/use-custom-reports-with-object-explorer-node-properties.md)  
[カスタム レポート実行時の警告の抑制を解除する方法](../../ssms/object/unsuppress-run-custom-report-warnings.md)  
[SQL Server Reporting Services](../../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
