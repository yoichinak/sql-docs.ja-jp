---
description: sp_restoremergeidentityrange (Transact-sql)
title: sp_restoremergeidentityrange (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_restoremergeidentityrange_TSQL
- sp_restoremergeidentityrange
helpviewer_keywords:
- sp_restoremergeidentityrange
ms.assetid: 7923e422-2748-40c0-b5a8-6410c48d5b70
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2886b4b93331ed59f1943b5625ee673df64b537d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99205106"
---
# <a name="sp_restoremergeidentityrange-transact-sql"></a>sp_restoremergeidentityrange (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このストアドプロシージャは、id 範囲の割り当てを更新するために使用されます。 このストアド プロシージャを使用すると、パブリッシャーがバックアップから復元された後に自動 ID 範囲の管理が正しく機能します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_restoremergeidentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値は **all** です。 指定した場合、そのパブリケーションの id 範囲のみが復元されます。  
  
`[ @article = ] 'article'` アーティクルの名前を指定します。 *アーティクル* は **sysname** で、既定値は **all** です。 指定した場合、そのアーティクルの id 範囲のみが復元されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_restoremergeidentityrange** は、マージレプリケーションで使用します。  
  
 **sp_restoremergeidentityrange** は、ディストリビューターから最大 id 範囲割り当て情報を取得し、自動 id 範囲管理を使用するアーティクルの [MSmerge_identity_range_allocations &#40;transact-sql&#41;](../../relational-databases/system-tables/msmerge-identity-range-allocations-transact-sql.md)の **max_used** 列の値を更新します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_restoremergeidentityrange** を実行できるのは、固定サーバーロール **sysadmin** または固定データベースロール **db_owner** のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_addmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [ID 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  
