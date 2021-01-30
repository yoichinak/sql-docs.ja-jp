---
description: sp_replication_agent_checkup (Transact-SQL)
title: sp_replication_agent_checkup (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_replication_agent_checkup_TSQL
- sp_replication_agent_checkup
helpviewer_keywords:
- sp_replication_agent_checkup
ms.assetid: 50357c2e-71aa-4e13-9e2e-0977a3655cc9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 77dd179aa4024f969d8e27a3d57cdc03374a4497
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99204395"
---
# <a name="sp_replication_agent_checkup-transact-sql"></a>sp_replication_agent_checkup (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  各ディストリビューションデータベースで、実行中のレプリケーションエージェントがあるかどうかを確認します。ただし、指定されたハートビート間隔内に履歴が記録されていません。 このストアドプロシージャは、ディストリビューター側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## <a name="arguments"></a>引数  
`[ @heartbeat_interval = ] 'heartbeat_interval'` エージェントが進行状況メッセージをログに記録しなくてもよい最大時間を分単位で指定します。 *heartbeat_interval* は **int**,、既定値は10分です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **sp_replication_agent_checkup** では、問題があると検出された各エージェントに対してエラー14151が発生します。 また、これらのエージェントに関する障害履歴メッセージをログに記録します。  
  
## <a name="remarks"></a>コメント  
 **sp_replication_agent_checkup** は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_replication_agent_checkup** を実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
