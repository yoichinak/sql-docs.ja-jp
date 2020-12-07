---
description: Configure a User to Create and Manage SQL Server Agent Jobs
title: Configure a User to Create and Manage SQL Server Agent Jobs
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cbe9bfd3727e90b330ea894ba3e2fdc590486a29
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035675"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>Configure a User to Create and Manage SQL Server Agent Jobs

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このトピックでは、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを作成または実行するユーザーを構成する方法について説明します。  

- **作業を開始する準備:** [セキュリティ](#Security)  
 
- **SQL Server エージェント ジョブを作成または管理するユーザーを構成するために使用するもの:**  [SQL Server Management Studio](#SSMS)  

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>はじめに  
  
### <a name="security"></a><a name="Security"></a>セキュリティ  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを作成または実行するユーザーを構成するには、まず、msdb データベース内の次のいずれかの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールに、既存の SQL Server ログインまたは msdb ロールを追加する必要があります: SQLAgentUserRole、SQLAgentReaderRole、または SQLAgentOperatorRole。  
  
既定では、これらのデータベース ロールのメンバーは、メンバー自身が実行する独自のジョブ ステップを作成できます。 このような管理者権限のないユーザーが他の種類のジョブ ステップ ( [!INCLUDE[ssIS](../../includes/ssis_md.md)] パッケージなど) を実行するには、プロキシ アカウントへのアクセスが必要です。 sysadmin 固定サーバー ロールのすべてのメンバーには、プロキシ アカウントを作成、変更、および削除する権限があります。 これら [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定のデータベース ロールに関連付けられている権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
#### <a name="permissions"></a><a name="Permissions"></a>アクセス許可  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>SQL Server Management Studio の使用  
**SQL ログインまたは msdb ロールを SQL Server エージェント固定データベース ロールに追加するには**  
  
1.  **オブジェクト エクスプローラー**で、サーバーを展開します。  
  
2.  **[セキュリティ]** を展開し、 **[ログイン]** を展開します。  
  
3.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールに追加するログインを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[ログインのプロパティ]** ダイアログ ボックスの **[ユーザー マッピング]** ページで、 **msdb**を含む行を選択します。  
  
5.  **[データベース ロールのメンバーシップ: msdb]** で、該当する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールのチェック ボックスをオンにします。  
  
**SQL Server エージェント ジョブ ステップを作成および管理できるようにプロキシ アカウントを構成するには**  
  
1.  **オブジェクト エクスプローラー**で、サーバーを展開します。  
  
2.  **[SQL Server エージェント]** を展開します。  
  
3.  **[プロキシ]** を右クリックして **[新しいプロキシ]** をクリックします。  
  
4.  **[新しいプロキシ アカウント]** ダイアログの **[全般]** ページで、新しいプロキシのプロキシ名、資格情報名、および説明を指定します。 SQL Server エージェントのプロキシを作成する前に、まず資格情報を作成する必要があることに注意してください。 資格情報の作成の詳細については、「[資格情報の作成](../../relational-databases/security/authentication-access/create-a-credential.md)」および「[CREATE CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md)」を参照してください。  
  
5.  このプロキシに適したサブシステムを確認します。
    1. [オペレーティング システム (CmdExec)](create-a-cmdexec-job-step.md)
    1. [SQL Server Analysis Services クエリ](create-an-analysis-services-job-step.md#to-create-an-analysis-services-query-job-step)
    1. [SQL Server Analysis Services コマンド](create-an-analysis-services-job-step.md#to-create-an-analysis-services-command-job-step-1)
    1. [SQL Server Integration Services パッケージ](../../integration-services/packages/run-integration-services-ssis-packages.md)
    1. [PowerShell](../../powershell/run-windows-powershell-steps-in-sql-server-agent.md)
  
6.  **[プリンシパル]** ページで、プロキシ アカウントへのアクセスを許可するログインまたはロールを追加するか、あるいは拒否するログインまたはロールを削除します。  

## <a name="see-also"></a>関連項目
- [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)