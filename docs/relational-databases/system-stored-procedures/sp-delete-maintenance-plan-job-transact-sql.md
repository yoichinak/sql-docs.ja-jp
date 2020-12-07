---
description: sp_delete_maintenance_plan_job (Transact-SQL)
title: sp_delete_maintenance_plan_job (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_maintenance_plan_job
- sp_delete_maintenance_plan_job_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_maintenance_plan_job
ms.assetid: 1c2148c3-2928-4d9b-b1c8-3512cfbd6a63
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0b06c9c385d85c1b1a4cb4df79ebb22f70d5abee
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536562"
---
# <a name="sp_delete_maintenance_plan_job-transact-sql"></a>sp_delete_maintenance_plan_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたジョブから、指定されたメンテナンスプランの関連付けを解除します。  
  
> [!NOTE]  
>  このストアドプロシージャは、データベースメンテナンスプランで使用されます。 この機能は、このストアドプロシージャを使用しないメンテナンスプランに置き換えられました。 このプロシージャは、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からアップグレードしたプログラムでデータベース メンテナンス プランを管理する場合に使用します。  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_delete_maintenance_plan_job [ @plan_id = ] 'plan_id' ,   
   [ @job_id = ] 'job_id'   
```  
  
## <a name="arguments"></a>引数  
`[ @plan_id = ] 'plan\_id'` メンテナンスプランの ID を指定します。 *plan_id* は **uniqueidentifier**で、有効な id である必要があります。  
  
`[ @job_id = ] 'job\_id'` メンテナンスプランが関連付けられているジョブの ID を指定します。 *job_id* は **uniqueidentifier**で、有効な id である必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_delete_maintenance_plan_job** は、 **msdb** データベースから実行する必要があります。  
  
 すべてのジョブをメンテナンスプランから削除した場合、ユーザーは **sp_delete_maintenance_plan_db** を実行して、プランから残りのデータベースを削除することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_delete_maintenance_plan_job**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 この例では、メンテナンスプランからジョブ "B8FCECB1-E22C-11D2-AA64-00C04F688EAE" を削除します。  
  
```  
EXECUTE   sp_delete_maintenance_plan_job N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC', N'B8FCECB1-E22C-11D2-AA64-00C04F688EAE';  
```  
  
## <a name="see-also"></a>参照  
 [メンテナンス プラン](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [データベースメンテナンスプランのストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
