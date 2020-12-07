---
description: sp_addrole (Transact-sql)
title: sp_addrole (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addrole
- sp_addrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrole
ms.assetid: e8a21642-8440-419a-8585-93d3d9d44f00
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 245e617a9756e276bc06907a6f1592ec5383e69e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489573"
---
# <a name="sp_addrole-transact-sql"></a>sp_addrole (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースに新しいデータベース ロールを作成します。  
  
> [!IMPORTANT]
>  **sp_addrole**は、以前のバージョンのとの互換性のために含まれて [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] おり、将来のリリースではサポートされない可能性があります。 代わりに [CREATE ROLE](../../t-sql/statements/create-role-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addrole [ @rolename = ] 'role' [ , [ @ownername = ] 'owner' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @rolename = ] 'role'` 新しいデータベースロールの名前を指定します。 *role* は **sysname**で、既定値はありません。 *ロール* は有効な識別子 (ID) である必要があり、現在のデータベースに存在していない必要があります。  
  
`[ @ownername = ] 'owner'` 新しいデータベースロールの所有者を示します。 *owner* は **sysname**で、既定値は現在実行中のユーザーです。 *所有者* は、現在のデータベースのデータベースユーザーまたはデータベースロールである必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 データベースロールの名前には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 1 ~ 128 文字を含めることができます (文字、記号、数字を含む)。 データベースロールの名前には、円記号 ( \\ )、NULL、または空の文字列 (**' '**) を含めることはできません。  
  
 データベースロールを追加した後、 [sp_addrolemember &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) を使用してプリンシパルをロールに追加します。 GRANT、DENY、または REVOKE ステートメントを使用してデータベースロールに権限を適用すると、データベースロールのメンバーは、権限がそのアカウントに直接適用されているかのように権限を継承します。  
  
> [!NOTE]  
>  新しいサーバーロールを作成することはできません。 ロールは、データベース レベルでのみ作成できます。  
  
 **sp_addrole** は、ユーザー定義のトランザクション内では使用できません。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する CREATE ROLE 権限が必要です。 スキーマを作成する場合は、データベースに CREATE SCHEMA が必要です。 *Owner*がユーザーまたはグループとして指定されている場合、そのユーザーまたはグループに対して IMPERSONATE が必要です。 *Owner*がロールとして指定されている場合、そのロールまたはそのロールのメンバーに対する ALTER 権限が必要です。 Owner がアプリケーションロールとして指定されている場合は、そのアプリケーションロールに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、`Managers` という新しいロールを現在のデータベースに追加します。  
  
```  
EXEC sp_addrole 'Managers';  
```  
  
## <a name="see-also"></a>関連項目  
 [システムストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)  
  
  
