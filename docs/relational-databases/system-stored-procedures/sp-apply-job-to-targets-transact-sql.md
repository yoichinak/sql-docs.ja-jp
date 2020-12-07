---
description: sp_apply_job_to_targets (Transact-sql)
title: sp_apply_job_to_targets (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_apply_job_to_targets
- sp_apply_job_to_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_apply_job_to_targets
ms.assetid: 4a3e9173-7e3c-4100-a9ac-2f5d2c60a8b0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a164569a5a62e24dabe0d47839eaa084b32e2efa
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89528989"
---
# <a name="sp_apply_job_to_targets-transact-sql"></a>sp_apply_job_to_targets (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  1つ以上の対象サーバー、または1つ以上の対象サーバーグループに属している対象サーバーにジョブを適用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_apply_job_to_targets { [ @job_id = ] job_id | [ @job_name = ] 'job_name' }  
     [ , [ @target_server_groups = ] 'target_server_groups' ]   
     [ , [ @target_servers = ] 'target_servers' ]   
     [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` 指定した対象サーバーまたは対象サーバーグループに適用するジョブのジョブ識別番号を指定します。 *job_id* は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` 指定した対象サーバーまたは対象サーバーグループに適用するジョブの名前。 *job_name* は **sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @target_server_groups = ] 'target_server_groups'` 指定されたジョブを適用する対象サーバーグループのコンマ区切りのリスト。 *target_server_groups* は **nvarchar (2048)**,、既定値は NULL です。  
  
`[ @target_servers = ] 'target_servers'` 指定されたジョブを適用する対象サーバーのコンマ区切りのリスト。 *target_servers*は **nvarchar (2048)**,、既定値は NULL です。  
  
`[ @operation = ] 'operation'` 指定したジョブを、指定した対象サーバーまたは対象サーバーグループに適用するか、または削除するかを指定します。 *操作*は **varchar (7)**,、既定値は APPLY です。 有効な操作は **APPLY** と **REMOVE**です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_apply_job_to_targets** を使用すると、複数の対象サーバーからジョブを簡単に適用 (または削除) できます。また、必要な対象サーバーごとに1回 **sp_add_jobserver** (または **sp_delete_jobserver**) を呼び出すこともできます。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 次の例では、以前に作成した `Backup Customer Information` ジョブを、グループ内のすべての対象サーバーに適用し `Servers Maintaining Customer Information` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_apply_job_to_targets  
    @job_name = N'Backup Customer Information',  
    @target_server_groups = N'Servers Maintaining Customer Information',   
    @operation = N'APPLY' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_remove_job_from_targets &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-remove-job-from-targets-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
