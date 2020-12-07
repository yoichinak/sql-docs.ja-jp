---
description: テスト リポジトリの使用 (SybaseToSQL)
title: テストリポジトリの使用 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Repositories
ms.assetid: c359c25c-db2a-4a20-afa9-62d87a62df72
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: b05dac0ec74bb6c0cd9c9e99d8bb631b0a242eb3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418248"
---
# <a name="using-test-repositories-sybasetosql"></a>テスト リポジトリの使用 (SybaseToSQL)
SSMA テストリポジトリには、後で使用するために SSMA Tester テストケースとテスト結果が格納されます。 リポジトリデータは、 **ssmatesterdb_syb**データベースのスキーマ**ssma_sybase_utilities**の SQL Server テーブル**TestCaseRepository**および**runtestcaseresultrepository**に保存されます。  
  
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
  
-   [ **実行** ] ボタンをクリックし [て、実行中のテストケース &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md) ] ダイアログを開き、選択したテストを実行します。  
  
## <a name="test-results-repository"></a>テスト結果リポジトリ  
テスト結果リポジトリは、[**テストケース**] ウィンドウの [リポジトリ] の [**テスト結果**] ページで確認できます。 [**テスト担当**者] メニューの [**テスト結果...** ] をクリックして開きます。  
  
**テスト結果**のページでは、次の2つのフィルターを使用できます。  
  
-   テストケース名フィルター: テストケース名でテスト結果を選択できます。 このフィルターの **すべてのテストケース** 値を使用して、すべてのテストケースのテスト結果を表示できます。  
  
-   テストケース実行日付フィルター: 保存日によってテスト結果をフィルター処理します。このフィルターの **すべての期間** の値を使用すると、保存する日付に対してテスト結果を表示できます。  
  
テスト結果に関する次の情報がグリッドに表示されます。  
  
-   名前: テストケース名。  
  
-   開始: テストケースの実行日。  
  
-   結果: テストの実行の概要です (このセルのツールヒントには、テストの実行の完全な概要が表示されます)。  
  
[テスト結果] ページでは、次のボタンを使用できます。  
  
-   [ **表示** ] ボタンをクリックして、現在のテストケースの結果の [ [テストケースレポートの表示] &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md) を開きます。  
  
-   選択したテスト結果を削除するには、[ **削除** ] ボタンをクリックします  
  
## <a name="see-also"></a>参照  
[実行、テストケース &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[&#40;SybaseToSQL&#41;の移行されたデータベースオブジェクトのテスト ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
