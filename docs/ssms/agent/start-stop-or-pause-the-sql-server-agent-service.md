---
description: Start, Stop, or Pause the SQL Server Agent Service
title: サービスの開始、停止、または一時停止
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, starting
- SQL Server Agent, pausing
- SQL Server Agent, stopping
ms.assetid: c95a9759-dd30-4ab6-9ab0-087bb3bfb97c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 02bc27675493e7e8d1b5c5012d7541c0ad295bae
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038756"
---
# <a name="start-stop-or-pause-the-sql-server-agent-service"></a>Start, Stop, or Pause the SQL Server Agent Service

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の SQL Server エージェント サービスを開始、停止、または一時停止する方法について説明します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスは、オペレーティング システムの起動時に自動的に開始するよう構成したり、ジョブの完了が必要なときに手動で開始できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを停止または一時停止して、ジョブ、オペレーターへの通知、および警告を中断できます。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>はじめに  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>制限事項と制約事項  
  
-   管理タスクを自動化するためには、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがサービスとして実行されている必要があります。 詳細については、「 [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md)」をご覧ください。  
  
-   オブジェクト エクスプローラーに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ノードが表示されるのは、このノードの使用権限がある場合に限られます。  
  
### <a name="security"></a><a name="Security"></a>セキュリティ  
  
#### <a name="permissions"></a><a name="Permissions"></a>アクセス許可  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの機能を実行するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]固定サーバー ロールの **sysadmin** のメンバーであるアカウントの資格情報を使用するように構成する必要があります。 このアカウントには、次の Windows 権限が必要です。  
  
-   サービスとしてログオン (SeServiceLogonRight)  
  
-   プロセス レベル トークンを置き換える (SeAssignPrimaryTokenPrivilege)  
  
-   スキャン チェックを行わない (SeChangeNotifyPrivilege)  
  
-   プロセスに対してメモリ クォータを調整する (SeIncreaseQuotaPrivilege)  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントに必要な Windows 権限の詳細については、「 [SQL Server エージェント サービスのアカウントの選択](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) 」および「 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)」を参照してください。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-start-stop-or-restart-the-sql-server-agent-service"></a>SQL Server エージェント サービスを開始、停止、または一時停止するには  
  
1.  **オブジェクト エクスプ ローラー**で、プラス記号をクリックして、管理する SQL Server エージェント サービスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[開始]**、 **[停止]**、または **[再起動]** を選択します。  
  
3.  **[ユーザー アカウント制御]** ダイアログ ボックスで、**[はい]** をクリックします。  
  
4.  アクションを実行するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。  
  
詳細については、次を参照してください。  
  
-   [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)  
  
-   [SQL Server エージェントの自動起動 (SQL Server Management Studio)](../../ssms/agent/autostart-sql-server-agent-sql-server-management-studio.md)  
