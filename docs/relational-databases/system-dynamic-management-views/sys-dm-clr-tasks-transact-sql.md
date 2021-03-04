---
description: sys.dm_clr_tasks (Transact-SQL)
title: sys.dm_clr_tasks (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.dm_clr_tasks
- sys.dm_clr_tasks_TSQL
- dm_clr_tasks
- dm_clr_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_tasks dynamic management view
ms.assetid: 462b9061-09fa-4858-9707-03d6cc19c769
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c16eea33c1c0211b37823ecff1e2ae1131d2a335
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101837619"
---
# <a name="sysdm_clr_tasks-transact-sql"></a>sys.dm_clr_tasks (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在実行中のすべての共通言語ランタイム (CLR) タスクの行を返します。 [!INCLUDE[tsql](../../includes/tsql-md.md)]CLR ルーチンへの参照を含むバッチは、そのバッチ内のすべてのマネージコードを実行するための個別のタスクを作成します。 バッチ内に、マネージド コードの実行を必要とするステートメントが複数ある場合は、それらのステートメントで同じ CLR タスクが使用されます。 CLR タスクは、マネージコードの実行に関連するオブジェクトと状態を維持すると共に、のインスタンスと共通言語ランタイムの間の遷移を保持し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary (8)**|CLR タスクのアドレス。|  
|**sos_task_address**|**varbinary (8)**|基になる [!INCLUDE[tsql](../../includes/tsql-md.md)] batch タスクのアドレス。|  
|**appdomain_address**|**varbinary (8)**|このタスクが実行されているアプリケーションドメインのアドレス。|  
|**状態**|**nvarchar(128)**|タスクの現在の状態。|  
|**abort_state**|**nvarchar(128)**|中止の現在の状態 (タスクが取り消された場合)。タスクの中止中に複数の状態が関係しています。|  
|**type**|**nvarchar(128)**|タスクの種類。|  
|**affinity_count**|**int**|タスクの関係。|  
|**forced_yield_count**|**int**|タスクが強制的に生成された回数。|  
  
## <a name="permissions"></a>アクセス許可  

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
SQL Database Basic、S0、S1 のサービス目標、およびエラスティックプール内のデータベースについては、 [サーバー管理者](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) アカウントまたは [Azure Active Directory 管理者](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) アカウントが必要です。 その他のすべての SQL Database サービスの目的で `VIEW DATABASE STATE` は、データベースで権限が必要になります。   
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Transact-sql&#41;&#40;共通言語ランタイム関連の動的管理ビュー ](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
