---
description: ジョブのプロパティ - [新しいジョブ] ([全般] ページ)
title: ジョブのプロパティ - [新しいジョブ] ([全般] ページ)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.general.f1
ms.assetid: b6832840-1c18-4db8-94fc-080db880ae9f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9da8480712a40612b4078af57864dffdec561c4b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037921"
---
# <a name="job-properties---new-job-general-page"></a>ジョブのプロパティ - [新しいジョブ] ([全般] ページ)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

このページを使用すると、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの全般プロパティを表示および変更できます。  
  
## <a name="options"></a>オプション  
**名前**  
ジョブの名前を変更します。  
  
**所有者**  
ジョブの所有者を選択します。  
  
**カテゴリ**  
ジョブのカテゴリを選択します。  
  
**...**  
選択したカテゴリのジョブを表示します。  
  
**説明**  
ジョブの説明を変更します。  
  
**Enabled**  
ジョブを有効にします。 ジョブが有効ではない場合、スケジュールや警告に応じてジョブが実行されることはありませんが、 **sp_start_job** ストアド プロシージャを使用して引き続きジョブを開始することができます。  
  
**ソース**  
ジョブのマスター サーバーを表示します。 **[ジョブのプロパティ] の [全般]** ページでのみ表示されます。  
  
**Created**  
ジョブが作成された日時を表示します。 **[ジョブのプロパティ] の [全般]** ページでのみ表示されます。  
  
**[最終更新]**  
ジョブが最後に変更された日時を表示します。 **[ジョブのプロパティ] の [全般]** ページでのみ表示されます。  
  
**[最終実行]**  
ジョブの最後の実行の開始日時を表示します。 **[ジョブのプロパティ] の [全般]** ページでのみ表示されます。  
  
**[ジョブ履歴の表示]**  
ジョブ履歴を表示します。 **[ジョブのプロパティ] の [全般]** ページでのみ表示されます。  
  
## <a name="see-also"></a>参照  
[ジョブの実装](../../ssms/agent/implement-jobs.md)  
[[ジョブ カテゴリ] - [ジョブ カテゴリの管理]](../../ssms/agent/job-categories-manage-job-categories.md)  
