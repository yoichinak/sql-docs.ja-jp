---
description: ジョブの実装
title: ジョブの実装
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent]
- SQL Server Agent jobs
- SQL Server Agent jobs, about jobs
- jobs [SQL Server Agent], about jobs
ms.assetid: 69e06724-25c7-4fb3-8a5b-3d4596f21756
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: f9e6a036c6647abe0cac99d28e3f00d440bb666a
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034952"
---
# <a name="implement-jobs"></a>ジョブの実装
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを使用すると、定型的な管理作業を自動化して定期的に実行し、管理を効率化できます。  
  
ジョブとは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって順番に実行される一連の操作です。 ジョブで実行できる操作は多岐にわたり、 [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト、コマンド ライン アプリケーション、Microsoft ActiveX スクリプト、Integration Services パッケージ、Analysis Services のコマンドおよびクエリ、レプリケーション タスクなどを実行できます。 ジョブでは、繰り返し行う作業や、スケジュールに設定できる作業を実行できます。また、警告を生成してジョブの状態をユーザーに自動的に通知できるので、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の管理を大幅に簡素化できます。  
  
ジョブは手動で実行することも、スケジュールや警告に応じて実行されるように構成することもできます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|説明|トピック|  
|-|-|   
|ジョブの作成と所有権の割り当てについて説明します。|[ジョブの作成](../../ssms/agent/create-jobs.md)|  
|ジョブをカテゴリごとに編成するための情報を記載しています。|[ジョブの整理](../../ssms/agent/organize-jobs.md)|  
|ユーザーが作成できるさまざまな種類のジョブ ステップおよびそれらの管理方法について説明します。|[ジョブ ステップの管理](../../ssms/agent/manage-job-steps.md)|  
|ジョブの実行開始時刻および実行頻度を定義する方法について説明します。|[スケジュールの作成とジョブへのアタッチ](../../ssms/agent/create-and-attach-schedules-to-jobs.md)|  
|(スケジュールを設定せずに) ジョブを手動で実行するための情報を記載しています。|[ジョブの実行](../../ssms/agent/run-jobs.md)|  
|ジョブに応答できるように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを構成する方法について説明します。 たとえば、ジョブが完了したら管理者に通知するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを構成できます。|[ジョブ応答の指定](../../ssms/agent/specify-job-responses.md)|  
|既存のジョブおよびその実行履歴を参照する方法と、既存のジョブを変更する方法について説明します。|[ジョブの表示または変更](../../ssms/agent/view-or-modify-jobs.md)|  
|ジョブを削除する方法について説明します。|[ジョブの削除](../../ssms/agent/delete-jobs.md)|  
  
## <a name="see-also"></a>関連項目  
[SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)  
