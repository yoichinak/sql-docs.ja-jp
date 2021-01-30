---
description: sp_helpsrvrolemember (Transact-sql)
title: sp_helpsrvrolemember (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_helpsrvrolemember
- sp_helpsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrolemember
ms.assetid: d0714913-8d6b-4de3-b042-3ae9934f839d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f17a4be7d5e9b1511a840857c933ed240d0e3d31
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99198698"
---
# <a name="sp_helpsrvrolemember-transact-sql"></a>sp_helpsrvrolemember (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定サーバー ロールのメンバーに関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpsrvrolemember [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @srvrolename = ] 'role'` 固定サーバーロールの名前を指定します。 *role* の部分は **sysname** で、既定値は NULL です。 *Role* が指定されていない場合、結果セットには、すべての固定サーバーロールに関する情報が含まれます。  
  
 *role* には、次のいずれかの値を指定できます。  
  
|固定サーバーロール|説明|  
|-----------------------|-----------------|  
|[sysadmin]|システム管理者|  
|securityadmin|セキュリティ管理者|  
|serveradmin|サーバー管理者。|  
|setupadmin|セットアップ管理者|  
|processadmin|プロセス管理者|  
|diskadmin|ディスク管理者|  
|dbcreator|データベース作成者。|  
|bulkadmin|BULK INSERT ステートメントを実行できます|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|サーバーロールの名前|  
|メンバー名|**sysname**|ServerRole のメンバーの名前。|  
|MemberSID|**varbinary(85)**|MemberName のセキュリティ識別子|  
  
## <a name="remarks"></a>コメント  
 データベースロールのメンバーを表示するには、sp_helprolemember を使用します。  
  
 すべてのログインは public のメンバーです。 内部で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は public がロールとして実装されていないため、sp_helpsrvrolemember はパブリックロールを認識しません。  
  
 サーバーロールのメンバーを追加または削除するには、「 [ALTER SERVER ROLE &#40;transact-sql&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)」を参照してください。  
  
 sp_helpsrvrolemember は、ユーザー定義のサーバーロールを引数として受け取りません。 ユーザー定義サーバーロールのメンバーを確認するには、「 [ALTER SERVER role &#40;transact-sql&#41;](../../t-sql/statements/alter-server-role-transact-sql.md)」の例を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 public ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、固定サーバーロールのメンバーを一覧表示し `sysadmin` ます。  
  
```  
EXEC sp_helpsrvrolemember 'sysadmin';  
```  
  
## <a name="see-also"></a>参照  
 [sp_helprole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helprolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
