---
description: server_audits (Transact-sql)
title: server_audits (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_audits_TSQL
- sys.server_audits_TSQL
- sys.server_audits
- server_audits
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_audits catalog view
ms.assetid: c2c4a000-1127-46a8-b1e9-947fd1136e1e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ea8ed9b7b779b9a81743ab909aa2bbba1e3c4856
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539615"
---
# <a name="sysserver_audits-transact-sql"></a>server_audits (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバー インスタンス内の各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 監査について行を 1 つずつ含みます。 詳しくは、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**audit_id**|**int**|監査の ID。|  
|**name**|**sysname**|監査の名前。|  
|**audit_guid**|**uniqueidentifier**|サーバーの起動時およびデータベースのアタッチ操作中に、メンバーサーバー&#124;データベース監査の仕様による監査を列挙するために使用される監査の GUID。|  
|**create_date**|**datetime**|監査が作成された UTC 日付。|  
|**modify_date**|**datetime**|監査が最後に変更された UTC 日付。|  
|**principal_id**|**int**|サーバーに登録されている監査の所有者の ID。|  
|**type**|**char(2)**|監査の種類。<br /><br /> SL-NT セキュリティイベントログ<br /><br /> AL-NT アプリケーションイベントログ<br /><br /> ファイルシステム上の FL ファイル|  
|**type_desc**|**nvarchar(60)**|SECURITY LOG<br /><br /> APPICATION ログ<br /><br /> FILE|  
|**on_failure**|**tinyint**|アクションエントリの書き込みに失敗した場合:<br /><br /> 0-続行<br /><br /> 1-サーバーインスタンスのシャットダウン<br /><br /> 2-失敗した操作|  
|**on_failure_desc**|**nvarchar(60)**|アクションエントリの書き込みに失敗した場合:<br /><br /> CONTINUE<br /><br /> サーバーインスタンスのシャットダウン<br /><br /> FAIL_OPERATION|  
|**is_state_enabled**|**tinyint**|0-無効<br /><br /> 1 - 有効|  
|**queue_delay**|**int**|ディスクに書き込むまでの最大待機時間 (ミリ秒単位)。 0の場合、イベントが続行される前に、監査によって書き込みが保証されます。|  
|**predicate**|**nvarchar (3000)**|イベントに適用される述語式。|  
  
## <a name="permissions"></a>アクセス許可  
 **ALTER ANY SERVER AUDIT**または**VIEW any DEFINITION**権限を持つプリンシパルは、このカタログビューにアクセスできます。 また、プリンシパルに **対して VIEW ANY DEFINITION** 権限を拒否することはできません。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
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
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [サーバー監査およびサーバー監査の仕様を作成する](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
