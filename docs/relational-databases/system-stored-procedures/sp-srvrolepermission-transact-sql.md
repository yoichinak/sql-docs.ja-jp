---
description: sp_srvrolepermission (Transact-sql)
title: sp_srvrolepermission (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_srvrolepermission_TSQL
- sp_srvrolepermission
dev_langs:
- TSQL
helpviewer_keywords:
- sp_srvrolepermission
ms.assetid: 5709667f-e3e4-48a2-93ec-af5e22a2ac58
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fb7a553adf516002a61f54ef900fd579f9d15856
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473714"
---
# <a name="sp_srvrolepermission-transact-sql"></a>sp_srvrolepermission (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  固定サーバーロールの権限を表示します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_srvrolepermission [ [ @srvrolename = ] 'role']  
```  
  
## <a name="arguments"></a>引数  
`[ @srvrolename = ] 'role'` 権限を返す固定サーバーロールの名前を指定します。 *role* の部分は **sysname**で、既定値は NULL です。 ロールが指定されていない場合は、すべての固定サーバーロールの権限が返されます。 *ロール* は、次のいずれかの値を持つことができます。  
  
|値|説明|  
|-----------|-----------------|  
|**sysadmin**|システム管理者|  
|**securityadmin**|セキュリティ管理者|  
|**serveradmin**|サーバー管理者。|  
|**setupadmin**|セットアップ管理者|  
|**processadmin**|プロセス管理者|  
|**diskadmin**|ディスク管理者|  
|**dbcreator**|データベース作成者。|  
|**bulkadmin**|BULK INSERT ステートメントを実行できます|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**ServerRole**|**sysname**|固定サーバーロールの名前|  
|**権限**|**sysname**|**ServerRole**に関連付けられたアクセス許可|  
  
## <a name="remarks"></a>解説  
 表示される権限には、固定サーバー ロールのメンバーが実行できる、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントとその他の特別な操作が含まれます。 固定サーバーロールの一覧を表示するには、 **sp_helpsrvrole**を実行します。  
  
 **Sysadmin**固定サーバーロールには、他のすべての固定サーバーロールの権限が与えられています。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次のクエリでは、固定サーバー ロール `sysadmin` に関連する権限が返されます。  
  
```  
EXEC sp_srvrolepermission 'sysadmin';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_dropsrvrolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [sp_helpsrvrole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
