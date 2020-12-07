---
description: .dqs ファイルからのナレッジ ベースのインポート
title: .dqs ファイルからのナレッジ ベースのインポート
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9b9786fe-9e80-429a-afcb-dc3b3dd6f0b0
author: swinarko
ms.author: sawinark
ms.openlocfilehash: c6be16bf484f3b5f6f55afaaacbeda8d2bb6d341
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491571"
---
# <a name="import-a-knowledge-base-from-a-dqs-file"></a>.dqs ファイルからのナレッジ ベースのインポート

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) で .dqs データ ファイルからナレッジ ベース全体をインポートする方法について説明します。 データ ファイルは、既存のナレッジ ベースを [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーションでエクスポートすることによって作成します (「 [ナレッジ ベースを .dqs ファイルにエクスポート](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)」を参照)。  
  
 .dqs データ ファイルを使用してナレッジ ベースのコンテンツをエクスポートし、後でそのコンテンツを同じ [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] の別のナレッジ ベースや異なる [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] にインポートすることで、ナレッジの生成処理を簡略化し、時間と労力を節約します。 ナレッジ ベースやその中のナレッジを他のユーザーと共有でき、他のユーザーの時間を節約できます。 .dqs ファイルには、ドメインや照合ポリシーを含むナレッジ ベースのすべての情報が含まれます。ただし、アタッチされた参照データ情報は含まれません。 発行済みのデータと発行されていないデータがインポートされます。  
  
 .dqs データ ファイルは、表示できないように暗号化されています。  
  
 ナレッジ ベースをインポートする際に同じ名前を使用できますが、クライアント アプリケーションにそのナレッジ ベースの名前が既に存在する場合は名前を変更する必要があります。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
 ナレッジ ベースを .dqs ファイルからインポートするには、事前にナッレジ ベースを .dqs ファイルにエクスポートしている必要があります。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 ナレッジ ベースを .dqs データ ファイルからインポートするには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="import-a-knowledge-base-from-a-dqs-file"></a><a name="Import"></a> Dqs ファイルからナレッジベースをインポートする  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で **[新しいナレッジ ベース]** をクリックします。  
  
3.  ナレッジ ベースの名前を入力します。  
  
4.  **[次の場所からナレッジ ベースを作成]** の下矢印をクリックし、 **[DQS ファイルからインポート]** をクリックします。  
  
5.  **[データ ファイルの選択]** で **[参照]** をクリックします。  
  
6.  **[データ ファイルからインポート]** ダイアログ ボックスで、インポートする .dqs ファイルを含むフォルダーに移動してファイル名をクリックします。 **[開く]** をクリックします。  
  
7.  正しいナレッジ ベースとドメインが **[ドメイン]** リストに表示されていることを確認します。  
  
8.  実行するアクティビティを選択して **[作成]** をクリックします。  
  
9. **[ナレッジ ベースのインポート]** ダイアログ ボックスで、ステータス行にインポートの完了が表示されていることを確認します。 **[OK]** をクリックします。  
  
10. 必要なナレッジ検出、ドメイン管理、または照合ポリシー タスクを実行し、 **[完了]** をクリックします。  
  
11. ナレッジ ベースのナレッジを発行する場合は **[発行]** をクリックし、発行しない場合は **[いいえ]** をクリックします。  
  
12. ナレッジ ベースを発行した場合は **[OK]** をクリックします。  
  
13. Data Quality Services のホーム ページで、 **[最近使用したナレッジ ベース]** の下にナレッジ ベースが表示されていることを確認します。  
  
##  <a name="follow-up-after-importing-a-knowledge-base-from-a-dqs-file"></a><a name="FollowUp"></a> 補足情報: .dqs ファイルからナレッジ ベースをインポートした後  
 .dqs ファイルからナレッジ ベースをインポートした後で、ナレッジ ベースのコンテンツに応じてナレッジをナレッジ ベースに追加したり、ナレッジ ベースをクレンジング プロジェクトや照合プロジェクトで使用したりすることができます。 詳しくは、「[ナレッジ検出の実行](../data-quality-services/perform-knowledge-discovery.md)」、「[ドメインの管理](../data-quality-services/managing-a-domain.md)」、「[複合ドメインの管理](../data-quality-services/managing-a-composite-domain.md)」、「[照合ポリシーの作成](../data-quality-services/create-a-matching-policy.md)」、「[データ クレンジング](../data-quality-services/data-cleansing.md)」、または「[データ照合](../data-quality-services/data-matching.md)」をご覧ください。  
  
  
