---
description: sp_dbfixedrolepermission (Transact-sql)
title: sp_dbfixedrolepermission (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbfixedrolepermission
- sp_dbfixedrolepermission_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbfixedrolepermission
ms.assetid: b8c30191-f532-49cd-83f3-c271f63ce572
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7a7abd42379d62d9a2c34adb50b7610494493b6c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536618"
---
# <a name="sp_dbfixedrolepermission-transact-sql"></a>sp_dbfixedrolepermission (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  固定データベース ロールの権限を表示します。 **sp_dbfixedrolepermission** では、に正しい情報が返さ [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] れます。 出力には、に実装された権限階層への変更は反映されません [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。 詳細については、「 [データベースレベルのロール](../../relational-databases/security/authentication-access/database-level-roles.md#fixed-database-roles)」を参照してください。これには、固定データベースロールの一覧と、それに対応する権限が表示されます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbfixedrolepermission [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @rolename = ] 'role'` 有効な固定データベースロールの名前を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *role* の部分は **sysname**で、既定値は NULL です。 *Role*が指定されていない場合は、すべての固定データベースロールの権限が表示されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|固定データベース ロールの名前。|  
|**権限**|**nvarchar (70)**|**Dbfixedrole**に関連付けられている権限|  
  
## <a name="remarks"></a>解説  
 固定データベースロールの一覧を表示するには、 **sp_helpdbfixedrole**を実行します。 次の表は、固定データベースロールを示しています。  
  
|固定データベースロール|説明|  
|-------------------------|-----------------|  
|**db_owner**|データベース所有者|  
|**db_accessadmin**|データベース アクセス管理者|  
|**db_securityadmin**|データベースセキュリティ管理者|  
|**db_ddladmin**|データベース データ定義言語 (DDL) 管理者|  
|**db_backupoperator**|データベースバックアップオペレーター|  
|**db_datareader**|データベースデータリーダー|  
|**db_datawriter**|データベースデータライター|  
|**db_denydatareader**|データベース否定データ リーダー|  
|**db_denydatawriter**|データベース拒否データライター|  
  
 **Db_owner**固定データベースロールのメンバーは、他のすべての固定データベースロールの権限を持っています。 固定サーバーロールの権限を表示するには、 **sp_srvrolepermission**を実行します。  
  
 結果セットには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 実行可能なステートメントと、データベースロールのメンバーによって実行可能なその他の特別な操作が含まれます。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次のクエリでは、固定データベースロールが指定されていないため、すべての固定データベースロールの権限が返されます。  
  
```  
EXEC sp_dbfixedrolepermission;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helpdbfixedrole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)   
 [sp_srvrolepermission &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
