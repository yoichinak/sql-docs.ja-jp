---
description: ポリシー ベースの管理ポリシーのエクスポート
title: ポリシー ベースの管理ポリシーのエクスポート | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, export policy
ms.assetid: f0001b33-9078-4432-8460-496736fb325a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 62fff3bda286f50b2220dbb1ea4732547e98829f
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127867"
---
# <a name="export-a-policy-based-management-policy"></a>ポリシー ベースの管理ポリシーのエクスポート
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でポリシー ベースの管理ポリシーをエクスポートする方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **以下を使用してポリシーをエクスポートするには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 msdb データベースの PolicyAdministratorRole ロールのメンバーシップが必要です。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-export-a-policy"></a>ポリシーをエクスポートするには  
  
1.  オブジェクト エクスプローラーで、エクスポートするポリシー ベースの管理ポリシーを含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[管理]** フォルダーを展開します。  
  
3.  プラス記号をクリックして **[ポリシー管理]** を展開します。  
  
4.  プラス記号をクリックして **[ポリシー]** フォルダーを展開します。  
  
5.  エクスポートするポリシーを右クリックし、 **[ポリシーのエクスポート]** をクリックします。  
  
6.  **[ポリシーのエクスポート]** ダイアログ ボックスで、アドレス バーにファイルのパスと名前を入力します。 または、ダイアログ ボックスのナビゲーション ウィンドウでファイルの適切な場所を見つけ、 **[ファイル名]** ボックスに XML ファイルの名前を入力します。  
  
7.  完了したら、 **[保存]** をクリックします。  

