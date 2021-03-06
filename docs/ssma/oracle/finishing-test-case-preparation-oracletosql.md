---
description: テスト ケースの準備の終了 (OracleToSQL)
title: テストケースの準備を完了しています (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: f1d0f99987a58a8d942c9d7601124c3cfc39b09d
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100014623"
---
# <a name="finishing-test-case-preparation-oracletosql"></a>テスト ケースの準備の終了 (OracleToSQL)
ウィザードの最後のページには、テストケースの説明と、テストに関係するオブジェクトに関する情報が表示されます。 また、このページでは、テストの実行オプションを設定することもできます。  
  
[ **テストケース情報** ] セクションには、テストケースの名前と説明が表示されます。  
  
[ **テスト対象として選択されたオブジェクト** ] セクションには、オブジェクトの種類別にグループ化されたテスト済みオブジェクトの名前付きリストが含まれます。  
  
[ **分析されるテストの影響を受けるオブジェクト** ] セクションには、テスト済みオブジェクトの実行後にデータ変更を比較する必要があるオブジェクトの名前付きリストが表示されます。  
  
## <a name="test-case-settings"></a>テストケースの設定  
[ **テストケースの設定** ] セクションでは、次の実行テストオプションを設定できます。  
  
### <a name="stop-test-execution-after-first-failure"></a>最初の失敗後にテストの実行を停止する  
テストの実行中にエラーが発生した場合にテストを中断するように指定します。  
  
-   **[はい]** を選択すると、エラーが発生した場合にテストの実行が中断します。  
  
-   [ **いいえ**] を選択した場合、テストの実行はエラーの後も続行されます。  
  
### <a name="perform-data-rollback"></a>データのロールバックを実行する  
テスト実行後の自動データロールバックを有効にします。  
  
-   **[はい]** を選択した場合、データの変更はテストの実行後に失われます。  
  
-   [ **いいえ**] を選択すると、すべてのテスト実行データの変更が保存されます。  
  
### <a name="auxiliary-tables-saving-mode"></a>補助テーブル保存モード  
テストの実行中に作成される補助テーブルの保存モードを定義します。 「 [実行中のテストケース &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md) 」トピックの補助テーブルの説明を参照してください。  
  
-   [ **常に保存**] を選択した場合、補助テーブルデータは、後で使用するために常に格納されます。  
  
-   [ **テーブル比較に失敗** した場合に保存] を選択すると、補助テーブルデータはエラーが発生した場合にのみ保存されます。  
  
-   [ **常に削除**] を選択した場合は、テストの実行後、補助テーブルは常に削除されます。  
  
-   [ **テーブル比較に失敗** した場合にユーザーに問い合わせる] を選択すると、エラーが発生した場合に、ユーザーは必要な操作を選択できます。  
  
[ **完了** ] ボタンをクリックして、準備されたテストケースを [テストリポジトリ (OracleToSQL) を使用して](./using-test-repositories-oracletosql.md)に保存します。  
  
## <a name="see-also"></a>参照  
[テストリポジトリ &#40;OracleToSQL&#41;の使用 ](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[OracleToSQL&#41;&#40;のテストケースの実行 ](../../ssma/oracle/running-test-cases-oracletosql.md)  
[移行されたデータベースオブジェクト &#40;OracleToSQL&#41;のテスト ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
