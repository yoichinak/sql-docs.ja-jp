---
description: sp_dropanonymousagent (Transact-sql)
title: sp_dropanonymousagent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropanonymousagent
- sp_dropanonymousagent_TSQL
helpviewer_keywords:
- sp_dropanonymousagent
ms.assetid: 4cb96efa-9358-44a3-a8ee-a7e181bed089
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: d6e687976dab6d526a2413260d2ad2f980001086
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474282"
---
# <a name="sp_dropanonymousagent-transact-sql"></a>sp_dropanonymousagent (Transact-sql)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ディストリビューター側のレプリケーション監視用の匿名エージェントをパブリッシャーから削除します。 このストアドプロシージャは、パブリッシャー側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_dropanonymousagent [ @subid= ] sub_id    , [ @type= ] type  
```  
  
## <a name="arguments"></a>引数  
`[ @subid = ] sub_id` 匿名サブスクリプションのグローバル識別子を示します。 *sub_id* は **uniqueidentifier**,、既定値はありません。 この識別子は **sp_helppullsubscription**を使用してサブスクライバーで取得できます。 返された結果セットの **subid** フィールドの値は、このグローバル識別子です。  
  
`[ @type = ] type` サブスクリプションの種類を示します。 *型* は **int**,、既定値はありません。 有効な値は **1** または **2**です。 スナップショットレプリケーションまたはディストリビューションエージェントを使用したトランザクションレプリケーションの場合は、 **1**を指定します。 マージエージェントを使用したマージレプリケーションの場合は、 **2**を指定します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_dropanonymousagent** は、すべての種類のレプリケーションで使用されます。  
  
 このストアドプロシージャは、匿名サブスクリプションエージェントのみを削除するために使用され、既知のサブスクリプションを削除するためには使用できません。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_dropanonymousagent**を実行できるのは、ディストリビューションデータベースの**db_owner**固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
