---
title: sp_dropsubscription (Transact-sql) |Microsoft Docs
description: パブリッシャーのアーティクル、パブリケーション、またはサブスクリプションに対するサブスクリプションを削除します。 このストアドプロシージャは、パブリッシャー側のパブリケーションデータベースで実行されます。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropsubscription
- sp_dropsubscription_TSQL
helpviewer_keywords:
- sp_dropsubscription
ms.assetid: 7551f345-5510-4684-ab53-f9057249d13a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c8c13030b1232a01aac14ac936323c05c540ab1f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536570"
---
# <a name="sp_dropsubscription-transact-sql"></a>sp_dropsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  パブリッシャー上の特定のアーティクル、パブリケーション、またはサブスクリプションの集合へのサブスクリプションを削除します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
        , [ @subscriber= ] 'subscriber'  
    [ , [ @destination_db= ] 'destination_db' ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 関連付けられているパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値は NULL です。 **All**の場合、指定されたサブスクライバーのすべてのパブリケーションのすべてのサブスクリプションが取り消されます。 *publication* は必須パラメーターです。  
  
`[ @article = ] 'article'` アーティクルの名前を指定します。 *アーティクル* は **sysname**で、既定値は NULL です。 **All**を指定すると、指定された各パブリケーションおよびサブスクライバーのすべてのアーティクルに対するサブスクリプションが削除されます。 即時更新が可能なパブリケーションの場合は、 **all** を使用します。  
  
`[ @subscriber = ] 'subscriber'` サブスクリプションを削除するサブスクライバーの名前を指定します。 *サブスクライバー* は **sysname**,、既定値はありません。 **All**を使用すると、すべてのサブスクライバーのすべてのサブスクリプションが削除されます。  
  
`[ @destination_db = ] 'destination_db'` 転送先データベースの名前を指定します。 *destination_db* は **sysname**,、既定値は NULL です。 NULL の場合、そのサブスクライバーからのすべてのサブスクリプションが削除されます。  
  
`[ @ignore_distributor = ] ignore_distributor`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @reserved = ] 'reserved'`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_dropsubscription** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 即時同期パブリケーションのアーティクルに対してサブスクリプションを削除した場合、パブリケーションのすべてのアーティクルに対してサブスクリプションを削除して一度に追加しない限り、サブスクリプションを追加し直すことはできません。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropsubscription-tran_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールのメンバー、 **db_owner**固定データベースロールのメンバー、またはサブスクリプションを作成したユーザーだけが**sp_dropsubscription**を実行できます。  
  
## <a name="see-also"></a>参照  
 [プッシュサブスクリプションを削除する](../../relational-databases/replication/delete-a-push-subscription.md)   
 [sp_addsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
