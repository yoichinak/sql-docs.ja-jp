---
description: テスト ケースの作成 (SybaseToSQL)
title: テストケースの作成 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: fb3fe4816faeb050a1c4321def0e7dd4e6937bdb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463154"
---
# <a name="creating-test-cases-sybasetosql"></a>テスト ケースの作成 (SybaseToSQL)
テストケースウィザードを使用して、テストを作成します。 このウィザードでは、テスト済みオブジェクトと検証済みオブジェクトを選択し、テストパラメーターを指定することによって、テストケースを作成できます。  
  
## <a name="starting-the-test-case-wizard"></a>テストケースウィザードの開始  
テストケースウィザードを開始するには、[テスト**担当**者] メニューの [**新しいテストケース**] をクリックします。  
  
ウィザードを開始すると、ソースの Sybase サーバーでデータベースの ssmatester2005db または ssmatester2008db (プロジェクトの種類によって異なります) が検索されます。 補助オブジェクトを格納するために使用される Tester 拡張機能スキーマです。 テストケースウィザードで ssmatester2005db または ssmatester2008db が見つからない場合は、テスト担当者拡張データベースを作成するように提案するダイアログウィンドウが表示されます。 (通常、この状況は SSMA Tester の初回実行時に発生します)。  
  
ダイアログウィンドウが表示されたら、[ **はい** ] をクリックして、ソースサーバーに Sybase tester データベースを作成します。 新しいダイアログウィンドウが表示され、新しいテスト担当者データベースを検索するデバイスを1つ以上追加する必要があります。 [ **追加** ] をクリックしてデバイスを追加します。 [ **Tester データベースの割り当て領域** ] ダイアログボックスで、デバイスを選択し、テスターデータベースで使用されるサイズを指定します。 また、データベースログ用に個別のデバイスを設定することもできます。 データベースを作成するには、Sybase 特権が必要です。  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>ウィザードを使用したテストケースの作成の概要  
テストケースを作成するプロセスは、次の5つの手順で構成されます。  
  
1.  [テストケース &#40;SybaseToSQL&#41;を初期化 ](../../ssma/sybase/initializing-test-cases-sybasetosql.md)しています。  
  
2.  [&#40;SybaseToSQL&#41;をテストするオブジェクトを選択して構成して ](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)います。  
  
3.  [影響を受けるオブジェクトの選択と構成 &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)。  
  
4.  [&#40;SybaseToSQL&#41;の呼び出し順序をカスタマイズ ](../../ssma/sybase/customizing-calls-order-sybasetosql.md)しています。  
  
5.  [SybaseToSQL&#41;&#40;テストケースの準備を完了 ](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md)しています。  
  
## <a name="see-also"></a>参照  
[&#40;SybaseToSQL&#41;の移行されたデータベースオブジェクトのテスト ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
