---
description: sp_validatelogins (Transact-sql)
title: sp_validatelogins (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_validatelogins
- sp_validatelogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validatelogins
ms.assetid: 6ac52e21-e20d-469b-ad40-5aa091e06b61
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b3237ed7a7d585e128b678772ec6d3a010fe3d00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473441"
---
# <a name="sp_validatelogins-transact-sql"></a>sp_validatelogins (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  プリンシパルにマップされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が windows 環境に存在しなくなった windows ユーザーおよびグループに関する情報を報告します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_validatelogins  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**SID**|**varbinary (85)**|Windows ユーザーまたはグループの windows セキュリティ識別子 (SID)。|  
|**NT Login**|**sysname**|Windows ユーザーまたはグループの名前。|  
  
## <a name="remarks"></a>解説  
 孤立したサーバー レベルのプリンシパルがデータベース ユーザーを所有している場合、孤立したサーバー プリンシパルを削除するには、先にデータベース ユーザーを削除する必要があります。 データベースユーザーを削除するには、 [DROP user](../../t-sql/statements/drop-user-transact-sql.md)を使用します。 サーバーレベルのプリンシパルがデータベースで securables を所有している場合は、securables の所有権を転送するか、削除する必要があります。 データベース securables の所有権を譲渡するには、 [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)を使用します。  
  
 存在しなくなった Windows ユーザーおよびグループへのマッピングを削除するには、 [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**または**securityadmin**固定サーバーロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、存在しなくなってものインスタンスへのアクセスが許可されている Windows ユーザーおよびグループを表示し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
```  
EXEC sp_validatelogins;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システムストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Transact-sql&#41;&#40;のログインを削除します。 ](../../t-sql/statements/drop-login-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
