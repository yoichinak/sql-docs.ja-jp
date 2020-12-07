---
description: テスト ケースの作成 (OracleToSQL)
title: テストケースの作成 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 4f7183089fd67f413515034a557e4b73388f950f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418388"
---
# <a name="creating-test-cases-oracletosql"></a>テスト ケースの作成 (OracleToSQL)
テストケースウィザードを使用して、テストを作成します。 このウィザードでは、テスト済みオブジェクトと検証済みオブジェクトを選択し、テストパラメーターを指定することによって、テストケースを作成できます。  
  
## <a name="starting-the-test-case-wizard"></a>テストケースウィザードの開始  
テストケースウィザードを開始するには、[テスト**担当**者] メニューの [**新しいテストケース**] をクリックします。  
  
ウィザードを開始すると、ソース Oracle サーバーでスキーマ SSMATESTER_ORACLE が検索されます。 補助オブジェクトを格納するために使用される Tester 拡張機能スキーマです。 テストケースウィザードで SSMATESTER_ORACLE が見つからない場合は、スキーマの作成を提案するダイアログウィンドウが表示されます。 (通常、この状況は SSMA Tester の初回実行時に発生します)。  
  
ダイアログウィンドウが表示されたら、[ **はい** ] をクリックして、移行元サーバーに SSMATESTER_ORACLE スキーマを作成します。 新しいユーザーを作成し、このユーザーのスキーマにオブジェクトを作成するには、Oracle 特権が必要であることに注意してください。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>ウィザードを使用したテストケースの作成の概要  
テストケースを作成するプロセスは、次の5つの手順で構成されます。  
  
1.  [テストケース &#40;OracleToSQL&#41;の初期化 ](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [&#40;OracleToSQL&#41;をテストするオブジェクトの選択と構成 ](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [影響を受けるオブジェクトの選択と構成 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [呼び出し順序のカスタマイズ &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [テストケースの準備 &#40;OracleToSQL&#41;を終了しています ](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>参照  
[移行されたデータベースオブジェクト &#40;OracleToSQL&#41;のテスト ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
