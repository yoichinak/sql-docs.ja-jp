---
description: sp_post_msx_operation (Transact-sql)
title: sp_post_msx_operation (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_post_msx_operation
- sp_post_msx_operation_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_post_msx_operation
ms.assetid: 085deef8-2709-4da9-bb97-9ab32effdacf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 304eef1c0e707ecb77fb8d13d5e2b524eb9e9e00
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546003"
---
# <a name="sp_post_msx_operation-transact-sql"></a>sp_post_msx_operation (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  対象サーバーをダウンロードして実行するための操作 (行) を **sysdownloadlist** システムテーブルに挿入します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_post_msx_operation  
     [ @operation = ] 'operation'  
     [ , [ @object_type = ] 'object' ]   
     { , [ @job_id = ] job_id }   
     [ , [ @specific_target_server = ] 'target_server' ]   
     [ , [ @value = ] value ]  
     [ , [ @schedule_uid = ] schedule_uid ]  
```  
  
## <a name="arguments"></a>引数  
`[ @operation = ] 'operation'` ポストされた操作の操作の種類。 *操作*は **varchar (64)**,、既定値はありません。 有効な操作は *object_type*によって異なります。  
  
|オブジェクトの種類|Operation|  
|-----------------|---------------|  
|**補足**|INSERT<br /><br /> UPDATE<br /><br /> DELETE<br /><br /> スタート<br /><br /> STOP|  
|**SERVER**|再参加<br /><br /> DEFECT<br /><br /> SYNC-TIME<br /><br /> SET-POLL|  
|**予定**|INSERT<br /><br /> UPDATE<br /><br /> DELETE|  
  
`[ @object_type = ] 'object'` 操作をポストする対象のオブジェクトの型。 有効な種類は、 **JOB**、 **SERVER**、 **SCHEDULE**です。 *オブジェクト* は **varchar (64)**,、既定値は **JOB**です。  
  
`[ @job_id = ] job_id` 操作が適用されるジョブのジョブ識別番号を指定します。 *job_id* は **uniqueidentifier**,、既定値はありません。 **0x00** は、すべてのジョブを示します。 *オブジェクト*が**SERVER**の場合、 *job_id*は必要ありません。  
  
`[ @specific_target_server = ] 'target_server'` 指定された操作を適用する対象サーバーの名前。 *Job_id*が指定されていても*target_server*が指定されていない場合、操作はジョブのすべてのジョブサーバーに対して通知されます。 *target_server* は **nvarchar (30)**,、既定値は NULL です。  
  
`[ @value = ] value` ポーリング間隔 (秒単位)。 *value* のデータ型は **int**で、既定値は NULL です。 このパラメーターは、 *操作* が " **設定-ポーリング**" の場合にのみ指定します。  
  
`[ @schedule_uid = ] schedule_uid` 操作が適用されるスケジュールの一意の識別子。 *schedule_uid* は **uniqueidentifier**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **sp_post_msx_operation** は、 **msdb** データベースから実行する必要があります。  
  
 **sp_post_msx_operation** は、現在のサーバーがマルチサーバー Microsoft SQL Server エージェントであるかどうかを最初に確認し、存在する場合は、 *オブジェクト*がマルチサーバージョブであるかどうかを判断するため、常に安全に呼び出すことができます。  
  
 操作が投稿されると、 **sysdownloadlist** テーブルに表示されます。 ジョブが作成および投稿された後、そのジョブに対するその後の変更は、対象サーバー (TSX) にも伝達される必要があります。 これは、ダウンロードリストを使用して行うこともできます。  
  
 ダウンロードの一覧は、SQL Server Management Studio を使用して管理することを強くお勧めします。 詳細については、「 [ジョブの表示または変更](../../ssms/agent/view-or-modify-jobs.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 このストアドプロシージャを実行するには、 **sysadmin** 固定サーバーロールがユーザーに付与されている必要があります。  
  
## <a name="see-also"></a>参照  
 [sp_add_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)   
 [sp_delete_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [sp_delete_jobserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_resync_targetserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)   
 [sp_start_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-start-job-transact-sql.md)   
 [sp_stop_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-stop-job-transact-sql.md)   
 [sp_update_job &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md)   
 [sp_update_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
