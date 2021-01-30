---
description: sp_syscollector_delete_collection_item (Transact-SQL)
title: sp_syscollector_delete_collection_item (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_syscollector_delete_collection_item
- sp_syscollector_delete_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_delete_collecton_item
- data collector [SQL Server], stored procedures
ms.assetid: 9c2b0990-1d3d-4a59-94a0-3cca6fef4681
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ae900632edd8ccce0e31c87bd7814c41f02da291
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99204325"
---
# <a name="sp_syscollector_delete_collection_item-transact-sql"></a>sp_syscollector_delete_collection_item (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  コレクションセットからコレクションアイテムを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_delete_collection_item [[ @collection_item_id = ] collection_item_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>引数  
 [ @collection_item_id =] *collection_item_id*  
 コレクション アイテムの一意な識別子を指定します。 *collection_item_id* は **int** で、既定値は NULL です。 *名前* が NULL の場合、 *collection_item_id* には値が必要です。  
  
 [ @name =] '*name*'  
 コレクションアイテムの名前を指定します。 *名前* は **sysname** で、既定値は NULL です。 *collection_item_id* が NULL の場合、*名前* には値を指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_syscollector_delete_collection_item は、msdb システム データベースのコンテキストで実行する必要があります。 コレクションアイテムをシステムコレクションセットから削除することはできません。  
  
 この操作が実行されている間、コレクション アイテムを含むコレクション セットは停止し、再開されます。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、dc_admin (EXECUTE 権限を持つ) 固定データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、という名前のコレクションアイテムを削除し `MyCollectionItem1` ます。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_delete_collection_item @name = 'MyCollectionItem1';  
```  
  
## <a name="see-also"></a>参照  
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_create_collection_item &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
