---
description: sp_helpdbfixedrole (Transact-SQL)
title: sp_helpdbfixedrole (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdbfixedrole
- sp_helpdbfixedrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdbfixedrole
ms.assetid: ad87e9a0-b901-4e37-9950-aa517d680fc3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e0b72a64d8d895956273a7c76e21dbb88152b546
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538803"
---
# <a name="sp_helpdbfixedrole-transact-sql"></a>sp_helpdbfixedrole (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  固定データベース ロールの一覧を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdbfixedrole [ [ @rolename = ] 'role' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @rolename = ] 'role'` 固定データベースロールの名前を指定します。 *role* の部分は **sysname**で、既定値は NULL です。 *Role*を指定すると、そのロールに関する情報のみが返されます。それ以外の場合は、すべての固定データベースロールの一覧と説明が返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|固定データベースロールの名前。|  
|**説明**|**nvarchar (70)**|**Dbfixedrole の説明です。**|  
  
## <a name="remarks"></a>解説  
 次の表に示すように、固定データベースロールはデータベースレベルで定義され、特定のデータベースレベルの管理アクティビティを実行する権限を持っています。 固定データベース ロールは、追加または削除できません。 固定データベースロールに付与された権限は変更できません。  
  
|固定データベースロール|説明|  
|-------------------------|-----------------|  
|**db_owner**|データベース所有者|  
|**db_accessadmin**|データベース アクセス管理者|  
|**db_securityadmin**|データベースセキュリティ管理者|  
|**db_ddladmin**|データベース DDL 管理者|  
|**db_backupoperator**|データベースバックアップオペレーター|  
|**db_datareader**|データベースデータリーダー|  
|**db_datawriter**|データベースデータライター|  
|**db_denydatareader**|データベース否定データ リーダー|  
|**db_denydatawriter**|データベース拒否データライター|  
  
 次の表は、データベース ロールを変更するときに使用するストアド プロシージャです。  
  
|ストアド プロシージャ|アクション|  
|----------------------|------------|  
|**sp_addrolemember**|固定データベースロールにデータベースユーザーを追加します。|  
|**sp_helprole**|固定データベース ロールのメンバーの一覧を表示します。|  
|**sp_droprolemember**|固定データベースロールからメンバーを削除します。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
 返される情報には、メタデータへのアクセスに関する制限が適用されます。 プリンシパルに権限がないエンティティは表示されません。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、すべての固定データベースロールの一覧を示します。  
  
```  
EXEC sp_helpdbfixedrole;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_dbfixedrolepermission &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md)   
 [sp_droprolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helprolemember &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
