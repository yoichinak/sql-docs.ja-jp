---
title: SQL Server の単体テストにテスト条件を追加する
description: SQL Server の単体テストにテスト条件を追加する方法について説明します。 このタスクに SQL Server 単体テスト デザイナーを使用する方法を確認します。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 85ba2e56-a0b2-489c-aea2-fb135cce0cfc
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 9920430615d8391ef069078272ed8abbfcef6a00
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100063597"
---
# <a name="how-to-add-test-conditions-to-sql-server-unit-tests"></a>方法:SQL Server の単体テストにテスト条件を追加する

SQL Server の単体テストにテスト条件を追加するには、**SQL Server 単体テスト デザイナー** を使用します。 テスト クラスを保存すると、テスト条件は、テスト クラスを含むソース コード ファイルの Visual C\# コードまたは Visual Basic コードとして、テスト プロジェクトに自動的に保存されます。 保存したテスト条件は、**SQL Server 単体テスト デザイナー** またはソース コード ファイルで編集できます。  
  
### <a name="to-add-test-conditions-to-a-sql-server-unit-test"></a>SQL Server の単体テストにテスト条件を追加するには  
  
1.  **SQL Server 単体テスト デザイナー** で SQL Server の単体テストを開きます。  
  
    開いたテストの名前は、SQL Server 単体テスト デザイナーの上部にあるナビゲーション バーに表示されます。 ナビゲーション バーを使用すると、テスト クラスに含まれているさまざまなテスト メソッドを選択できます。  
  
2.  ナビゲーション バーで、テスト条件を追加するテスト メソッドをクリックするか、 **[共通スクリプト]** をクリックします。  
  
    > [!NOTE]  
    > 共通スクリプトは、特定の単体テストに属していません。 共通スクリプトは、テスト クラスの単体テストの前または後に実行されます。 詳しくは、「[SQL Server の単体テストのスクリプト](../ssdt/scripts-in-sql-server-unit-tests.md)」をご覧ください。  
  
3.  ナビゲーション バーで、テスト条件の追加先となる Transact\-SQL スクリプトをクリックします。 テスト条件は、事前テスト スクリプト、テスト スクリプト、または事後テスト スクリプトに追加できます。  
  
    そのテストの Transact\-SQL スクリプトが Transact\-SQL エディターに表示され、そのテスト条件が **[テスト条件]** ウィンドウに表示されます。  
  
4.  **[テスト条件]** の選択肢の一覧で、テスト条件をクリックし、 **[テスト条件を追加します]** (+) をクリックします。  
  
    テスト条件が単体テスト メソッドに追加されます。  
  
    > [!NOTE]  
    > テスト メソッド内のテスト条件の順序を変更するには、**[テスト条件]** ウィンドウでテスト条件をクリックし、上矢印または下矢印をクリックします。  
  
5.  追加したテスト条件を選択して、 **[プロパティ]** ウィンドウを表示します。  
  
    [プロパティ] ウィンドウで、テスト条件を構成します。 たとえば、実行時間テスト条件の **"実行時間"** プロパティを変更できます。 このプロパティを設定すると、指定した時間内に Transact\-SQL スクリプトが実行されない場合にテストが失敗します。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[方法: 空の SQL Server の単体テストを作成する方法](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)  
[方法: 関数、トリガー、ストアド プロシージャに対する SQL Server の単体テストを作成する方法](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)  
[SQL Server の単体テストでのテスト条件の使用](../ssdt/using-test-conditions-in-sql-server-unit-tests.md)  
[SQL Server の単体テストのスクリプト](../ssdt/scripts-in-sql-server-unit-tests.md)  
[SQL Server の単体テストの結果の解釈](../ssdt/interpreting-sql-server-unit-test-results.md)  
[方法:  SQL Server の単体テストを実行する](../ssdt/how-to-run-sql-server-unit-tests.md)  
  
