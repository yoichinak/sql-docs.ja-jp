---
description: server_file_audits (Transact-sql)
title: server_file_audits (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_file_audits_TSQL
- sys.server_file_audits_TSQL
- sys.server_file_audits
- server_file_audits
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_file_audits catalog view
ms.assetid: 553288a0-be57-4d79-ae53-b7cbd065e127
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bfe2aebe8a85e8ca32641e4cf334298aa1485956
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542451"
---
# <a name="sysserver_file_audits-transact-sql"></a>server_file_audits (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバーインスタンス上の監査に含まれるファイル監査の種類に関する拡張情報を格納 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 詳しくは、「[SQL Server Audit &#40;データベース エンジン&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|audit_id|**int**|監査の ID。|  
|name|**sysname**|監査の名前。|  
|audit_guid|**uniqueidentifier**|監査の GUID。|  
|create_date|**datetime**|ファイル監査が作成された UTC 日付。|  
|modify_date|**datatime**|ファイル監査が最後に変更された UTC 日付。|  
|principal_id|**int**|サーバーに登録されている監査の所有者の ID。|  
|型|**char(2)**|監査の種類。<br /><br /> 0 = NT セキュリティ イベント ログ<br /><br /> 1 = NT アプリケーションイベントログ<br /><br /> 2 = ファイル システムのファイル|  
|type_desc|**nvarchar(60)**|監査の種類の説明。|  
|on_failure|**tinyint**|エラー状態時:<br /><br /> 0 = 続行<br /><br /> 1 = サーバー インスタンスのシャットダウン<br /><br /> 2 = 失敗の操作|  
|on_failure_desc|**nvarchar(60)**|アクションエントリの書き込みに失敗した場合:<br /><br /> CONTINUE<br /><br /> サーバーインスタンスのシャットダウン<br /><br /> 失敗した操作|  
|is_state_enabled|**tinyint**|0 = 無効<br /><br /> 1 = 有効|  
|queue_delay|**int**|ディスクに書き込む前に待機する最大時間をミリ秒単位で提示します。 0 の場合は、イベントが続行する前に必ず書き込みが行われます。|  
|predicate|**nvarchar (8000)**|イベントに適用される述語式。|  
|max_file_size|**bigint**|監査の最大サイズ (MB):<br /><br /> 0 = 無制限/選択した監査タイプには適用されません。|  
|max_rollover_files|**int**|ロールオーバーオプションと共に使用するファイルの最大数。|  
|max_files|**int**|ロールオーバーオプションを指定せずに使用するファイルの最大数。|  
|reserved_disk_space|**int**|ファイルごとに予約するディスク領域のサイズ。|  
|log_file_path|**nvarchar(260)**|監査が配置される場所のパス。 ファイル監査のファイルパス、アプリケーションログ監査のアプリケーションログパス。|  
|log_file_name|**nvarchar(260)**|CREATE AUDIT DDL で提供されるログ ファイルの基本名。 base_log_name ファイルにサフィックスとして連番が付加されて、ログ ファイル名が作成されます。|  
  
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
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [server_file_audits (Transact-sql)](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [サーバー監査およびサーバー監査の仕様を作成する](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
