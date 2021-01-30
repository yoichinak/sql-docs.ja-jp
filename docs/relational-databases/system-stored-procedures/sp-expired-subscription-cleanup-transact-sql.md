---
description: sp_expired_subscription_cleanup (Transact-SQL)
title: sp_expired_subscription_cleanup (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_expired_subscription_cleanup
- SP_EXPIRED_SUBSCRIPTION_CLEANUP_TSQL
helpviewer_keywords:
- sp_expired_subscription_cleanup
ms.assetid: 6abc29fe-d77a-4673-9d99-ae31c688012c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1c555f2aaabf3e245261a07cc0bc7257e2601926
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99187970"
---
# <a name="sp_expired_subscription_cleanup-transact-sql"></a>sp_expired_subscription_cleanup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  すべてのパブリケーションのすべてのサブスクリプションの状態を確認し、有効期限が切れたサブスクリプションを削除します。 このストアドプロシージャは、パブリッシャー側で任意のデータベースに対して実行されるか、ディストリビューター側で、以外のパブリッシャーのディストリビューションデータベースに対して実行され [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_expired_subscription_cleanup [ [ @publisher = ] 'publisher' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーの名前を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publication* は **sysname**,、既定値は NULL です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パブリッシャーの場合はこのパラメーターを指定しないでください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_expired_subscription_cleanup** は、すべての種類のレプリケーションで使用されます。  
  
 有効期限が切れたサブスクリプションのクリーンアップジョブによって実行される **sp_expired_subscription_cleanup** は、24時間ごとにパブリケーションデータベースから期限切れのサブスクリプションを検出して削除します。 保有期間内にパブリッシャーと同期されていないサブスクリプションがある場合、パブリケーションは期限切れとして宣言され、サブスクリプションのトレースがパブリッシャーでクリーンアップされます。 詳細については、「 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_expired_subscription_cleanup** を実行できるのは、固定サーバーロール **sysadmin** または固定データベースロール **db_owner** のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_mergesubscription_cleanup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
