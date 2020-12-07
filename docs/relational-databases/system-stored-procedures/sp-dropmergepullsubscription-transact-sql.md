---
description: sp_dropmergepullsubscription (Transact-sql)
title: sp_dropmergepullsubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergepullsubscription
- sp_dropmergepullsubscription_TSQL
helpviewer_keywords:
- sp_dropmergepullsubscription
ms.assetid: 9301dd80-72f7-4adb-9b13-87e7f9114248
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 20f8fb9eea5be15a3957c9ca430b81cf52a89709
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538955"
---
# <a name="sp_dropmergepullsubscription-transact-sql"></a>sp_dropmergepullsubscription (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージ プル サブスクリプションを削除します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropmergepullsubscription [ @publication= ] 'publication'   
        , [ @publisher= ] 'publisher'   
        , [ @publisher_db= ] 'publisher_db'   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値は NULL です。 このパラメーターは必須です。 すべてのパブリケーションに対するサブスクリプションを削除するには、 **all** の値を指定します  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher*は **sysname**で、既定値は NULL です。 このパラメーターは必須です。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャーデータベースの名前を指定します。 *publisher_db*は **sysname**,、既定値は NULL です。 このパラメーターは必須です。  
  
`[ @reserved = ] 'reserved'` 将来使用するために予約されています。 *予約済み* は **ビット**,、既定値は **0**です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_dropmergepullsubscription** は、マージレプリケーションで使用します。  
  
 このマージプルサブスクリプションのマージエージェントは**sp_dropmergepullsubscription**によって削除されますが、 **sp_addmergepullsubscription**にマージエージェントは作成されません。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_dropmergepullsubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropmergepullsubscrip_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_dropmergepullsubscription**を実行できるのは、 **sysadmin**固定サーバーロールのメンバー、またはマージプルサブスクリプションを作成したユーザーだけです。 **Db_owner**固定データベースロールは、マージプルサブスクリプションを作成したユーザーがこのロールに属している場合にのみ**sp_dropmergepullsubscription**を実行できます。  
  
## <a name="see-also"></a>参照  
 [プルサブスクリプションの削除](../../relational-databases/replication/delete-a-pull-subscription.md)   
 [sp_addmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)  
  
  
