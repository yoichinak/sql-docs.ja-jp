---
description: sp_replsetoriginator (Transact-SQL)
title: sp_replsetoriginator (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_replsetoriginator
- sp_replsetoriginator_TSQL
helpviewer_keywords:
- sp_replsetoriginator
ms.assetid: 030e5226-0585-439f-b8cd-36f48367d86d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c26248551ad949bcf27433d28898ba4ec98dc68b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99211633"
---
# <a name="sp_replsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  双方向のトランザクション レプリケーションでのループバックの検出および処理を開始するために使用されます。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>引数  
`[ @server_name = ] 'server_name'` トランザクションが適用されるサーバーの名前を指定します。 *originating_server* は **sysname** であり、既定値はありません。  
  
`[ @database_name = ] 'database_name'` トランザクションが適用されるデータベースの名前を指定します。 *originating_db* は **sysname** であり、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_replsetoriginator** は、レプリケーションによって適用されたトランザクションのソースを記録するためにディストリビューションエージェントによって実行されます。 この情報は、ループバック プロパティ セットを持つ双方向のトランザクション サブスクリプションに対するループバックの検出を開始するために使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replsetoriginator** を実行できるのは、パブリッシャー側の **sysadmin** 固定サーバーロールのメンバー、パブリケーションデータベースの固定データベースロール **db_owner** のメンバー、またはパブリケーションアクセスリスト (PAL) のユーザーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
