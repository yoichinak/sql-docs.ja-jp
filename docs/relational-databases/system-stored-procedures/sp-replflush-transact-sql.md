---
description: sp_replflush (Transact-sql)
title: sp_replflush (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_replflush
- sp_replflush_TSQL
helpviewer_keywords:
- sp_replflush
ms.assetid: 20809f5f-941d-427f-8f0c-de7a6c487584
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 45a015f0b7b2448c0cf19c147247e1dd09b565b2
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99211902"
---
# <a name="sp_replflush-transact-sql"></a>sp_replflush (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  アーティクルキャッシュをフラッシュします。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
> [!IMPORTANT]  
>  このプロシージャを手動で実行する必要はありません。 **sp_replflush** は、経験豊富なレプリケーションサポート担当者が指示するように、レプリケーションのトラブルシューティングにのみ使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replflush  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replflush** は、トランザクションレプリケーションで使用します。  
  
 効率を上げるため、アーティクル定義がキャッシュに格納されます。 **sp_replflush** は、アーティクル定義が変更または削除されるたびに、他のレプリケーションストアドプロシージャによって使用されます。  
  
 特定のデータベースに対するログリーダーアクセス権を持つことができるのは、1つのクライアント接続のみです。 クライアントがデータベースへのログリーダーアクセス権を持っている場合、 **sp_replflush** を実行すると、クライアントはそのアクセスを解放します。 その他のクライアントは、 **sp_replcmds** または **sp_replshowcmds** を使用して、トランザクションログをスキャンできます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replflush** を実行できるのは、固定サーバーロール **sysadmin** または固定データベースロール **db_owner** のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_repltrans &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
