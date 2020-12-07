---
description: sp_getqueuedrows (Transact-SQL)
title: sp_getqueuedrows (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getqueuedrows_TSQL
- sp_getqueuedrows
helpviewer_keywords:
- sp_getqueuedrows
ms.assetid: 139e834f-1988-4b4d-ac81-db1f89ea90e8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8aae51ed8d3806fb32375ddebd6d09c1c6c37d1f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548035"
---
# <a name="sp_getqueuedrows-transact-sql"></a>sp_getqueuedrows (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  キューで保留中の更新があるサブスクライバーの行を取得します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_getqueuedrows [ @tablename = ] 'tablename'  
    [ , [ @owner = ] 'owner'  
    [ , [ @tranid = ] 'transaction_id' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @tablename = ] 'tablename'` テーブルの名前を指定します。 *tablename* は **sysname**,、既定値はありません。 テーブルは、キューに登録されたサブスクリプションの一部である必要があります。  
  
`[ @owner = ] 'owner'` はサブスクリプションの所有者です。 *owner* は **sysname**,、既定値は NULL です。  
  
`[ @tranid = ] 'transaction_id'` 出力をトランザクション ID でフィルター処理できます。 *transaction_id* は **nvarchar (70)**,、既定値は NULL です。 指定した場合、キューに登録されたコマンドに関連付けられているトランザクション ID が表示されます。 NULL の場合、キュー内のすべてのコマンドが表示されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 サブスクライブされたテーブルに対して1つ以上のキューに登録されたトランザクションを現在保持しているすべての行を表示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**操作**|**nvarchar (10)**|同期を実行するときに行われるアクションの種類。<br /><br /> INS= 挿入<br /><br /> DEL = 削除<br /><br /> UPD = 更新|  
|**Tranid**|**nvarchar (70)**|コマンドが実行されたトランザクション ID。|  
|**table column1...n**||*Tablename*で指定されたテーブルの各列の値。|  
|**msrepl_tran_version**|**uniqueidentifier**|この列は、レプリケートされたデータへの変更を追跡し、パブリッシャーで競合検出を実行するために使用されます。 この列は、自動的にテーブルに追加されます。|  
  
## <a name="remarks"></a>解説  
 **sp_getqueuedrows** は、キュー更新に参加しているサブスクライバーで使用されます。  
  
 **sp_getqueuedrows** は、キュー更新に参加しているサブスクリプションデータベース上の特定のテーブルの行を検索しますが、現在はキューリーダーエージェントによって解決されていません。  
  
## <a name="permissions"></a>アクセス許可  
 **sp_getqueuedrows** には、 *tablename*で指定されたテーブルに対する SELECT 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [キュー更新の競合の検出と解決](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
