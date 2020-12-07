---
description: sp_droppullsubscription (Transact-sql)
title: sp_droppullsubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droppullsubscription
- sp_droppullsubscription_TSQL
helpviewer_keywords:
- sp_droppullsubscription
ms.assetid: 7352d94a-f8f2-42ea-aaf1-d08c3b5a0e76
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e4e7e0f9292d9ed94139b9facfe496821b91fb03
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543446"
---
# <a name="sp_droppullsubscription-transact-sql"></a>sp_droppullsubscription (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  サブスクライバーの現在のデータベースでサブスクリプションを削除します。 このストアド プロシージャは、サブスクライバー側でプル サブスクリプション データベースについて実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_droppullsubscription [ @publisher= ] 'publisher'  
        , [ @publisher_db= ] 'publisher_db'  
        , [ @publication= ] 'publication'  
    [ , [ @reserved= ] reserved ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` リモートサーバー名を指定します。 *publisher* は **sysname**で、既定値はありません。 **All**の場合、サブスクリプションはすべてのパブリッシャーで削除されます。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャーデータベースの名前を指定します。 *publisher_db* は **sysname**であり、既定値はありません。 **all** はすべてのパブリッシャーデータベースを意味します。  
  
`[ @publication = ] 'publication'` パブリケーション名を指定します。 *publication* は **sysname**,、既定値はありません。 **All**の場合、すべてのパブリケーションに対してサブスクリプションが削除されます。  
  
`[ @reserved = ] reserved` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_droppullsubscription** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 **sp_droppullsubscription** によって、 [MSreplication_subscriptions &#40;transact-sql&#41;](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) テーブルの対応する行と、サブスクライバー側の対応するディストリビューターエージェントが削除されます。 [Transact-sql&#41;&#40;MSreplication_subscriptions](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md)に行が残されていない場合は、テーブルが削除されます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_droptranpullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-droppullsubscription-_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_droppullsubscription**を実行できるのは、 **sysadmin**固定サーバーロールのメンバー、またはプルサブスクリプションを作成したユーザーだけです。 **Db_owner**固定データベースロールは、プルサブスクリプションを作成したユーザーがこのロールに属している場合にのみ**sp_droppullsubscription**を実行できます。  
  
## <a name="see-also"></a>参照  
 [プルサブスクリプションの削除](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addpullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_change_subscription_properties &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
