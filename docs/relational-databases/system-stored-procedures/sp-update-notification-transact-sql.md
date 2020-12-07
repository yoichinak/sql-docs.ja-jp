---
description: sp_update_notification (Transact-sql)
title: sp_update_notification (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_notification_TSQL
- sp_update_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatenotification
ms.assetid: 3e1c3d40-8c24-46ce-a68e-ce6c6a237fda
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 103e697c8aad38fa19769358372b31d89d3b5978
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549542"
---
# <a name="sp_update_notification-transact-sql"></a>sp_update_notification (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  警告通知の通知方法を更新します。  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_update_notification  
          [@alert_name =] 'alert' ,  
     [@operator_name =] 'operator' ,  
     [@notification_method =] notification  
```  
  
## <a name="arguments"></a>引数  
`[ @alert_name = ] 'alert'` この通知に関連付けられている警告の名前。 *alert* は **sysname**で、既定値はありません。  
  
`[ @operator_name = ] 'operator'` アラートが発生したときに通知を受けるオペレーター。 *operator* は **sysname**,、既定値はありません。  
  
`[ @notification_method = ] notification` オペレーターに通知する方法。 *通知*は **tinyint**,、既定値はありませんが、これらの値の1つ以上を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|電子メール|  
|**2**|ポケットベル|  
|**4**|**net send**|  
|**7**|すべてのメソッド|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_update_notification** は、 **msdb** データベースから実行する必要があります。  
  
 指定された *notification_method*を使用して、必要なアドレス情報を持たないオペレーターの通知を更新できます。 電子メールメッセージまたはポケットベルによる通知の送信時にエラーが発生した場合は、Microsoft SQL Server エージェントのエラーログにエラーが報告されます。  
  
## <a name="permissions"></a>アクセス許可  
 このストアドプロシージャを実行するには、 **sysadmin** 固定サーバーロールがユーザーに付与されている必要があります。  
  
## <a name="examples"></a>例  
 次の例では、アラートのに送信される通知の通知方法を変更し `François Ajenstat` `Test Alert` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_notification  
   @alert_name = N'Test Alert',  
   @operator_name = N'François Ajenstat',  
   @notification_method = 7;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
