---
description: .dqs ファイルからのドメインのインポート
title: .dqs ファイルからのドメインのインポート
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: fabd88b0-22b3-4543-a993-6d5b202ded80
author: swinarko
ms.author: sawinark
ms.openlocfilehash: c1d597c8ab750b5debe221d2cf68c231143736b4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491533"
---
# <a name="import-a-domain-from-a-dqs-file"></a>.dqs ファイルからのドメインのインポート

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) で .dqs ファイルから既存のナレッジ ベースにドメインをインポートする方法について説明します。 .dqs データ ファイルは、 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] アプリケーションからドメインまたはナレッジ ベースをエクスポートすることによって作成されます。 .dqs データ ファイルは、表示できないように暗号化されています。  
  
 .dqs データ ファイルを使用してナレッジ ベースからドメインをエクスポートし、別のナレッジ ベースにインポートすることで、ナレッジの生成処理を簡略化し、時間と労力を節約します。 ドメインやそのナレッジを他のユーザーと共有でき、他のユーザーの時間を節約できます。 ドメインをインポートするときは、1 つの単一ドメインまたは 1 つの複合ドメイン (複数の単一ドメインで構成されるドメイン) をインポートできます。 単一ドメインについての .dqs ファイルには、ドメインのプロパティ、値、ルールのデータを含む、ドメインのすべてのデータが格納されています。ただし、マップされた参照データ情報は格納されません。 複合ドメインについての .dqs ファイルには、複合ドメインに含まれる単一ドメインのすべてのドメイン データと複合ドメインのプロパティ、値のリレーション、CD ルールを含む、複合ドメインのすべてのデータが格納されています。ただし、マップされた参照データ情報は格納されません。 発行済みのデータと発行されていないデータがインポートされます。  
  
 ドメインをインポートする際、ドメインの名前は、エクスポートした元のドメインの名前と同じになります。ただし、そのドメイン名が既に存在する場合は、名前に "_1" が追加されます。 これは、複合ドメインをインポートする際に、それに含まれる個々のドメインの名前が既存のドメインと同じだった場合も同様です。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
 ドメインを .dqs ファイルからインポートするには、1 つの単一ドメインまたは 1 つの複合ドメイン (複数の単一ドメインで構成されるドメイン) を .dqs ファイルにエクスポートしておく必要があります。 .dqs ファイルにはドメインが 1 つだけ含まれている必要があります。 また、ドメインをインポートするナレッジ ベースを作成して開いておく必要があります。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 ドメインを .dqs データ ファイルからインポートするには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="import-a-domain-from-a-dqs-file"></a><a name="Import"></a> Dqs ファイルからドメインをインポートする  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、ドメイン管理アクティビティ内のナレッジ ベースを開きます。  
  
3.  **[ドメインをデータ ファイルからインポートします]** アイコンをクリックします。  
  
4.  **[データ ファイルからインポート]** ダイアログ ボックスで、インポートするファイルを含むフォルダーに移動し、ファイル (DQS ファイル) を選択して **[開く]** をクリックします。  
  
5.  **[ドメインのインポート]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
    > [!NOTE]  
    >  インポート操作が成功するのは、インポートする .dqs ファイルに単一ドメインまたは複合ドメイン (複数の単一ドメインで構成されるドメイン) が 1 つだけ含まれている場合のみです。  
  
6.  インポートしたドメインが **[ドメイン]** リストに表示されていることを確認します。 複合ドメインをインポートした場合は、複合ドメインとそれに含まれるすべての単一ドメインが **[ドメイン]** リストに表示されていることを確認します。  
  
##  <a name="follow-up-after-importing-a-domain-from-a-dqs-file"></a><a name="FollowUp"></a> 補足情報: .dqs ファイルからドメインをインポートした後  
 .dqs ファイルからドメインをインポートした後、ドメインの内容に応じて、ナレッジをドメインに追加したり、ドメインをクレンジング プロジェクトや照合プロジェクトで使用したりすることができます。 詳しくは、「[ナレッジ検出の実行](../data-quality-services/perform-knowledge-discovery.md)」、「[ドメインの管理](../data-quality-services/managing-a-domain.md)」、「[複合ドメインの管理](../data-quality-services/managing-a-composite-domain.md)」、「[照合ポリシーの作成](../data-quality-services/create-a-matching-policy.md)」、「[データ クレンジング](../data-quality-services/data-cleansing.md)」、または「[データ照合](../data-quality-services/data-matching.md)」をご覧ください。  
  
  
