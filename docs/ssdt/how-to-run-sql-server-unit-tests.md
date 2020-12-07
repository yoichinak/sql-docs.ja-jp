---
title: SQL Server の単体テストを実行する
description: SQL Server 単体テストを実行する方法について説明します。 異なるバージョンの Visual Studio でさまざまなウィンドウやツールからテストを実行するための手順を確認します。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 34fe2d1e-d47b-4808-af56-8cc0fdae6518
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 3968ea4001b4ada8940f4434bfbb2eff35840850
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988208"
---
# <a name="how-to-run-sql-server-unit-tests"></a>方法:SQL Server の単体テストを実行する

SQL Server の単体テストは、さまざまなウィンドウやコマンド プロンプト ウィンドウを使用するなど、複数の方法で実行できます。  
  
> [!NOTE]  
> リモートで単体テストを実行することはできません。  
  
使用できる方法は、「[SQL Server の単体テストの実行](../ssdt/running-sql-server-unit-tests.md)」で説明されているように、インストールしたソフトウェアによって異なります。  
  
### <a name="to-run-sql-server-unit-tests-using-test-view-visual-studio-2010"></a>テスト ビューを使用して SQL Server 単体テストを実行するには (Visual Studio 2010)  
  
1.  **[テスト]** メニューの **[ウィンドウ]** をポイントし、 **[テスト ビュー]** をクリックします。  
  
    **[テスト ビュー]** ウィンドウが開きます。  
  
2.  **[テスト ビュー]** ウィンドウで、実行するテストをクリックします。 Ctrl キーまたは Shift キーを使用すると、連続しないテストまたは連続したテストのブロックを指定できます。  
  
3.  以下のいずれかを実行します。  
  
    -   **[テスト ビュー]** ウィンドウの任意の場所を右クリックし、 **[選択範囲の実行]** をクリックします。  
  
    -   **[テスト ビュー]** ツール バーの **[選択範囲の実行]** をクリックします。  
  
### <a name="to-run-sql-server-unit-tests-using-test-explorer-visual-studio-2012"></a>テスト エクスプローラーを使用して SQL Server 単体テストを実行するには (Visual Studio 2012)  
  
1.  **[テスト]** メニューの **[ウィンドウ]** をポイントし、 **[テスト エクスプローラー]** をクリックします。  
  
    **[テスト エクスプローラー]** ウィンドウが開きます。  
  
2.  **テスト エクスプローラー**で、実行するテストをクリックします。 Ctrl キーまたは Shift キーを使用すると、連続しないテストまたは連続したテストのブロックを指定できます。  
  
3.  強調表示されたテストの 1 つを右クリックし、 **[選択したテストの実行]** をクリックします。  
  
### <a name="to-run-sql-server-unit-tests-from-the-sql-server-unit-test-designer-visual-studio-2010"></a>SQL Server 単体テスト デザイナーを使用して SQL Server 単体テストを実行するには (Visual Studio 2010)  
  
-   **[テスト ツール]** ツール バーには、デバッガーを使用してプロジェクトを開始するボタンまたはデバッガーを使用しないでプロジェクトを開始するボタンがあります。  
  
この手順により、現在のテスト実行内のすべてのテストが実行されます。 テストの実行を開始するとすぐに、 **[テスト結果]** ウィンドウが表示され、テスト実行の進行状況が表示されます。 この表示には、実行中のテストと完了したテストが含まれます。 詳しくは、「[SQL Server の単体テストの結果の解釈](../ssdt/interpreting-sql-server-unit-test-results.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの実行](../ssdt/running-sql-server-unit-tests.md)  
[方法: Microsoft Visual Studio 2010 から自動テストを実行する](/previous-versions/visualstudio/visual-studio-2010/ms182470(v=vs.100))  
[コマンド ラインからの自動テストの実行 (Visual Studio 2010)](/previous-versions/visualstudio/visual-studio-2010/ms182486(v=vs.100))  
[アプリケーションのテスト (Visual Studio 2012)](/azure/devops/test/overview)  
