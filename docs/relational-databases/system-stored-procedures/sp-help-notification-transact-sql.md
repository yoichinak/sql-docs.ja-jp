---
description: sp_help_notification (Transact-SQL)
title: sp_help_notification (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_notification
- sp_help_notification_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_notification
ms.assetid: 0273457f-9d2a-4a6f-9a16-6a6bf281cba0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cce6fd1c7645857019399dae9934c8b730e14f77
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536155"
---
# <a name="sp_help_notification-transact-sql"></a>sp_help_notification (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたオペレーターのアラートの一覧、または特定のアラートのオペレーターの一覧を報告します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_notification  
     [ @object_type = ] 'object_type' ,  
     [ @name = ] 'name' ,  
     [ @enum_type = ] 'enum_type' ,   
     [ @notification_method = ] notification_method   
     [ , [ @target_name = ] 'target_name' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @object_type = ] 'object_type'` 返される情報の種類。 *object_type*は **char (9)**,、既定値はありません。 *object_type* は、指定されたオペレーター名に割り当てられたアラートを一覧表示するアラート、または指定されたアラート名を担当するオペレーターの*一覧を示す* オペレーターです *。*  
  
`[ @name = ] 'name'` オペレーター名 ( *object_type* が演算子の場合) または警告名 ( *object_type* がアラートの場合)。 *名前* は **sysname**,、既定値はありません。  
  
`[ @enum_type = ] 'enum_type'` 返される *object_type*情報。 ほとんどの場合、 *enum_type*は実際のものです。 *enum_type*は **char (10)** で、既定値はありません。これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|ACTUAL|*名前*に関連付けられている*object_types*のみを一覧表示します。|  
|ALL|*名前*に関連付けられていないものを含むすべての*object_types*を一覧表示します。|  
|TARGET|*名前*との関連付けに関係なく、指定された*target_name*に一致する*object_types*のみを一覧表示します。|  
  
`[ @notification_method = ] notification_method` 返される通知方法の列を決定する数値。 *notification_method* は **tinyint**で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|電子メール: **use_email** 列だけを返します。|  
|**2**|Pager: **use_pager** 列だけを返します。|  
|**4**|NetSend: **use_netsend** 列だけを返します。|  
|**7**|All: すべての列を返します。|  
  
`[ @target_name = ] 'target_name'` 検索するアラートの名前 ( *object_type* が警告の場合) または検索するオペレーター名 ( *object_type* がオペレーターの場合)。 *target_name* は *enum_type* がターゲットの場合にのみ必要です。 *target_name* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-valves"></a>リターンコードバルブ  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 *Object_type*が**警告**の場合、結果セットには特定のオペレーターに対するすべての警告が表示されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|アラートの識別子番号。|  
|**alert_name**|**sysname**|アラート名。|  
|**use_email**|**int**|電子メールはオペレーターに通知するために使用されます。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**use_pager**|**int**|ポケットベルを使用してオペレーターに通知します。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**use_netsend**|**int**|オペレーターへの通知にネットワーク ポップアップを使用するかどうか。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**has_email**|**int**|この警告で送信する電子メール通知の数。|  
|**has_pager**|**int**|このアラートに対して送信されたポケットベル通知の数。|  
|**has_netsend**|**int**|このアラートに対して送信された **net send** 通知の数。|  
  
 **Object_type**が**演算子**の場合、結果セットには特定の警告のすべての演算子が表示されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**operator_id**|**int**|オペレーター識別番号。|  
|**operator_name**|**sysname**|オペレーター名。|  
|**use_email**|**int**|電子メールは、オペレーターの通知を送信するために使用されます。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**use_pager**|**int**|オペレーターへの通知にポケットベルを使用するかどうか。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**use_netsend**|**int**|オペレーターに通知するために使用されるネットワークポップアップです。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**has_email**|**int**|オペレーターが電子メール アドレスを持っているかどうか。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**has_pager**|**int**|オペレーターがポケットベル アドレスを持っているかどうか。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
|**has_netsend**|**int**|オペレーターには、net send 通知が構成されています。<br /><br /> **1** = はい<br /><br /> **0** = いいえ|  
  
## <a name="remarks"></a>解説  
 このストアドプロシージャは、 **msdb** データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャを実行するには、 **sysadmin** 固定サーバー ロールのメンバーであることが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-alerts-for-a-specific-operator"></a>A. 特定のオペレーターに対する警告の一覧表示  
 次の例では、オペレーター `François Ajenstat` が通知を受け取るすべての警告を返します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_notification   
    @object_type = N'ALERTS',  
    @name = N'François Ajenstat',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
### <a name="b-listing-operators-for-a-specific-alert"></a>B. 特定の警告の送信先となるオペレーターを表示する  
 次の例では、警告に対して任意の種類の通知を受け取るすべてのオペレーターを返し `Test Alert` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_notification  
    @object_type = N'OPERATORS',  
    @name = N'Test Alert',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_update_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
