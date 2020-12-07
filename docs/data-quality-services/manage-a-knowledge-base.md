---
description: ナレッジ ベースの管理
title: ナレッジ ベースの管理
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 27f306f4-d67c-47f5-b35c-4260cc5d36e3
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 5676a182615dfa7ddf23dcda1841a6530467a8c0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462084"
---
# <a name="manage-a-knowledge-base"></a>ナレッジ ベースの管理

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  このトピックでは、 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) のナレッジ ベースに対して管理機能を実行する方法について説明します。 ナレッジ ベースの削除、ロック解除、作業の破棄、名前の変更、およびプロパティの表示を行うことができます。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
 ナレッジ ベースを管理するには、ナレッジ ベースが既に作成されていて、発行済みであるか (他のユーザーが作成した場合) または閉じられている (自分で作成した場合) 必要があります。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 ナレッジ ベースを開くには、DQS_MAIN データベースの dqs_kb_editor ロールまたは dqs_administrator ロールを所有している必要があります。  
  
##  <a name="manage-a-knowledge-base"></a><a name="Manage"></a> ナレッジベースの管理  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client アプリケーションを実行](../data-quality-services/run-the-data-quality-client-application.md)します。  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] のホーム画面で **[ナレッジ ベースを開く]** をクリックします。  
  
3.  ナレッジ ベース テーブル内のナレッジ ベースを右クリックします。  
  
4.  コンテキスト メニューでは、以下の操作を実行できます。  
  
    1.  **[開く]**: クリックすると、 **[アクティビティの選択]** ペインで選択したアクティビティでナレッジ ベースが開きます。  
  
    2.  **[ロック解除]**: ドメイン管理、ナレッジ検出、およびポリシー照合の各アクティビティのいずれかの手順でナレッジ ベースを操作していて、それを閉じたユーザーである場合は、ナレッジ ベースのロックを解除できます。 ナレッジ ベースをアンロードすると、別のユーザーがナレッジ ベースを開いて操作できるようになります。 このコマンドは、ナレッジ ベースがアクティビティの状態でない場合には使用できません。 詳細については、「 [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)」を参照してください。  
  
    3.  **[作業の破棄]**: ナレッジ ベースが作業中の状態になっている場合にクリックします。ナレッジ ベースの状態は、テーブルの [状態] フィールドのエントリで示されます。 このコマンドは、ナレッジ ベースがアクティビティの状態でない場合、およびナレッジ ベースがロックされている場合には使用できません。 詳細については、「 [Open a Knowledge Base](../data-quality-services/open-a-knowledge-base.md)」を参照してください。  
  
    4.  **[名前の変更]**: クリックすると、右クリックしたナレッジ ベースについて、テーブルの [ナレッジ ベース] フィールドが編集可能になります。 名前を変更し、そのナレッジ ベースとフィールド内の別のナレッジ ベースをクリックして名前の変更を受け入れます。  
  
    5.  **[削除]**: クリックすると、 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]の DQS_MAIN データベースからナレッジ ベースを削除します。  
  
    6.  **[プロパティ]**: クリックすると、データベースのプロパティを読み取り専用で表示します。  
  
        1.  **[ソース ナレッジ ベース]**: このデータベースの基になっているナレッジ ベースです。 これは省略可能です。  
  
        2.  **[状態]**: ナレッジ ベースの状態が **[作業中]** になっているかどうか、および特定のナレッジ マネージメント アクティビティになっているかどうかを示します。ナレッジ ベースの状態は、ナレッジ ベースが最後に閉じられたときに決定されます。 状態は、 **[作業中]**(ナレッジ ベースはナレッジ マネージメント セッションで開かれていますが、特定のアクティビティになっていません) または **[作業中]** かつナレッジ マネージメント アクティビティ (ナレッジ ベースはナレッジ マネージメント セッションで開かれていて、特定のアクティビティになっています) のいずれかです。  
  
        3.  **[ロック]**: ナレッジ ベースがロックされている場合は **[True]** 、ロックされていない場合は **[False]**  
  
        4.  **[発行されていないコンテンツを含む]**: ナレッジ ベースが発行によって保存されていないコンテンツを含んでいる場合は [True]、含んでいない場合は [False]  
  
        5.  **[ロックしているユーザー]**: ナレッジ ベースを閉じてロックしたユーザーの名前  
  
        6.  **[ロックされた日付]**: ロックされた日付  
  
        7.  **[作成者]**: ナレッジ ベースを作成したユーザーの名前とそのユーザーが属しているネットワーク  
  
        8.  **[作成日]**: 作成された日付  
  
##  <a name="follow-up-after-managing-a-knowledge-base"></a><a name="FollowUp"></a> 補足情報: ナレッジベースを管理した後  
 ナレッジ ベースを管理した後の次の手順は、ナレッジ ベースに対して実行したアクションによって異なります。  
  
-   ナレッジ ベースを開いた場合は、選択したアクティビティで続行します。  
  
-   ナレッジ ベースのロックを解除した場合は、別のユーザーがそのナレッジ ベースを示された状態で開いて作業できるようになります。  
  
-   ナレッジ ベースに対する作業を破棄した場合、ナレッジ ベースは最後に発行された状態で使用できるようになります。  
  
-   ナレッジ ベースの名前を変更した場合は、名前を変更したナレッジ ベースを開いて作業する必要があります。  
  
-   ナレッジ ベースを削除した場合は、別のナレッジ ベースを選択して作業するか、新しいナレッジ ベースを作成する必要があります。  
  
  
