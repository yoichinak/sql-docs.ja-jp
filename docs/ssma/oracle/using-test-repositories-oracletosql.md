---
description: テスト リポジトリの使用 (OracleToSQL)
title: テストリポジトリの使用 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Cases Repository
- Test Results Repository
ms.assetid: f941cce4-d3e3-4aeb-a88a-4f101a97a9f4
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6b070a45c7990efbb598401b241083fcb2d804f5
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035141"
---
# <a name="using-test-repositories-oracletosql"></a>テスト リポジトリの使用 (OracleToSQL)
SSMA テストリポジトリには、後で使用するために SSMA Tester テストケースとテスト結果が格納されます。 リポジトリデータは、 **ssmatesterdb**データベースのスキーマ**ssma_oracle_utilities**の SQL Server テーブル**TestCaseRepository**および**runtestcaseresultrepository**に保存されます。  
  
[テストケースのリポジトリ] ダイアログボックスでは、次のボタンを使用できます。  
  
-   [ **更新** ] ボタンをクリックして、テストケースまたはテスト結果一覧を更新します。  
  
-   [ **閉じる** ] ボタンをクリックして、[テストケースのリポジトリ] ダイアログボックスを閉じます。  
  
## <a name="test-cases-repository"></a>テストケースリポジトリ  
テストケースリポジトリを表示するには、テスト**担当**者メニューの [**テストケース**] をクリックします。 SSMA は、[テストケース **] ページに**保存されているテストケースの一覧を含む [テストケース] ダイアログウィンドウ**のリポジトリ**を表示します。  
  
グリッドには、各テストケースに関する次の情報が表示されます。  
  
-   名前: テストケース名。  
  
-   Created: テストケースの作成日。  
  
-   Modified: テストケースの最終更新日。  
  
-   説明: テストケースの説明。  
  
[テストケース] ページでは、次のボタンを使用できます。  
  
-   [ **追加** ] ボタンをクリックして、テストケースウィザードを実行し、新しいテストを作成します。  
  
-   選択したテストをリポジトリから削除するには、[ **削除** ] ボタンをクリックします。テストケースが削除されると、関連するすべてのテスト結果も削除されます。  
  
-   [ **編集** ] ボタンをクリックして、テストケースウィザードを実行し、選択したテストを変更します。  
  
-   [ **実行** ] ボタンをクリックして [ [実行中のテストケース (OracleToSQL)](./running-test-cases-oracletosql.md) ] ダイアログを開き、選択したテストを実行します。  
  
## <a name="test-results-repository"></a>テスト結果リポジトリ  
テスト結果リポジトリは、[**テストケース**] ウィンドウの [リポジトリ] の [**テスト結果**] ページで確認できます。 [**テスト担当**者] メニューの [**テスト結果...** ] をクリックして開きます。  
  
**テスト結果**のページでは、次の2つのフィルターを使用できます。  
  
-   テストケース名フィルター: テストケース名でテスト結果を選択できます。 このフィルターの **すべてのテストケース** 値で、すべてのテストケースのテスト結果を表示できます。  
  
-   テストケース実行日付フィルター: 保存日によってテスト結果をフィルター処理します。このフィルターの **すべての期間** の値を使用すると、保存する日付に対してテスト結果を表示できます。  
  
テスト結果に関する次の情報がグリッドに表示されます。  
  
-   名前: テストケース名。  
  
-   Saved: 保存するテストケースの日付。  
  
-   結果: テストの実行の概要です (このセルのツールヒントには、テストの実行の完全な概要が表示されます)。  
  
[テスト結果] ページでは、次のボタンを使用できます。  
  
-   [ **表示** ] ボタンをクリックして、現在のテストケースの結果の [ [テストケースレポートの表示 &#40;OracleToSQL&#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md) を開きます。  
  
-   選択したテスト結果を削除するには、[ **削除** ] ボタンをクリックします  
  
## <a name="see-also"></a>参照  
[OracleToSQL&#41;&#40;のテストケースの実行 ](../../ssma/oracle/running-test-cases-oracletosql.md)  
[移行されたデータベースオブジェクト &#40;OracleToSQL&#41;のテスト ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
