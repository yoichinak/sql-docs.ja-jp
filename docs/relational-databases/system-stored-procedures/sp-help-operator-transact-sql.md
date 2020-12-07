---
description: sp_help_operator (Transact-sql)
title: sp_help_operator (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_operator
- sp_help_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_operator
ms.assetid: caedc43d-44b8-415a-897e-92923f6de3b8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2cbf7c84c22998b5ee7e43fadad6a42cf02d17b8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535385"
---
# <a name="sp_help_operator-transact-sql"></a>sp_help_operator (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバーに対して定義されているオペレーターに関する情報をレポートします。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_operator  
     { [ @operator_name = ] 'operator_name'   
     | [ @operator_id = ] operator_id }  
```  
  
## <a name="arguments"></a>引数  
`[ @operator_name = ] 'operator_name'` 演算子名。 *operator_name* は **sysname**です。 *Operator_name*が指定されていない場合は、すべての演算子に関する情報が返されます。  
  
`[ @operator_id = ] operator_id` 情報を要求するオペレーターの識別番号を指定します。 *operator_id*は **int**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Operator_id*または*operator_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|オペレーター識別番号。|  
|**name**|**sysname**|オペレーター名。|  
|**有効**|**tinyint**|オペレーターが通知を受け取ることが可能かどうか。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**email_address**|**nvarchar (100)**|オペレーターの電子メールアドレス。|  
|**last_email_date**|**int**|オペレーターが最後に電子メールで通知した日付。|  
|**last_email_time**|**int**|オペレーターが最後に電子メールで通知した時刻。|  
|**pager_address**|**nvarchar (100)**|オペレーターのポケットベルアドレス。|  
|**last_pager_date**|**int**|オペレーターが前回、ポケットベルによる通知を受け取った日付。|  
|**last_pager_time**|**int**|オペレーターが最後にポケットベルによる通知を行った時刻。|  
|**weekday_pager_start_time**|**int**|平日にオペレーターがポケットベルによる通知を受け取ることのできる開始時刻。|  
|**weekday_pager_end_time**|**int**|オペレーターが平日にポケットベルによる通知を受け取ることができる期間の終了。|  
|**saturday_pager_start_time**|**int**|土曜日にオペレーターがポケットベルによる通知を受け取ることができる期間の開始時刻です。|  
|**saturday_pager_end_time**|**int**|土曜日にオペレーターがポケットベルによる通知を受け取ることのできる最終時刻。|  
|**sunday_pager_start_time**|**int**|日曜日にオペレーターがポケットベルによる通知を受け取ることのできる開始時刻。|  
|**sunday_pager_end_time**|**int**|日曜日にオペレーターがポケットベルによる通知を受け取ることのできる最終時刻。|  
|**pager_days**|**tinyint**|オペレーターがポケットベルによる通知を受け取ることができるかどうかを示すビットマスク (**1** = 日曜日、 **64** = 土曜日)。|  
|**netsend_address**|**nvarchar (100)**|ネットワークポップアップ通知のオペレーターアドレス。|  
|**last_netsend_date**|**int**|オペレーターが最後にネットワークポップアップによる通知を受け取った日付。|  
|**last_netsend_time**|**int**|オペレーターが前回、ネットワーク ポップアップによる通知を受け取った時刻。|  
|**category_name**|**sysname**|このオペレーターが所属するオペレーター カテゴリの名前。|  
  
## <a name="remarks"></a>解説  
 **sp_help_operator** は、 **msdb** データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、オペレーター `François Ajenstat` についての情報をレポートします。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_operator  
    @operator_name = N'François Ajenstat' ;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_add_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
