---
description: sp_releaseapplock (Transact-SQL)
title: sp_releaseapplock (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_releaseapplock_TSQL
- sp_releaseapplock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_releaseapplock
ms.assetid: 51b03c2f-0d54-40f5-9172-e747942d4a46
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ec619fc8053b735e952b2577f6cdee5d4647e652
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538668"
---
# <a name="sp_releaseapplock-transact-sql"></a>sp_releaseapplock (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  アプリケーションリソースのロックを解放します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_releaseapplock [ @Resource = ] 'resource_name'   
     [ , [ @LockOwner = ] 'lock_owner' ]  
     [ , [ @DbPrincipal = ] 'database_principal' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 [ @Resource =] '*resource_name*'  
 は、クライアントアプリケーションによって指定されたロックリソース名です。 アプリケーションでは、リソースが一意であることを確認する必要があります。 指定した名前は内部的にハッシュされ、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロック マネージャーに格納できる値に変換されます。 *resource_name* は **nvarchar (255)** で、既定値はありません。 *resource_name* はバイナリ比較されます。したがって、現在のデータベースの照合順序の設定に関係なく、大文字と小文字が区別されます。  
  
 [ @LockOwner =] '*lock_owner*'  
 ロックの所有者を指定します。これはロックが要求されたときの *lock_owner* 値です。 *lock_owner* は **nvarchar (32)** です。 この値は **Transaction** (既定値) または **Session** のいずれかです。 *Lock_owner*値が**transaction**、既定で、または明示的に指定されている場合、sp_getapplock はトランザクション内から実行する必要があります。  
  
 [ @DbPrincipal =] '*database_principal*'  
 データベース内のオブジェクトに対する権限を持つユーザー、ロール、またはアプリケーションロールを設定します。 関数を正常に呼び出すには、関数の呼び出し元が *database_principal*、dbo、または db_owner 固定データベースロールのメンバーである必要があります。 既定値はパブリックです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 \>= 0 (成功)、または < 0 (失敗)  
  
|[値]|結果|  
|-----------|------------|  
|0|ロックが正常に解放されました。|  
|-999|パラメーターの検証エラーまたはその他の呼び出しエラーです。|  
  
## <a name="remarks"></a>解説  
 アプリケーションで、同じロック リソースに対して sp_getapplock が複数回呼び出される場合は、同じ回数だけ sp_releaseapplock を呼び出して、ロックを解放する必要があります。  
  
 何らかの理由でサーバーがシャットダウンすると、ロックが解放されます。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、データベース内のリソースの現在のトランザクションに関連付けられているロックを解放し `Form1` `AdventureWorks2012` ます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_getapplock @DbPrincipal = 'dbo', @Resource = 'Form1',   
     @LockMode = 'Shared';  
EXEC sp_releaseapplock @DbPrincipal = 'dbo', @Resource = 'Form1';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [APPLOCK_MODE &#40;Transact-sql&#41;](../../t-sql/functions/applock-mode-transact-sql.md)   
 [APPLOCK_TEST &#40;Transact-sql&#41;](../../t-sql/functions/applock-test-transact-sql.md)   
 [sp_getapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
  
  
