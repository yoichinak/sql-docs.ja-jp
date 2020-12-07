---
description: オペレーターの作成
title: オペレーターの作成
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, operators
- jobs [SQL Server Agent], notification options
- operators (users) [Database Engine], creating with Management Studio
- SQL Server Agent jobs, notification options
- jobs [SQL Server Agent], operators
- notifications [SQL Server], job status
ms.assetid: 1359d790-5905-4927-a208-e7155e7768a2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bad9dcc1d3fad1e7f0359d7805f93cbe44cb7652
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035047"
---
# <a name="create-an-operator"></a>オペレーターの作成
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブに関する通知を受信するようにユーザーを構成する方法について説明します。  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>はじめに  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>制限事項と制約事項  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の今後のバージョンでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントからポケットベル オプションと **net send** オプションが削除される予定です。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。  
  
-   SQL Server エージェントは、データベース メールを使用して、電子メールおよびポケットベルによる通知をオペレーターへ送信するように構成する必要があります。 詳細については、「 [オペレーターへの警告の割り当て](assign-alerts-to-an-operator.md)」を参照してください。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、ジョブを簡単に管理できるグラフィカルなツールです。ジョブのインフラストラクチャを作成し、管理するには、このツールを使用することをお勧めします。  
  
### <a name="security"></a><a name="Security"></a>セキュリティ  
  
#### <a name="permissions"></a><a name="Permissions"></a>アクセス許可  
オペレーターを作成できるのは、 **sysadmin** 固定サーバー ロールのメンバーだけです。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-create-an-operator"></a>オペレーターを作成するには  
  
1.  **オブジェクト エクスプ ローラー**で、SQL Server エージェント オペレーターを作成するサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  **[オペレーター]** フォルダーを右クリックし、 **[新しいオペレーター]** を選択します。  
  
    **[新しいオペレーター]** ダイアログ ボックスの **[全般]** ページでは、次のオプションを使用できます。  
  
    **名前**  
    オペレーターの名前を変更します。  
  
    **Enabled**  
    オペレーターを有効にします。 有効になっていない場合は、オペレーターに通知が送信されません。  
  
    **[電子メール名]**  
    オペレーターの電子メール アドレスを指定します。  
  
    **[Net Send アドレス]**  
    **net send**に使用するアドレスを指定します。  
  
    **[ポケットベル用電子メール ログイン名]**  
    オペレーターのポケットベルに使用する電子メール アドレスを指定します。  
  
    **[ポケットベルの受信スケジュール]**  
    ポケットベルをアクティブにする時間を設定します。  
  
    **[月曜日] ～ [日曜日]**  
    ポケットベルをアクティブにする日を選択します。  
  
    **[始業時刻]**  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがポケットベルへのメッセージ送信を開始する時刻を選択します。  
  
    **[終業時刻]**  
    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがポケットベルへのメッセージ送信を終了する時刻を選択します。  
  
    **[新しいオペレーター]** ダイアログ ボックスの **[通知]** ページでは、次のオプションを使用できます。  
  
    **警告**  
    インスタンス内の警告を表示します。  
  
    **ジョブ**  
    インスタンス内のジョブを表示します。  
  
    **[警告の一覧]**  
    インスタンス内の警告を一覧表示します。  
  
    **[ジョブ一覧]**  
    インスタンス内のジョブを一覧表示します。  
  
    **電子メール**  
    電子メールを使用してこのオペレーターに通知します。  
  
    **ポケットベル**  
    電子メールをポケット ベルに送信することによって、このオペレーターに通知します。  
  
    **Net send**  
    **net send**を使用してこのオペレーターに通知します。  
  
4.  新しいオペレーターの作成が完了したら、 **[OK]** をクリックします。  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-create-an-operator"></a>オペレーターを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- sets up the operator information for user 'danwi.'
    -- The operator is enabled.   
    -- SQL Server Agent sends notifications by pager 
    -- from Monday through Friday from 8 A.M. to 5 P.M.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_operator  
        @name = N'Dan Wilson',  
        @enabled = 1,  
        @email_address = N'danwi',  
        @pager_address = N'5551290AW@pager.Adventure-Works.com',  
        @weekday_pager_start_time = 080000,  
        @weekday_pager_end_time = 170000,  
        @pager_days = 62 ;  
    GO  
    ```  
  
詳細については、「 [sp_add_operator (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)」を参照してください。  
