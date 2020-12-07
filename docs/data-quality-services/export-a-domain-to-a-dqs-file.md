---
description: .dqs ファイルへのドメインのエクスポート
title: .dqs ファイルへのドメインのエクスポート
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eba10d3d-b5c4-447b-8a30-fa07996cb28e
author: swinarko
ms.author: sawinark
ms.openlocfilehash: d3e37309a430b92e12493c178eeaf7a117a41552
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484888"
---
# <a name="export-a-domain-to-a-dqs-file"></a>.dqs ファイルへのドメインのエクスポート

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) でドメインを .dqs ファイルにエクスポートする方法について説明します。 ドメインまたはナレッジ ベース全体をデータ ファイルにエクスポートできます。 ナレッジ ベースのエクスポートについては、「[.dqs ファイルへのナレッジ ベースのエクスポート](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)」をご覧ください。  
  
 ナレッジ ベースからドメインを .dqs データ ファイルにエクスポートし、別のナレッジ ベースにインポートすることで、ナレッジの生成処理を簡略化し、時間と労力を節約します。 ドメインやその中のナレッジを他のユーザーと共有できます。  
  
 1 つの単一ドメインまたは 1 つの複合ドメインをエクスポートできます。 単一ドメインについての .dqs ファイルには、ドメインのプロパティ、値、ルールを含む、ドメインのすべてのデータが格納されています。ただし、アタッチされた参照データ情報は格納されません。 複合ドメインについての .dqs ファイルには、複合ドメインに含まれるドメインのすべてのドメイン データと複合ドメインのプロパティ、リレーション、ルールを含む、複合ドメインのすべてのデータが格納されています。ただし、参照データ情報は格納されません。 .dqs ファイルをインポートした後、必要に応じて、ドメインまたは複合ドメインを適切な参照データ サービスに再度アタッチします。 発行済みのデータと発行されていないデータの両方がエクスポートされます。  
  
 エクスポート処理で作成された .dqs データ ファイルは暗号化されるため、内容を表示することはできません。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
 ドメインを .dqs データ ファイルにエクスポートするには、1 つの単一ドメインまたは 1 つの複合ドメイン (複数の単一ドメインで構成されるドメイン) を作成および選択しておく必要があります。 エクスポート先の .dqs ファイルを用意する必要はありません。1 .dqs ファイルは作成されます。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 ドメインを .dqs データ ファイルにエクスポートするには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="export-a-domain-to-a-dqs-file"></a><a name="Export"></a> Dqs ファイルにドメインをエクスポートする  
 [ドメイン管理] の任意のページからエクスポートできます。 エクスポート コマンドは、ユーザー インターフェイスのコントロールから実行することも、[ドメイン リスト] ペインのショートカット メニューのコマンドから実行することもできます。  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、ドメイン管理アクティビティ内のナレッジ ベースを開きます。  
  
3.  **[ドメイン管理]** ページ (任意のタブを選択) の **[ドメイン]** リストで、単一ドメインまたは複合ドメインを選択します。  
  
4.  ドメイン リストの上にある **[ナレッジ ベース データをエクスポートします]** アイコンをクリックして、 **[ドメインのエクスポート]** をクリックします。 または、 **[ドメイン]** リスト内でドメインを右クリックして **[エクスポート]** をポイントし、 **[ドメインのエクスポート]** をクリックします。  
  
5.  **[データ ファイルにエクスポート]** ダイアログ ボックスで、ファイルを保存するフォルダーに移動し、ファイルに名前を付けるか既定の名前のままにし、**[ファイルの種類]** を **[DQS データ ファイル (\*.dqs)]** のままにして、**[保存]** をクリックします。  
  
6.  **[ドメインのエクスポート]** ダイアログ ボックスで、ステータス行にエクスポートの完了が表示されていることを確認します。 **[OK]** をクリックします。  
  
##  <a name="follow-up-after-exporting-a-domain-to-a-dqs-file"></a><a name="FollowUp"></a> 補足情報: ドメインを .dqs ファイルにエクスポートした後  
 ドメインを .dqs ファイルにエクスポートしたら、そのドメインを別のナッレジ ベースにインポートすることができます。  
  
  
