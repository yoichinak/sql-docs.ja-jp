---
description: sys.server_permissions (Transact-SQL)
title: server_permissions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 09/20/2019
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.server_permissions_TSQL
- sys.server_permissions
- server_permissions
- server_permissions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_permissions catalog view
ms.assetid: 7d78bf17-6c64-4166-bd0b-9e9e20992136
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a8f0541d743ea7feaa8991c2b085173b4c6e8f40
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88376938"
---
# <a name="sysserver_permissions-transact-sql"></a>sys.server_permissions (Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  サーバーレベルの権限ごとに1行の値を返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|権限が存在するリソースのクラスの識別子。<br /><br /> 100 = サーバー<br /><br /> 101 = サーバープリンシパル<br /><br /> 105 = エンドポイント|  
|**class_desc**|**nvarchar(60)**|権限が存在するクラスの説明です。 次のいずれかの値です。<br /><br /> **SERVER**<br /><br /> **SERVER_PRINCIPAL**<br /><br /> **終点**|  
|**major_id**|**int**|権限が存在するセキュリティ保護可能なリソースの ID。クラスに基づいて解釈されます。 ほとんどの場合、これはクラスが表すものに適用される ID の種類にすぎません。 標準以外のリソースに対する解釈は、次のようになります。<br /><br /> 100 = 常に0|  
|**minor_id**|**int**|権限が存在するセカンダリ ID。クラスに従って解釈されます。|  
|**grantee_principal_id**|**int**|権限が付与されているサーバープリンシパル ID。|  
|**grantor_principal_id**|**int**|サーバープリンシパル-これらのアクセス許可の権限の許可の付与の ID。|  
|**type**|**char (4)**|サーバー権限の種類。 権限の種類の一覧については、次の表を参照してください。|  
|**permission_name**|**nvarchar(128)**|アクセス許可の名前。|  
|**状態**|**char (1)**|アクセス許可の状態:<br /><br /> D = 拒否<br /><br /> R = 取り消し<br /><br /> G = 許可<br /><br /> W = grant With Grant option|  
|**state_desc**|**nvarchar(60)**|権限の状態の説明。<br /><br /> DENY<br /><br /> REVOKE<br /><br /> GRANT<br /><br /> GRANT_WITH_GRANT_OPTION|  
  
|アクセス許可の種類|アクセス許可名|適用されるセキュリティ保護可能なリソース|  
|---------------------|---------------------|--------------------------|  
|AAES|ALTER ANY EVENT SESSION|SERVER|
|ADBO|ADMINISTER BULK OPERATIONS|SERVER|  
|AL|ALTER|エンドポイント、ログイン|  
|ALAA|ALTER ANY SERVER AUDIT|SERVER|
|ALAG|ALTER ANY AVAILABILITY GROUP|SERVER|
|ALCD|ALTER ANY CREDENTIAL|SERVER|  
|ALCO|ALTER ANY CONNECTION|SERVER|  
|ALDB|ALTER ANY DATABASE|SERVER|  
|ALES|ALTER ANY EVENT NOTIFICATION|SERVER|  
|ALHE|ALTER ANY ENDPOINT|SERVER|  
|ALLG|ALTER ANY LOGIN|SERVER|  
|ALLS|ALTER ANY LINKED SERVER|SERVER|  
|ALRS|ALTER RESOURCES|SERVER|
|ALSR|ALTER ANY SERVER ROLE|SERVER|  
|ALSS|ALTER SERVER STATE|SERVER|  
|ALST|ALTER SETTINGS|SERVER|  
|ALTR|ALTER TRACE|SERVER|  
|AUTH|AUTHENTICATE SERVER|SERVER|
|CADB|CONNECT ANY DATABASE|SERVER|  
|CL|CONTROL|エンドポイント、ログイン|  
|CL|CONTROL SERVER|SERVER|  
|CO|CONNECT|ENDPOINT|  
|COSQ|CONNECT SQL|SERVER|
|CRAC|CREATE AVAILABILITY GROUP|SERVER|  
|CRDB|CREATE ANY DATABASE|SERVER|  
|CRDE|CREATE DDL EVENT NOTIFICATION|SERVER|  
|CRHE|CREATE ENDPOINT|SERVER|
|CRSR|CREATE SERVER ROLE|SERVER|  
|CRTE|CREATE TRACE EVENT NOTIFICATION|SERVER|
|IAL|IMPERSONATE ANY LOGIN|SERVER|  
|IM|IMPERSONATE|Login|  
|SHDN|SHUTDOWN|SERVER|
|SUS|SELECT ALL USER SECURABLES|SERVER|
|TO|TAKE OWNERSHIP|ENDPOINT|  
|VW|VIEW DEFINITION|エンドポイント、ログイン|  
|VWAD|VIEW ANY DEFINITION|SERVER|  
|VWDB|VIEW ANY DATABASE|SERVER|  
|VWSS|VIEW SERVER STATE|SERVER|  
|XA|外部アクセス|SERVER|
|XU|UNSAFE ASSEMBLY|SERVER|
  
## <a name="permissions"></a>アクセス許可  
 すべてのユーザーは自分の権限を参照できます。 他のログインの権限を表示するには、VIEW DEFINITION、ALTER ANY LOGIN、またはログインに対する権限が必要です。 ユーザー定義サーバーロールを表示するには、ALTER ANY SERVER ROLE または ROLE のメンバーシップが必要です。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>例  
 次のクエリは、サーバープリンシパルに対して明示的に許可または拒否された権限を一覧表示します。  
  
> [!IMPORTANT]  
> 固定サーバー ロールの権限は、sys.server_permissions には表示されません。 そのため、サーバープリンシパルには、ここに記載されていない追加のアクセス許可がある場合があります。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pe.state_desc, pe.permission_name   
FROM sys.server_principals AS pr   
JOIN sys.server_permissions AS pe   
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
## <a name="see-also"></a>参照  
 [セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [権限の階層 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
