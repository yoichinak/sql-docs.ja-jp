---
description: オペレーターへの警告の割り当て
title: オペレーターへの警告の割り当て
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- assigning alerts to operator
- SQL Server Agent, alerts
- alerts [SQL Server], assigning to operator
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: aa818155-6fa2-4565-a09f-5c7e31c89754
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 33621e680b958bf6945fb26fa82209ee640ba9f2
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92033953"
---
# <a name="assign-alerts-to-an-operator"></a>オペレーターへの警告の割り当て

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告をオペレーターに割り当てて、ジョブに関する通知を受信できるようにする方法について説明します。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>はじめに  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>制限事項と制約事項  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、警告システム全体を簡単に管理できるグラフィカルなツールです。 警告システムを構成するときには、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用することをお勧めします。  
  
-   警告に対応して通知を送るには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがメールを送れるようにあらかじめ構成しておく必要があります。 詳細については、「 [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)」を参照してください。  
  
-   電子メールのメッセージやポケットベルによる通知に失敗した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス エラー ログに失敗がレポートされます。  
  
### <a name="security"></a><a name="Security"></a>セキュリティ  
  
#### <a name="permissions"></a><a name="Permissions"></a>アクセス許可  
オペレーターに警告を割り当てることができるのは、 **sysadmin** 固定サーバー ロールのメンバーだけです。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-assign-alerts-to-an-operator"></a>オペレーターに警告を割り当てるには  
  
1.  **オブジェクト エクスプローラー**で、警告を割り当てるオペレーターを含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  プラス記号をクリックして **[オペレーター]** フォルダーを展開します。  
  
4.  警告を割り当てるオペレーターを右クリックし、 **[プロパティ]** を選択して、 **[通知]** ページを選択します。  
  
5.  _[operator\_name_**のプロパティ]** ダイアログ ボックスで、 **[ページの選択]** の **[通知]** を選択します。  
  
6.  **[このユーザーに送信された通知の表示方法]** で、 **[警告]** を選択してこのオペレーターに送信する警告の一覧を表示するか、または **[ジョブ]** を選択してこのオペレーターに通知を送信するジョブの一覧を表示します。 **[電子メール]**、 **[ポケットベル]**、 **[Net Send]** のチェック ボックスの中から 1 つ以上を選択し、必要に応じて通知ごとに通知方法を定義します。  
  
7.  完了したら、 **[OK]** をクリックします。  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-assign-alerts-to-an-operator"></a>オペレーターに警告を割り当てるには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- adds an e-mail notification for the specified alert (Test Alert)  
    -- This example assumes that Test Alert already exists
    -- and that François Ajenstat is a valid operator name.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_notification  
     @alert_name = N'Test Alert',  
     @operator_name = N'François Ajenstat',  
     @notification_method = 1 ;  
    GO  
    ```  
  
詳細については、「 [sp_add_notification (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)」を参照してください。  
