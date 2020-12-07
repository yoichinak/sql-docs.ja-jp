---
description: ジョブの表示または変更
title: ジョブの表示または変更
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f6765a371624248f1accd46fa9cfa708ad22e817
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92030588"
---
# <a name="view-or-modify-jobs"></a>ジョブの表示または変更
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

作成したジョブはどのジョブでも表示できます。 ジョブの実行後は、履歴を表示することもできます。 ジョブの履歴を表示すると、ジョブを実行した時間、ジョブ全体のステータス、およびジョブを構成するジョブ ステップごとのステータスを確認できます。 これまでにジョブが失敗したことがあるかどうか、最後にジョブが正常に実行されたのはいつか、各ジョブの実行でジョブにより作成された出力はどのようなものかを確認できます。 **sysadmin** 固定サーバー ロールのメンバーは、ジョブの所有者がだれであるかにかかわらず、すべてのジョブを表示または変更できます。  
  
> [!NOTE]  
> 一度も実行されていないジョブには、ジョブ履歴はありません。 ジョブ履歴ログ全体のサイズとジョブごとのサイズは制限できます。  
  
また、新たな要件に合わせて、ジョブは変更できます。 次の項目を変更できます。  
  
-   応答オプション  
  
-   スケジュール  
  
-   ジョブ ステップ  
  
-   所有権  
  
-   ジョブ カテゴリ  
  
-   ターゲット サーバー (マルチサーバー ジョブの場合のみ)  
  
マルチサーバー ジョブに対する変更を確実に有効にするには、ターゲット サーバーが更新されたジョブをダウンロードできるように、変更をダウンロード一覧に適用する必要があります。 ターゲット サーバーが最新のジョブ定義を保持するようにするには、マルチサーバー ジョブの更新後に、次のような INSERT 命令を通知します。  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
詳細については、「 [sp_purge_jobhistory (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)」をご覧ください。  
  
**sysadmin** 固定サーバー ロールのメンバーは、あらゆるジョブに対して、ジョブの定義や履歴を表示したり、ジョブを変更したりできます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|説明|トピック|  
|-|-|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを表示する方法について説明します。|[View a Job](../../ssms/agent/view-a-job.md)|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ履歴ログを表示する方法について説明します。|[View the Job History](../../ssms/agent/view-the-job-history.md)|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ履歴ログの内容を削除する方法について説明します。|[Clear the Job History Log](../../ssms/agent/clear-the-job-history-log.md)|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ履歴ログのサイズ制限を設定する方法について説明します。|[Resize the Job History Log](../../ssms/agent/resize-the-job-history-log.md)|  
|[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエージェント ジョブのプロパティを変更する方法について説明します。|[Modify a Job](../../ssms/agent/modify-a-job.md)|  
  
## <a name="see-also"></a>参照  
[sysjobhistory](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
