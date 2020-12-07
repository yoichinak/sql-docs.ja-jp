---
description: ジョブの作成
title: ジョブの作成
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: 465fb7fc-7622-4252-a178-ea51691c935b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3d4559bb32152f7e4ba99f7d598c3f9080caccc9
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038015"
---
# <a name="create-jobs"></a>ジョブの作成
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

ジョブとは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって順番に実行される一連の操作です。 ジョブは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト、コマンド プロンプト アプリケーション、Microsoft ActiveX スクリプト、Integration Services パッケージ、Analysis Services コマンドおよびクエリ、レプリケーション タスクの実行など、広範な操作を実行できます。 ジョブは、反復的なタスクやスケジュール可能なタスクを実行でき、警告を発生させてジョブのステータスをユーザーに自動的に通知できるので、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の管理が非常に簡単になります。  
  
ジョブを作成するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールか **sysadmin** 固定サーバー ロールのメンバーである必要があります。 ジョブの編集は、ジョブの所有者または **sysadmin** ロールのメンバーのみが行うことができます。 **sysadmin** ロールのメンバーは、別のユーザーにジョブの所有権を割り当てることができ、そのユーザーはジョブの所有者とは無関係にジョブを実行できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント固定データベース ロールの詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
ジョブは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンスまたは企業全体の複数のインスタンスで実行するように記述できます。 複数のサーバーでジョブを実行するには、最低 1 つのマスター サーバーと 1 つ以上のターゲット サーバーをセットアップする必要があります。 マスター サーバーとターゲット サーバーの詳細については、「[エンタープライズ全体の管理の自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)」をご覧ください。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントにより、ジョブとジョブ ステップの情報がジョブ履歴に記録されます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|説明|トピック|  
|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを作成する方法について説明します。|[ジョブの作成](../../ssms/agent/create-a-job.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブの所有権を他のユーザーに再割り当てする方法について説明します。|[Give Others Ownership of a Job](../../ssms/agent/give-others-ownership-of-a-job.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ履歴ログをセットアップする方法について説明します。|[Set Up the Job History Log](../../ssms/agent/set-up-the-job-history-log.md)|  
  
## <a name="see-also"></a>参照  
[ジョブ ステップの管理](../../ssms/agent/manage-job-steps.md)  
[エンタープライズ全体の管理の自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[スケジュールの作成とジョブへのアタッチ](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[ジョブの実行](../../ssms/agent/run-jobs.md)  
[ジョブの表示または変更](../../ssms/agent/view-or-modify-jobs.md)  
