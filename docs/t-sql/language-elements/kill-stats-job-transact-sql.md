---
description: KILL STATS JOB (Transact-SQL)
title: KILL STATS JOB (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KILL STATS JOB
- KILL_STATS_JOB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending statistics update jobs [SQL Server]
- stopping statistics update jobs
- terminating statistics update jobs
- asynchronous statistics updates [SQL Server]
- KILL STATS JOB statement
- statistics update jobs [SQL Server]
ms.assetid: 55a8f9f1-3259-45c0-8ab9-60b9c088b4b4
author: rothja
ms.author: jroth
ms.openlocfilehash: a3d76f64539df36751f87cf3a9c3586b138ddbbb
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193359"
---
# <a name="kill-stats-job-transact-sql"></a>KILL STATS JOB (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で統計の非同期更新ジョブを終了します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
KILL STATS JOB job_id   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *job_id*  
 ジョブの sys.dm_exec_background_job_queue 動的管理ビューによって返された job_id フィールドです。  
  
## <a name="remarks"></a>解説  
 job_id は、他の形式の KILL ステートメントで使用されている session_id または作業単位とは無関係です。  
  
## <a name="permissions"></a>アクセス許可  
 sys.dm_exec_background_job_queue 動的管理ビューからの情報にアクセスするには VIEW SERVER STATE 権限が必要です。  
  
 KILL STATS JOB 権限は、特に指定のない限り固定データベース ロール sysadmin および processadmin のメンバーに与えられ、これを譲渡することはできません。  
  
## <a name="examples"></a>例  
 次の例は、*job_id* = `53` のジョブに関連付けられた統計情報の更新を終了する方法を示しています。  
  
```sql  
KILL STATS JOB 53;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)   
 [sys.dm_exec_background_job_queue &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-background-job-queue-transact-sql.md)   
 [統計](../../relational-databases/statistics/statistics.md)  
  
  
