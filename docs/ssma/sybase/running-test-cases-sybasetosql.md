---
description: テスト ケースの実行 (SybaseToSQL)
title: テストケースの実行 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: ea2b250f59a29a16bc77ad23e28b0823461a8ace
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468756"
---
# <a name="running-test-cases-sybasetosql"></a>テスト ケースの実行 (SybaseToSQL)
SSMA Tester がテストケースを実行すると、テスト用に選択されたオブジェクトが実行され、検証結果に関するレポートが作成されます。 結果が両方のプラットフォームで同一の場合、テストは成功しました。 Sybase との間のオブジェクトの対応 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、現在の SSMA プロジェクトのスキーママッピングの設定に従って決定されます。  
  
テストを成功させるために必要な要件は、すべての Sybase オブジェクトが変換され、ターゲットデータベースに読み込まれることです。 また、両方のプラットフォームのテーブルの内容が同期されるように、テーブルデータを移行する必要があります。  
  
## <a name="run-test-case"></a>テストケースの実行  
準備されたテストケースを実行するには:  
  
1.  [**実行**] ボタンをクリックします。  
  
2.  [ **Sybase への接続** ] ダイアログボックスで、接続情報を入力し、[ **接続**] をクリックします。  
  
テストが完了すると、テストケースレポートが作成されます。 [ **レポート** ] ボタンをクリックすると、 [&#40;SybaseToSQL&#41;のテストケースレポートの表示 ](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)が表示されます。 テストの結果 (テストケースレポート) は、後で使用するために、 [テストリポジトリ &#40;SybaseToSQL&#41;を使用して ](../../ssma/sybase/using-test-repositories-sybasetosql.md) に自動的に格納されます。  
  
## <a name="test-case-execution-steps"></a>テストケースの実行ステップ  
  
### <a name="prerequisites"></a>[前提条件]  
SSMA Tester は、テストを開始する前に、テストの実行ですべての前提条件が満たされているかどうかを確認します。 条件が満たされていない場合は、エラーメッセージが表示されます。  
  
### <a name="initialization"></a>初期化  
この手順では、SSMA Tester が Sybase との両方に補助オブジェクト (テーブル、トリガー、およびビュー) を作成し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 テーブル比較モードが変更された場合に **のみ**、検証対象として選択された影響を受けるテーブルでの変更のトレースを許可します。  
  
検証されたテーブルに USER_TABLE という名前が付けられているとします。 このようなテーブルの場合、Sybase では次の補助オブジェクトが作成されます。  
  
次のオブジェクトは、Sybase の SSMATESTER2005db データベースまたは SSMATESTER2008db データベース、および ssmatesterdb_syb データベースに作成され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
|名前|Type|説明|  
|--------|--------|---------------|  
|USER_TABLE $ Trg|トリガー|検証されたテーブルの変更の監査をトリガーします。|  
|USER_TABLE $ Aud|テーブル|削除された行と上書きされた行が保存されるテーブル。|  
|USER_TABLE $ AudID|テーブル|新しい行と変更された行が保存されるテーブル。|  
|USER_TABLE|View|テーブル変更の簡略化された表現。|  
|USER_TABLE $ new|View|挿入行と上書き行の簡略化された表現。|  
|USER_TABLE $ new_id|View|挿入および変更された行の識別。|  
|USER_TABLE $ old|View|削除行と上書き行の簡略化された表現。|  
  
次のオブジェクトは、Sybase とで検証済みテーブルのデータベースに作成され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
|名前|Type|説明|  
|--------|--------|---------------|  
|USER_TABLE $ Trg|トリガー|検証されたテーブルの変更の監査をトリガーします。|  
  
### <a name="test-object-calls"></a>オブジェクト呼び出しのテスト  
この手順では、SSMA Tester はテスト用に選択された各オブジェクトを呼び出し、結果を比較して、レポートを表示します。  
  
### <a name="finalization"></a>最終  
終了処理中に、 **初期化** ステップで作成された補助オブジェクトがクリーンアップされます。  
  
## <a name="next-step"></a>次の手順  
[テストケースレポートの表示 &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>参照  
[&#40;SybaseToSQL&#41;をテストするオブジェクトの選択と構成 ](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[影響を受けるオブジェクトの選択と構成 &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[&#40;SybaseToSQL&#41;の移行されたデータベースオブジェクトのテスト ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
