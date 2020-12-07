---
description: sp_xtp_unbind_db_resource_pool (Transact-sql)
title: sp_xtp_unbind_db_resource_pool (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xtp_unbind_db_resource_pool_TSQL
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool_TSQL
- sys.sp_xtp_unbind_db_resource_pool
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool
ms.assetid: 695a796d-087e-4bc8-99d0-ddc342604c75
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 27d5d5efd923dfffd66054da48b8baf28b6f193b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551109"
---
# <a name="syssp_xtp_unbind_db_resource_pool-transact-sql"></a>sp_xtp_unbind_db_resource_pool (Transact-sql)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  このシステムプロシージャは、メモリ使用量を追跡するために、データベースとリソースプールの間の既存のバインドを削除し [!INCLUDE[hek_2](../../includes/hek-2-md.md)] ます。  指定したデータベースに現在バインドされたプールがない場合、成功が返されます。 データベースがバインド解除されると、以前に割り当てられたメモリ最適化オブジェクトのメモリは、前のリソースプールに割り当てられたままになります。 割り当てられたメモリを解放するには、データベースを再起動する必要があります。 データベースがリソースプールからバインド解除されると、バインドは既定のリソースプールに並べ替えられます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
sys.sp_xtp_unbind_db_resource_pool 'database_name'  
```  
  
## <a name="arguments"></a>引数  
 database_name  
 既存の [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 有効なデータベースの名前。  
  
#### <a name="parameters"></a>パラメーター  
  
## <a name="messages"></a>メッセージ  
 データベースが名前付きリソースプールにバインドされている場合、プロシージャは正常に返されます。 ただし、バインド解除を有効にするには、データベースを再起動する必要があります。  
 指定したデータベースに既存のバインドが存在しない場合、`sp_xtp_unbind_db_resource_pool` は正常に終了しますが、次のような情報メッセージが表示されます。  
  
```  
Msg 41374, Level 16, State 1, Procedure sp_xtp_unbind_db_resource_pool_internal, Line 140.  
Database 'Hekaton_DB' does not have a binding to a resource pool.  
  
```  
  
## <a name="example"></a>例  
 次のコードは、バインドされた[!INCLUDE[hek_2](../../includes/hek-2-md.md)] リソース プールからデータベース Hekaton_DB をバインド解除します。  Hekaton_DB が[!INCLUDE[hek_2](../../includes/hek-2-md.md)] リソース プールに現在バインドされていない場合、メッセージが表示されます。 バインドの解除を有効にするにはデータベースを再起動する必要があります。  
  
```sql  
sys.sp_xtp_unbind_db_resource_pool 'Hekaton_DB'  
```  
  
## <a name="requirements"></a>要件  
  
-   によって指定されたデータベースには、 `database_name` リソースプールへのバインドが必要 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] です。  
  
-   CONTROL SERVER 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [データベースを作成してリソース プールにバインドする方法については、「](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)  
  
  
