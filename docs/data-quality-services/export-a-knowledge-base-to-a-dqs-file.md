---
description: .dqs ファイルへのナレッジ ベースのエクスポート
title: .dqs ファイルへのナレッジ ベースのエクスポート
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a324ead5-c8aa-4e26-abe3-ef415add00f8
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 946b1192b314c5303cd529c176e93ebf1fb0204f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457938"
---
# <a name="export-a-knowledge-base-to-a-dqs-file"></a>.dqs ファイルへのナレッジ ベースのエクスポート

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) で .dqs データ ファイルにナレッジ ベース全体をエクスポートする方法について説明します。 ドメインまたはナレッジ ベース全体をデータ ファイルにエクスポートできます。 ドメインのエクスポートについては、「[.dqs ファイルへのドメインのエクスポート](../data-quality-services/export-a-domain-to-a-dqs-file.md)」をご覧ください。  
  
 ナレッジ ベースを .dqs ファイルにエクスポートし、後で別のナレッジ ベースとしてインポートすることで、ナレッジの生成処理を簡略化し、時間と労力を節約します。 ナレッジ ベースやその中のナレッジを他のユーザーと共有できます。 .dqs ファイルには、ドメインや照合ポリシーを含むナレッジ ベースのすべての情報が含まれます。ただし、アタッチされた参照データ情報は含まれません。 .dqs ファイルをインポートした後、必要に応じて、必要なドメインを適切な参照データ サービスに再度アタッチします。 ナレッジ ベース内の発行済みのデータと発行されていないデータの両方がエクスポートされます。  
  
 エクスポート処理で作成された .dqs データ ファイルは暗号化されるため、内容を表示することはできません。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
 ナレッジ ベースを .dqs データ ファイルにエクスポートするには、ナレッジ ベースを作成して開いておく必要があります。 エクスポート先の .dqs ファイルを用意する必要はありません。1 .dqs ファイルは作成されます。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 ナレッジ ベースを .dqs データ ファイルにエクスポートするには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールが必要です。  
  
##  <a name="export-a-knowledge-base-to-a-dqs-file"></a><a name="Export"></a> ナレッジベースを dqs ファイルにエクスポートする  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で、ドメイン管理アクティビティ内のナレッジ ベースを開きます。  
  
3.  [ドメイン管理] ページで (任意のタブを選択し)、ドメイン リストの上にある **[ナレッジ ベース データをエクスポートします]** アイコンをクリックして、 **[ナレッジ ベースのエクスポート]** をクリックします。 または、 **[ドメイン]** リスト内で右クリックして **[エクスポート]** にマウス ポインターを合わせ、 **[ナレッジ ベースのエクスポート]** をクリックします。  
  
4.  **[データ ファイルにエクスポート]** ダイアログ ボックスで、ファイルを保存するフォルダーに移動し、ファイルに名前を付けるかナレッジ ベース名のままにし、**[ファイルの種類]** を **[DQS データ ファイル (\*.dqs)]** のままにして、**[保存]** をクリックします。  
  
5.  **[ナレッジ ベースのエクスポート]** ダイアログ ボックスで、ステータス行にエクスポートの完了が表示されていることを確認します。 **[OK]** をクリックします。  
  
##  <a name="follow-up-after-exporting-a-domain-to-a-dqs-file"></a><a name="FollowUp"></a> 補足情報: ドメインを .dqs ファイルにエクスポートした後  
 ナレッジ ベースを .dqs ファイルにエクスポートした後で、そのナレッジ ベースを (新しい名前で) 同じ [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] にインポートしたり、異なる [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]にインポートしたりできます。  
  
  
