---
description: ポリシー ベースの管理ポリシーがスケジュールに従っていることの評価
title: ポリシー ベースの管理ポリシーがスケジュールに従っていることの評価 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: bea09522-ff47-4037-ab55-a98ea7c10099
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 79e16f9a39e235f7ceed5a77e55d03f4c5efed72
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127875"
---
# <a name="evaluate-a-policy-based-management-policy-on-a-schedule"></a>ポリシー ベースの管理ポリシーがスケジュールに従っていることの評価
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でポリシー ベースの管理ポリシーがスケジュールに従っていることを評価する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **以下を使用してポリシーがスケジュールに従っていることを評価するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-evaluate-a-policy-on-a-schedule"></a>ポリシーがスケジュールに従っていることを評価するには  
  
1.  **オブジェクト エクスプローラー** で、評価するポリシーのスケジュールを含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[管理]** フォルダーを展開します。  
  
3.  プラス記号をクリックして **[ポリシー管理]** を展開します。  
  
4.  プラス記号をクリックして **[ポリシー]** フォルダーを展開します。  
  
5.  スケジュールを評価するポリシーを右クリックし、 **[プロパティ]** をクリックします。  
  
6.  **[ポリシーを開く - <_ポリシー名_>]** ダイアログ ボックスで、 **[評価モード]** ボックスの一覧の **[スケジュールで実行]** をクリックします。  
  
7.  **[スケジュール]** で、 **[選択]** をクリックして既存のスケジュールを指定するか、 **[新規作成]** をクリックして新しいスケジュールを作成します。  
  
8.  完了したら、 **[OK]** をクリックします。  
  
  
