---
description: DROP QUEUE (Transact-SQL)
title: DROP QUEUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP QUEUE
- DROP_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping queues
- queues [Service Broker], removing
- deleting queues
- DROP QUEUE statement
- removing queues
ms.assetid: fd866520-ca00-477d-b2e9-0110e9610ed4
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: ead004ad07fbab696e42e5efdefa89a04cc0c2a2
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096935"
---
# <a name="drop-queue-transact-sql"></a>DROP QUEUE (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  既存のキューを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
DROP QUEUE <object>  
[ ; ]  
  
<object> ::=  
{ database_name.schema_name.queue_name | schema_name.queue_name | queue_name }
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *database_name*  
 削除するキューを含むデータベースの名前。 *database_name* を指定しない場合、既定では現在のデータベースが使用されます。  
  
 *schema_name (object)*  
 削除するキューを所有するスキーマの名前を指定します。 *schema_name* を指定しない場合、既定では現在のユーザーに関する既定のスキーマが使用されます。  
  
 *queue_name*  
 削除するキューの名前。  
  
## <a name="remarks"></a>解説  
 サービスでキューが参照されている場合は、キューを削除できません。  
  
## <a name="permissions"></a>アクセス許可  
 キューを削除する権限は、既定ではキューの所有者、**db_ddladmin** 固定データベース ロールまたは **db_owner** 固定データベース ロールのメンバー、および **sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="examples"></a>例  
 次の例では、現在のデータベースから **ExpenseQueue** キューを削除します。  
  
```sql  
DROP QUEUE ExpenseQueue ;  
```  
  
## <a name="see-also"></a>参照  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
