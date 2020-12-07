---
description: データベース メールを使用するように SQL Server エージェント メールを構成する
title: データベース メールを使用するように SQL Server エージェント メールを構成する
ms.date: 08/05/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], SQL Server Agent Mail
- SQL Server Agent Mail
ms.assetid: 4b8b61bd-4bd1-43cd-b6e5-c6ed2e101dce
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
ms.openlocfilehash: 44252fa011dcdeaca457d6aa7f9819f581dbeb11
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96125259"
---
# <a name="configure-sql-server-agent-mail-to-use-database-mail"></a>データベース メールを使用するように SQL Server エージェント メールを構成する
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の通知と警告をデータベース メールを使用して送信するように [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]エージェントを構成する方法について説明します。  データベース メール機能を有効にして構成する方法の詳細については、「 [データベース メールの構成](../../relational-databases/database-mail/configure-database-mail.md)」を参照してください。  [!INCLUDE[tsql](../../includes/tsql-md.md)]の使用例については、「 [データベース メール プロファイルの作成](../../relational-databases/database-mail/create-a-database-mail-profile.md)」をご覧ください。
  
-   **作業を開始する準備:**  
  
-   [前提条件](#Prerequisites)  
  
-   [Security](#Security)  
  
-   [SQL Server Management Studio でデータベース メールを使用するように SQL Server エージェントを構成するには](#SSMSProcedure)  
  
-   [フォロー アップ タスク](#Follow_Up)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
  > [!NOTE]
  > Managed Instance 上の SQL エージェントは常に、データベース メールを使用するように構成されます。そのため、このコンテンツはマネージド インスタンスには該当しません。 Managed Instance では、SQL エージェントとデータベース メールをバインドする目的でプロファイルを用意する必要があります。このプロファイルの名前は **[AzureManagedInstance_dbmail_profile](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)** という名前にする必要があります。 
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 前提条件  
  
-   [データベース メールを有効にします](../../relational-databases/database-mail/configure-database-mail.md)。  
  
-    使用する[エージェント サービス アカウントの](../../relational-databases/database-mail/create-a-database-mail-account.md) データベース メール アカウントを作成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。  
  
-   [エージェント サービス アカウントで使用する](../../relational-databases/database-mail/create-a-database-mail-profile.md) データベース メール プロファイルを作成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] し、ユーザーを **msdb** データベースの **DatabaseMailUserRole** に追加します。
  
-   作成したプロファイルを **msdb** データベースの既定のプロファイルに設定します。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 プロファイル アカウントを作成し、ストアド プロシージャを実行するユーザーは、sysadmin 固定サーバー ロールのメンバーである必要があります。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **データベース メールを使用するように SQL Server エージェントを構成するには**  
  
-   オブジェクト エクスプローラーで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを展開します。  
  
-   **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** をクリックします。  
  
-   **[警告システム]** をクリックします。  
  
-   **[メール プロファイルを有効にする]** チェック ボックスをオンにします。  
  
-   **[メール システム]** ボックスの一覧で、 **[データベース メール]** を選択します。  
  
-   **[メール プロファイル]** ボックスの一覧で、データベース メールのメール プロファイルを選択します。 
  
-   SQL Server エージェントを再起動します。  
  
##  <a name="follow-up-tasks"></a><a name="Follow_Up"></a> フォロー アップ タスク  
 警告および通知を送信できるようにエージェントを構成するには、次のタスクが必要となります。  
  
-   [警告](../../ssms/agent/alerts.md)  
  
     特定のデータベース イベントまたはオペレーティング システムの状態がオペレーターに通知されるように、警告を構成できます。  
  
-   [オペレーター](../../ssms/agent/operators.md)  
  
     オペレーターとは、電子通知を受け取ることのできる人またはグループの別名です。  
  
