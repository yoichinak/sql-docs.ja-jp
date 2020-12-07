---
description: dbo.sysjobschedules (Transact-sql)
title: dbo.sysjobschedules (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysjobschedules
- dbo.sysjobschedules
- dbo.sysjobschedules_TSQL
- sysjobschedules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysjobschedules system table
ms.assetid: ccdafec7-2a9b-4356-bffb-1caa3a12db59
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2cd3180f982b978a5918b505f9cf0989baf4e0fa
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544594"
---
# <a name="dbosysjobschedules-transact-sql"></a>dbo.sysjobschedules (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  エージェントによって実行されるジョブのスケジュール情報を格納 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 このテーブルは、 **msdb** データベースに格納されます。  
  
> **注:****Sysjobschedules**テーブルは20分ごとに更新され、 **sp_help_jobschedule**ストアドプロシージャによって返される値に影響を与える可能性があります。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|スケジュールの ID。|  
|**job_id**|**uniqueidentifier**|ジョブの ID。|  
|**next_run_date**|**int**|ジョブの次回の実行予定日。 日付の形式は YYYYMMDD です。|  
|**next_run_time**|**int**|ジョブの実行がスケジュールされている時刻。 時刻は HHMMSS 形式で、24時間制を使用します。|  
  
## <a name="see-also"></a>参照  
 [dbo.sysのスケジュール &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
