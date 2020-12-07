---
description: '[ジョブのスケジュール選択]'
title: '[ジョブのスケジュール選択]'
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.pickscheduleforjob.f1
helpviewer_keywords:
- Pick Schedule for Job dialog box
ms.assetid: 6de2025d-c25c-47b9-9a25-18c294935c15
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: c095370f69aaa1e9f06cfc3e57500c09442c728a
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92030878"
---
# <a name="pick-schedule-for-job"></a>[ジョブのスケジュール選択]
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の違い](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このダイアログを使用して、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの既存のスケジュールを選択します。  
  
## <a name="options"></a>オプション  
**[利用可能なスケジュール]**  
このジョブで利用可能なスケジュールの一覧を表示します。 ジョブとスケジュールの所有者は同じである必要があるので、この一覧には、このジョブの所有者が所有しているスケジュールだけが表示されます。  
  
**名前**  
スケジュールの名前を表示します。  
  
**Enabled**  
スケジュールが有効な場合に選択されます。  
  
**説明**  
ジョブを実行するスケジュールの条件を説明します。  
  
**[スケジュール済みのジョブ]**  
スケジュールにアタッチされているジョブの番号を表示します。 番号をクリックすると、ジョブのプロパティが表示されます。  
  
**プロパティ**  
**[ジョブ スケジュールのプロパティ]** ダイアログを表示します。このダイアログには、スケジュールに関する情報が表示されます。  
  
## <a name="see-also"></a>参照  
[スケジュールの作成とジョブへのアタッチ](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
