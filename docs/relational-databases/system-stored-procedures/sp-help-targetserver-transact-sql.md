---
description: sp_help_targetserver (Transact-SQL)
title: sp_help_targetserver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_targetserver_TSQL
- sp_help_targetserver
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_targetserver
ms.assetid: f841d3bd-901a-4980-ad0b-1c6eeba3f717
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 02304ff4c41f45e90c24fb4be1a815be49c1336a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89527562"
---
# <a name="sp_help_targetserver-transact-sql"></a>sp_help_targetserver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  すべての対象サーバーを一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_targetserver   
     [ [ @server_name = ] 'server_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @server_name = ] 'server_name'` 情報を返すサーバーの名前。 *server_name* は **nvarchar (30)**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 *Server_name*が指定されていない場合、 **sp_help_targetserver**はこの結果セットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|サーバーの識別番号。|  
|**server_name**|**nvarchar(30)**|サーバー名。|  
|**location**|**nvarchar(200)**|指定されたサーバーの場所です。|  
|**time_zone_adjustment**|**int**|グリニッジ標準時 (GMT) からのタイムゾーンの調整 (時間単位)。|  
|**enlist_date**|**datetime**|指定したサーバーの参加日。|  
|**last_poll_date**|**datetime**|ジョブに対してサーバーが最後にポーリングされた日付。|  
|**status**|**int**|指定されたサーバーの状態。|  
|**unread_instructions**|**int**|サーバーに未読の指示があるかどうか。 すべての行がダウンロードされている場合、この列は **0**になります。|  
|**local_time**|**datetime**|対象サーバーのローカルの日付と時刻。これは、マスターサーバーの最後のポーリング時点での対象サーバーのローカル時刻に基づいています。|  
|**enlisted_by_nt_user**|**nvarchar (100)**|ターゲット サーバーに参加した Microsoft Windows のユーザー。|  
|**poll_interval**|**int**|ジョブをダウンロードしてジョブの状態をアップロードするために、対象サーバーがマスター SQLServerAgent サービスをポーリングする間隔 (秒単位)。|  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャを実行するには、 **sysadmin** 固定サーバー ロールのメンバーであることが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-information-for-all-registered-target-servers"></a>A. 登録されているすべての対象サーバーの情報を一覧表示する  
 次の例では、すべての登録されたターゲット サーバーの情報を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-target-server"></a>B. 特定の対象サーバーの情報を一覧表示する  
 次の例では、対象サーバーの情報を一覧表示し `SEATTLE2` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_targetserver N'SEATTLE2' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_targetservergroup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_delete_targetserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetserver-transact-sql.md)   
 [sp_delete_targetservergroup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_update_targetservergroup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)   
 [dbo.sysdownloadlist &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysdownloadlist-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
