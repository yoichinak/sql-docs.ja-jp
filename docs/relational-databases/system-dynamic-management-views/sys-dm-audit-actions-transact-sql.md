---
description: sys.dm_audit_actions (Transact-SQL)
title: dm_audit_actions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_audit_actions_TSQL
- sys.dm_audit_actions
- dm_audit_actions_TSQL
- dm_audit_actions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_audit_actions dynamic management view
ms.assetid: b987c2b9-998a-4a5f-a82d-280dc6963cbe
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 897d83dcf6c85606ac513d9075cca9ebc316a6cf
ms.sourcegitcommit: 27f95e50f11a98164e9e7a5130a3e00ac06b4cea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2020
ms.locfileid: "91412818"
---
# <a name="sysdm_audit_actions-transact-sql"></a>sys.dm_audit_actions (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  監査ログで報告される可能性のあるすべての監査アクション、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit の一部として構成できるすべての監査アクション グループに対して 1 つの行を返します。 監査の詳細につい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ては、「 [SQL Server audit &#40;データベースエンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**action_id**|**varchar (4)**|監査アクションの ID。 各監査レコードに書き込まれた **action_id** 値に関連します。 NULL 値が許可されます。 監査グループの場合は NULL。|  
|**action_in_log**|**bit**|アクションを監査ログに書き込むことができるかどうかを示します。 値は次のとおりです。<br /><br /> 1 = はい<br /><br /> 0 = いいえ|  
|**name**|**sysname**|監査アクションまたはアクショングループの名前。 NULL 値は許可されません。|  
|**class_desc**|**nvarchar(120)**|監査アクションが適用されるオブジェクトのクラス名。 には、サーバー、データベース、またはスキーマスコープオブジェクトのいずれかを指定できますが、スキーマオブジェクトは含まれません。 NULL 値は許可されません。|  
|**parent_class_desc**|**nvarchar(120)**|class_desc で記述されるオブジェクトの親クラスの名前。 Class_desc がサーバーの場合は NULL です。|  
|**covering_parent_action_name**|**nvarchar(120)**|この行で記述される監査アクションを含む、監査アクションまたは監査グループの名前。 これは、アクションとカバーアクションの階層を作成するために使用されます。 NULL 値が許可されます。|  
|**configuration_level**|**nvarchar (10)**|この行に指定されているアクションまたはアクショングループがグループまたはアクションレベルで構成可能であることを示します。 アクションが構成可能でない場合、は NULL になります。|  
|**containing_group_name**|**nvarchar(120)**|指定されたアクションを含む監査グループの名前。 Name の値がグループの場合は NULL になります。|  
  
## <a name="permissions"></a>アクセス許可  
このビューはパブリックに表示されます。
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]. 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [サーバー監査およびサーバー監査の仕様を作成する](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
