---
description: ドメインへのクレンジング プロジェクトの値のインポート
title: ドメインへのクレンジング プロジェクトの値のインポート
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.importprojectvalues.f1
ms.assetid: f23e38e2-39e0-42d7-abd5-34d8fcca5d2a
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 06600482f843ecf014b5ec8648bc8079c871be6a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426354"
---
# <a name="import-cleansing-project-values-into-a-domain"></a>ドメインへのクレンジング プロジェクトの値のインポート

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) では、データ品質プロジェクトのクレンジング プロセス中、または Integration Services パッケージの DQS クレンジング コンポーネントで収集されるデータ品質ナレッジをドメインにインポートできます。 これにより、信頼できるナレッジを保持し、ナレッジ ベースを継続的に改善することができます。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
  
-   クレンジング プロジェクトの値をドメインにインポートするには、そのドメインが、Data Quality Client のクレンジング プロジェクト、または DQS クレンジング コンポーネントを含む Integration Services パッケージで使用されている必要があります。  
  
-   Data Quality Client のクレンジング プロジェクト、または DQS クレンジング コンポーネントを含む Integration Services パッケージが正常に完了している必要があります。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 クレンジング プロセス中に収集したデータ品質ナレッジ ベースをドメインにインポートするには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="import-cleansing-project-values"></a><a name="Import"></a> クレンジング プロジェクトの値のインポート  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、ドメイン管理アクティビティ内のナレッジ ベースを開きます。  
  
3.  既存のドメインに値を追加する場合は、ドメイン リストでドメインを選択します。  
  
4.  **[ドメイン値]** タブをクリックし、アイコン バーの **[値をインポートします]** アイコンをクリックし、 **[プロジェクトの値のインポート]** をクリックします。 **[プロジェクトの値のインポート]** ダイアログ ボックスには、そのドメインを使用してクレンジングされたデータ品質プロジェクトおよび Integration Services パッケージのリストが表示されます。  
  
    > [!NOTE]  
    >   ドメインまたはそのリンク ドメインを使用して作成されたプロジェクトがない場合、またはプロジェクトが完了しなかった場合、 **[プロジェクトの値のインポート]** オプションは使用できません。  
  
5.  **[プロジェクトの値のインポート]** ダイアログ ボックスで、次の操作を行います。  
  
    -   **[インポート済み]** ボックスの一覧で、 **[すべて]** をクリックしてすべてのプロジェクトを表示するか、 **[なし]** をクリックして値がインポートされていないプロジェクトのみを表示します。  
  
    -   値をインポートするプロジェクトを選択します。  
  
    -   **[[新規] タブから値を追加する]** を選択し、 **[適切]** タブと **[修正済み]** タブの値に加えて新しいタブの値を追加します。  
  
    -   **[OK]** をクリックします。  
  
6.  **[ドメイン値]** のタブに戻ると、値が正常にインポートされた場合はメッセージが表示されます。 インポートされた値、つまりドメインに新しく追加された値は、 **"値"** テーブルに表示されます。  
  
7.  ドメイン内にあるすべての値を表示するには、 **[新規のみ表示]** の選択を解除します。  
  
8.  正しい値、エラー値、または無効な値のみを選択して表示するには、 **[適切]**、 **[エラー]**、 **[無効]** を選択します。  
  
9. 特定の文字列を検索するには、 **[検索]** ボックスに文字列を入力します。 検索条件を満たす値を 1 つずつ調べるには、上矢印または下矢印をクリックします。 これらのは黄色で強調表示されます。  
  
10. **[完了]** をクリックします。  
  
    > [!NOTE]  
    >  **[ドメイン値]** タブの値を操作する方法については、「 [Change Domain Values](../data-quality-services/change-domain-values.md)」を参照してください。  
  
##  <a name="follow-up-after-importing-project-values-into-a-domain"></a><a name="FollowUp"></a> 補足情報: プロジェクトの値をドメインにインポートした後  
 クレンジング プロセス中に収集したデータ品質ナレッジ ベースをドメインにインポートしたら、ドメインおよび値に対してその他のドメイン管理タスクを実行できます。 詳しくは、「[ドメインの管理](../data-quality-services/managing-a-domain.md)」をご覧ください。  
  
##  <a name="values-that-will-be-imported"></a><a name="Values"></a> インポートされる値  
 次の値がプロジェクトからドメインにインポートされます。  
  
-   文字列値のみがドメインにインポートされます。  
  
-   **[クレンジング]** アクティビティの **[結果の管理と表示]** ページにある **[適切]** タブ、 **[修正済み]** タブ、および **[新規作成]** タブの値のみがインポートされます。 **[プロジェクトの値のインポート]** ダイアログ ボックスの **[新しいタブから値を追加します。]** チェック ボックスがオンになっている場合にのみ、 **[新規作成]** タブの値がインポートされます。  
  
-   値は、正しい値か、修正値を持つエラー値としてインポートされます。 エラー値は、修正値を持つもののみがインポートされます。  
  
-   修正値は、ナレッジ ベースに存在しない新しい値か、既存の正しい値のいずれかです。  
  
-   レコード レベルではなく値レベルで修正された値のみがナレッジ ベースにインポートされます。  
  
-   インポートされた値がドメイン ルールと矛盾する場合は、無効な値が作成されます。  
  
-   複数のプロジェクトから一度に値をインポートする場合、値は順番にインポートされます。  
  
-   ドメイン内の用語ベースのリレーションの結果として修正された値は正しい値 (エラー値ではなく) としてインポートされます。  
  
##  <a name="values-that-will-not-be-imported"></a><a name="ValuesNot"></a> インポートされない値  
 次の値はプロジェクトからドメインにインポートされません。  
  
-   **[クレンジング]** アクティビティの **[結果の管理と表示]** ページの **[提案]** タブと **[無効]** タブの値はインポートされません。  
  
-   クレンジング プロジェクトで見つかった値がドメイン内の既存の値と矛盾する場合、プロジェクトで見つかった値はスキップされます。 これには、クレンジングとナレッジ ベースの値の間の競合が含まれます。  
  
-   レコード レベルで修正された値はナレッジ ベースにインポートされません。  
  
-   置換先の値が参照データ サービスによって修正されたか、正しい値として承認された場合、置換元の値はドメインにインポートされません。  
  
-   修正値がナレッジ ベースで無効な値またはエラー値として表示される場合、エラー値も修正値もインポートされません。  
  
-   ドメインが複合ドメインの一部で、クレンジングがその複合ドメインに対して実行された場合、値はインポートされません。  
  
-   プロジェクトから値をインポートできるのは、ナレッジ ベースが作業中の状態になっていて、インポートしているユーザーがナレッジ ベースをロックしている場合だけです。  
  
## <a name="see-also"></a>参照  
 [データクレンジング](../data-quality-services/data-cleansing.md)   
 [DQS クレンジング変換](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
