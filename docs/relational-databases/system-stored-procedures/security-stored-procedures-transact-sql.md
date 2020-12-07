---
description: セキュリティストアドプロシージャ (Transact-sql)
title: セキュリティストアドプロシージャ (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system stored procedures [SQL Server], security
- stored procedures [SQL Server], security
- security [SQL Server], stored procedures
ms.assetid: 62b72907-7e95-4c97-9891-0c45d5b678ce
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a36470835da89f54fdfa9e474ed8b5e993ef0377
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753970"
---
# <a name="security-stored-procedures-transact-sql"></a>セキュリティストアドプロシージャ (Transact-sql)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、セキュリティの管理に使用される次のシステムストアドプロシージャがサポートされています。 これらのストアドプロシージャの一部は非推奨とされますが、旧バージョンとの互換性をサポートするために引き続き使用できます。 非推奨のプロシージャに関するトピックでは、それらの置換の一覧が表示されます。  

:::row:::
    :::column:::
        [sys.sp_add_trusted_assembly]( sys-sp-add-trusted-assembly-transact-sql.md) 
    :::column-end:::
    :::column:::
        [sp_addapprole](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md) (非推奨)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)
    :::column-end:::
    :::column:::
        [sp_addlinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_addlogin](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_addremotelogin](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md) (非推奨)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) (非推奨)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_addserver](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md) (非推奨)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_approlepassword](../../relational-databases/system-stored-procedures/sp-approlepassword-transact-sql.md) (非推奨)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_audit_write](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md) 
    :::column-end:::
    :::column:::
        [sp_change_users_login](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md) (非推奨)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_changeobjectowner](../../relational-databases/system-stored-procedures/sp-changeobjectowner-transact-sql.md) (非推奨)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_control_dbmasterkey_password](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md) 
    :::column-end:::
    :::column:::
        [sp_dbfixedrolepermission](../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md) (非推奨)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md) (非推奨)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_denylogin](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_dropalias](./system-stored-procedures-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sys.sp_drop_trusted_assembly]( sys-sp-drop-trusted-assembly-transact-sql.md) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_dropapprole](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_droplogin](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_dropremotelogin](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md) (非推奨) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_droprole](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_droprolemember](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) (非推奨) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_dropserver](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md) 
    :::column-end:::
    :::column:::
        [sp_dropsrvrolemember](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md) (非推奨) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_dropuser](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_grantdbaccess](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md) (非推奨) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_helpdbfixedrole](../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_helplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-helplinkedsrvlogin-transact-sql.md) 
    :::column-end:::
    :::column:::
        [sp_helplogins](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_helpntgroup](../../relational-databases/system-stored-procedures/sp-helpntgroup-transact-sql.md) 
    :::column-end:::
    :::column:::
        [sp_helpremotelogin](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md) (非推奨) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_helprole](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md) 
    :::column-end:::
    :::column:::
        [sp_helprolemember](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_helprotect](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md) (非推奨) 
    :::column-end:::
    :::column:::
        [sp_helpsrvrole](../../relational-databases/system-stored-procedures/sp-helpsrvrole-transact-sql.md) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_helpsrvrolemember](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md) 
    :::column-end:::
    :::column:::
        [sp_helpuser](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md) (非推奨) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_migrate_user_to_contained](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md)
    :::column-end:::
    :::column:::
        [sp_MShasdbaccess](../../relational-databases/system-stored-procedures/sp-mshasdbaccess-transact-sql.md) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md) (非推奨)
    :::column-end:::
    :::column:::
        [sp_refresh_parameter_encryption](../../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_remoteoption](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md) (非推奨)
    :::column-end:::
    :::column:::
        [sp_revokedbaccess](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md) (非推奨) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_revokelogin](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md) (非推奨)
    :::column-end:::
    :::column:::
        [sp_setapprole](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_srvrolepermission](../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md) (非推奨)
    :::column-end:::
    :::column:::
        [sp_testlinkedserver](../../relational-databases/system-stored-procedures/sp-testlinkedserver-transact-sql.md) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_unsetapprole](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md) 
    :::column-end:::
    :::column:::
        [sp_validatelogins](../../relational-databases/system-stored-procedures/sp-validatelogins-transact-sql.md) 
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_xp_cmdshell_proxy_account](../../relational-databases/system-stored-procedures/sp-xp-cmdshell-proxy-account-transact-sql.md) 
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
