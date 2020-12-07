---
description: sp_dropmergepublication (Transact-SQL)
title: sp_dropmergepublication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepublication
- sp_dropmergepublication_TSQL
helpviewer_keywords:
- sp_dropmergepublication
ms.assetid: 9e1cb96e-5889-4f97-88cd-f60cf313ce68
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0c787c7c2503f9182b704e83a04664d7d377cef4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538974"
---
# <a name="sp_dropmergepublication-transact-sql"></a>sp_dropmergepublication (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージパブリケーションとそれに関連付けられたスナップショットエージェントを削除します。 マージ パブリケーションを削除する前に、すべてのサブスクリプションを削除しておく必要があります。 パブリケーション内のアーティクルは自動的に削除されます。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropmergepublication [ @publication= ] 'publication'   
    [ , [ @ignore_distributor = ] ignore_distributor ]   
    [ , [ @reserved = ] reserved ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 削除するパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。 **All**を使用すると、既存のすべてのマージパブリケーションと、それらに関連付けられているスナップショットエージェントジョブが削除されます。 *パブリケーション*に特定の値を指定すると、そのパブリケーションとそれに関連付けられたスナップショットエージェントジョブのみが削除されます。  
  
`[ @ignore_distributor = ] ignore_distributor` ディストリビューターでクリーンアップタスクを実行せずにパブリケーションを削除する場合に使用します。 *ignore_distributor* は **ビット**,、既定値は **0**です。 このパラメーターは、ディストリビューターを再インストールするときにも使用されます。  
  
`[ @reserved = ] reserved` 将来使用するために予約されています。 *予約済み* は **ビット**,、既定値は **0**です。  
  
`[ @ignore_merge_metadata = ] ignore_merge_metadata` 内部でのみ使用します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_dropmergepublication** は、マージレプリケーションで使用します。  
  
 **sp_dropmergepublication** は、パブリケーションに関連付けられているすべてのアーティクルを再帰的に削除してから、パブリケーション自体を削除します。 パブリケーションに1つ以上のサブスクリプションがある場合は、パブリケーションを削除できません。 サブスクリプションを削除する方法の詳細については、「 [delete a Push subscription](../../relational-databases/replication/delete-a-push-subscription.md) 」および「 [Delete a Pull subscription](../../relational-databases/replication/delete-a-pull-subscription.md)」を参照してください。  
  
 パブリケーションを削除するために **sp_dropmergepublication** を実行しても、パブリッシュされたオブジェクトはパブリケーションデータベースから削除されず、対応するオブジェクトはサブスクリプションデータベースから削除されません。 必要に応じて、DROP を使用して \<object> これらのオブジェクトを手動で削除します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_dropmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepublication-_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_dropmergepublication**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [パブリケーションを削除する](../../relational-databases/replication/publish/delete-a-publication.md)   
 [sp_addmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
