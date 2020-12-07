---
description: テスト ケースの準備の終了 (SybaseToSQL)
title: テストケースの準備を完了しています (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Test Case Settings
ms.assetid: 8b2a49b0-4296-4f3f-9e56-323aa6a6fa8e
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a1a3c415e8c13bf0ed1eaf4c75baf0230544964c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492223"
---
# <a name="finishing-test-case-preparation-sybasetosql"></a>テスト ケースの準備の終了 (SybaseToSQL)
ウィザードの最後のページには、テストケースの説明と、テストに関係するオブジェクトに関する情報が表示されます。 また、このページでは、テストの実行オプションを設定することもできます。  
  
[ **テストケース情報** ] セクションには、テストケースの名前と説明が表示されます。  
  
[ **テストオブジェクト** ] セクションには、オブジェクトの種類別にグループ化されたテスト済みオブジェクトの名前付きリストが含まれています。  
  
[ **分析される影響を受けるオブジェクト** ] セクションには、テスト済みオブジェクトの実行後にデータ変更を比較する必要があるオブジェクトの名前付きリストが表示されます。  
  
## <a name="test-case-settings"></a>テストケースの設定  
[ **テストケースの設定** ] セクションでは、次の実行テストオプションを設定できます。  
  
### <a name="stop-test-execution-after-first-failure"></a>最初の失敗後にテストの実行を停止する  
テストの実行中にエラーが発生した場合にテストを中断するように指定します。  
  
-   **[はい]** を選択すると、エラーが発生した場合にテストの実行が中断します。  
  
-   [ **いいえ**] を選択した場合、テストの実行はエラーの後も続行されます。  
  
### <a name="perform-data-rollback"></a>データのロールバックを実行する  
テストの実行後に自動データロールバックを有効にします。  
  
-   **[はい]** を選択した場合、データの変更はテストの実行後に失われます。  
  
-   [ **いいえ**] を選択すると、すべてのテスト実行データの変更が保存されます。  
  
### <a name="auxiliary-tables-saving-mode"></a>補助テーブル保存モード  
テストの実行中に作成される補助テーブルの保存モードを定義します。 「 [実行中のテストケース &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md) 」トピックの補助テーブルの説明を参照してください。  
  
-   [ **常に保存**] を選択した場合、補助テーブルデータは、後で使用するために常に格納されます。  
  
-   [ **テーブル比較に失敗**した場合に保存] を選択すると、補助テーブルデータはエラーが発生した場合にのみ保存されます。  
  
-   [ **常に削除**] を選択した場合は、テストの実行後、補助テーブルは常に削除されます。  
  
-   [ **テーブル比較に失敗**した場合にユーザーに問い合わせる] を選択すると、エラーが発生した場合に、ユーザーは必要な操作を選択できます。  
  
[ **完了** ] をクリックして、準備されたテストケースをに保存します。これには、 [テストリポジトリ &#40;SybaseToSQL&#41;を使用 ](../../ssma/sybase/using-test-repositories-sybasetosql.md)します。  
  
## <a name="see-also"></a>参照  
[テストリポジトリの使用 &#40;SybaseToSQL&#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[実行、テストケース &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[&#40;SybaseToSQL&#41;の移行されたデータベースオブジェクトのテスト ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
