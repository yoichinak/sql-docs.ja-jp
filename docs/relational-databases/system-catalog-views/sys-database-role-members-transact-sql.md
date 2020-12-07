---
description: sys.database_role_members (Transact-SQL)
title: database_role_members (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_role_members_TSQL
- sys.database_role_members
- database_role_members_TSQL
- database_role_members
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_role_members catalog view
ms.assetid: ed1b019d-ca48-4db3-85df-cf6d2db591cf
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 443df263f534d6f15648caacb5a810a0c15e555a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482141"
---
# <a name="sysdatabase_role_members-transact-sql"></a>sys.database_role_members (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  データベース ロールのメンバーごとに 1 行のデータを返します。  データベースユーザー、アプリケーションロール、およびその他のデータベースロールは、データベースロールのメンバーになることができます。 ロールにメンバーを追加するには、 [ALTER role](../../t-sql/statements/alter-role-transact-sql.md) ステートメントをオプションと共に使用し `ADD MEMBER` ます。 値の名前を返すには、 [database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)と結合します。 `principal_id`
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**role_principal_id**|**int**|ロールのデータベースプリンシパル ID。|  
|**member_principal_id**|**int**|メンバーのデータベースプリンシパル ID。|  
  
## <a name="permissions"></a>アクセス許可  
 すべてのユーザーは自分のロールのメンバーシップを参照できます。 他のロールのメンバーシップを表示するに `db_securityadmin` は、固定データベースロールまたはデータベースのメンバーシップが必要です `VIEW DEFINITION` 。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のクエリでは、データベースロールのメンバーが返されます。  
  
```  
SELECT DP1.name AS DatabaseRoleName,   
   isnull (DP2.name, 'No members') AS DatabaseUserName   
 FROM sys.database_role_members AS DRM  
 RIGHT OUTER JOIN sys.database_principals AS DP1  
   ON DRM.role_principal_id = DP1.principal_id  
 LEFT OUTER JOIN sys.database_principals AS DP2  
   ON DRM.member_principal_id = DP2.principal_id  
WHERE DP1.type = 'R'
ORDER BY DP1.name;  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [プリンシパル &#40;データベース エンジン&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
[ALTER ROLE (Transact-sql)](../../t-sql/statements/alter-role-transact-sql.md)      
[sys.server_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)   
  


