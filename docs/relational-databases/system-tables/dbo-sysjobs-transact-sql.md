---
description: dbo.sysジョブ (Transact-sql)
title: dbo.sysジョブ (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobs
- sysjobs_TSQL
- dbo.sysjobs
- dbo.sysjobs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobs system table
ms.assetid: e244a6a5-54c2-47a6-8039-dd1852b0ae59
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fb1e7125dd953fe4904c963f888ae9c11c400df9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545806"
---
# <a name="dbosysjobs-transact-sql"></a>dbo.sysジョブ (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによる実行が予定されているジョブに関する情報を格納します。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**job_id**|**uniqueidentifier**|ジョブの一意の ID。|  
|**originating_server_id**|**int**|ジョブの送信元のサーバーの ID。|  
|**name**|**sysname**|ジョブの名前。|  
|**有効**|**tinyint**|ジョブの実行が有効かどうかを示します。|  
|**description**|**nvarchar(512)**|ジョブの説明。|  
|**start_step_id**|**int**|実行を開始するジョブのステップの ID。|  
|**category_id**|**int**|ジョブカテゴリの ID。|  
|**owner_sid**|**varbinary(85)**|ジョブ所有者のセキュリティ識別番号 (SID)。|  
|**notify_level_eventlog**|**int**|どのような場合に通知イベントを Microsoft Windows アプリケーションログに記録するかを示す**ビットマスク**。<br /><br /> **0** = なし<br /><br /> **1** = ジョブが成功したとき<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = ジョブが完了するたびに (ジョブの結果に関係なく)|  
|**notify_level_email**|**int**|どのような場合に、ジョブの完了時に通知電子メールを送信するかを示すビットマスク。<br /><br /> **0** = なし<br /><br /> **1** = ジョブが成功したとき<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = ジョブが完了するたびに (ジョブの結果に関係なく)|  
|**notify_level_netsend**|**int**|どのような場合に、ジョブの完了時にネットワークメッセージを送信するかを示すビットマスク。<br /><br /> **0** = なし<br /><br /> **1** = ジョブが成功したとき<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = ジョブが完了するたびに (ジョブの結果に関係なく)|  
|**notify_level_page**|**int**|どのような場合に、ジョブの完了時にポケットベルのメッセージを送信するのかを示すビットマスク。<br /><br /> **0** = なし<br /><br /> **1** = ジョブが成功したとき<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = ジョブが完了するたびに (ジョブの結果に関係なく)|  
|**notify_email_operator_id**|**int**|通知するオペレーターの電子メール名。|  
|**notify_netsend_operator_id**|**int**|ネットワークメッセージを送信するときに使用されるコンピューターまたはユーザーの ID。|  
|**notify_page_operator_id**|**int**|ページの送信時に使用されるコンピューターまたはユーザーの ID。|  
|**delete_level**|**int**|どのような場合に、ジョブの完了時にジョブを削除する必要があるかを示す**ビットマスク**。<br /><br /> **0** = なし<br /><br /> **1** = ジョブが成功したとき<br /><br /> **2** = ジョブが失敗したとき<br /><br /> **3** = ジョブが完了するたびに (ジョブの結果に関係なく)|  
|**date_created**|**datetime**|ジョブが作成された日付。|  
|**date_modified**|**datetime**|ジョブが最後に変更された日付。|  
|**version_number**|**int**|ジョブのバージョン。|  
  
  
