---
description: sp_helpuser (Transact-SQL)
title: sp_helpuser (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpuser
- sp_helpuser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpuser
ms.assetid: 9c70b41d-ef4c-43df-92da-bd534c287ca1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e9ea3b0b0b6d1700c486514c29f889cc7beb3566
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546042"
---
# <a name="sp_helpuser-transact-sql"></a>sp_helpuser (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベースに存在するデータベース レベルのプリンシパルに関する情報をレポートします。  
  
> [!IMPORTANT]  
>  **sp_helpuser** は、で導入された securables に関する情報を返しません [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。 代わりに、 [sys. database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpuser [ [ @name_in_db = ] 'security_account' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @name_in_db = ] 'security_account'` 現在のデータベースのデータベースユーザーまたはデータベースロールの名前を指定します。 *security_account* は、現在のデータベースに存在している必要があります。 *security_account* は **sysname**,、既定値は NULL です。 *Security_account*が指定されていない場合、 **sp_helpuser**はすべてのデータベースプリンシパルに関する情報を返します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の表は、ユーザーアカウントも [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows ユーザーも、 *security_account*に対して指定されていない場合の結果セットを示しています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**UserName**|**sysname**|現在のデータベース内のユーザー。|  
|**RoleName**|**sysname**|**ユーザー名**が属するロール。|  
|**LoginName**|**sysname**|**ユーザー名**のログイン。|  
|**DefDBName**|**sysname**|**ユーザー名**の既定のデータベース。|  
|**DefSchemaName**|**sysname**|データベースユーザーの既定のスキーマ。|  
|**UserID**|**smallint**|現在のデータベースの **ユーザー名** の ID。|  
|**SID**|**smallint**|ユーザーのセキュリティ識別番号 (SID)。|  
  
 次の表は、ユーザーアカウントが指定されておらず、現在のデータベースに別名が存在する場合の結果セットを示しています。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|現在のデータベースに存在するユーザーの別名であるログイン。|  
|**UserNameAliasedTo**|**sysname**|ログインがエイリアス化されている現在のデータベース内のユーザー名。|  
  
 次の表に、 *security_account*にロールを指定した場合の結果セットを示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**Role_name**|**sysname**|現在のデータベース内のロールの名前。|  
|**Role_id**|**smallint**|現在のデータベース内のロールのロール ID。|  
|**Users_in_role**|**sysname**|現在のデータベースのロールのメンバー。|  
|**Userid**|**smallint**|ロールのメンバーのユーザー ID。|  
  
## <a name="remarks"></a>解説  
 データベースロールのメンバーシップに関する情報を表示するには、 [database_role_members](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)を使用します。 サーバーロールのメンバーに関する情報を表示するには、 [server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)を使用し、サーバーレベルのプリンシパルに関する情報を表示するには、 [server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
 返される情報には、メタデータへのアクセスに関する制限が適用されます。 プリンシパルに権限がないエンティティは表示されません。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-all-users"></a>A. すべてのユーザーを表示する  
 次の例では、現在のデータベースに存在するすべてのユーザーを表示します。  
  
```  
EXEC sp_helpuser;  
```  
  
### <a name="b-listing-information-for-a-single-user"></a>B. 特定のユーザーの情報を表示する  
 次の例では、ユーザーデータベースの所有者 () に関する情報を一覧表示し `dbo` ます。  
  
```  
EXEC sp_helpuser 'dbo';  
```  
  
### <a name="c-listing-information-for-a-database-role"></a>C. データベースロールの情報を一覧表示する  
 次の例では、`db_securityadmin` 固定データベース ロールに関する情報を表示します。  
  
```  
EXEC sp_helpuser 'db_securityadmin';  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
  
