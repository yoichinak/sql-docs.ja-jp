---
description: dbo.sysjobschedules (Transact-sql)
title: dbo.sysjobschedules (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
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
author: cawrites
ms.author: chadam
ms.openlocfilehash: f82fae854a00e73ec7d8d45304ee486e0df33373
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99160000"
---
# <a name="dbosysjobschedules-transact-sql"></a>dbo.sysjobschedules (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  エージェントによって実行されるジョブのスケジュール情報を格納 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 このテーブルは、 **msdb** データベースに格納されます。  
  
> **注:****Sysjobschedules** テーブルは20分ごとに更新され、 **sp_help_jobschedule** ストアドプロシージャによって返される値に影響を与える可能性があります。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|スケジュールの ID。|  
|**job_id**|**uniqueidentifier**|ジョブの ID。|  
|**next_run_date**|**int**|ジョブの次回の実行予定日。 日付の形式は YYYYMMDD です。|  
|**next_run_time**|**int**|ジョブの実行がスケジュールされている時刻。 時刻は HHMMSS 形式で、24時間制を使用します。|  
  
## <a name="see-also"></a>参照  
 [dbo.sysのスケジュール &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
