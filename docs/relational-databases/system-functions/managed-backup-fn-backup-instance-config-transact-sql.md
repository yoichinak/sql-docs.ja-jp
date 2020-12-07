---
description: managed_backup。 fn_backup_instance_config (Transact-sql)
title: managed_backup。 fn_backup_instance_config (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_backup_instance_config
- smart_admin.fn_backup_instance_config_TSQL
- fn_backup_instance_config_TSQL
- smart_admin.fn_backup_instance_config
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_instance_config
- fn_backup_instance_config
ms.assetid: 2382a547-c0c9-4e1d-87c9-d8526192eb5a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a65649b7b565475eebd69bcadf4ac28bef707d7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419566"
---
# <a name="managed_backupfn_backup_instance_config-transact-sql"></a>managed_backup。 fn_backup_instance_config (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  SQL Server インスタンスを対象とした、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の既定の構成設定を含む行を 1 つ返します。  
  
 SQL Server のインスタンスの現在の既定の構成設定を確認または確認するには、このストアドプロシージャを使用し [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ます。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
managed_backup.fn_backup_db_config ()  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引数  
 None  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|is_smart_backup_enabled|INT|が有効になっている場合は1、が無効になっている場合は0が表示され [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ます。|  
|credential_name|SYSNAME|ストレージへの認証に使用される既定の SQL 資格情報。|  
|retention_days|INT|インスタンス レベルで設定されている既定の保有期間。|  
|storage_url|NVARCHAR (1024)|インスタンス レベルで設定されている既定のストレージ アカウントの URL。|  
|encryption_algorithm|SYSNAME|暗号化アルゴリズムの名前。 暗号化が指定されていない場合、は NULL に設定されます。|  
|encryptor_type|NVARCHAR (32)|使用される暗号化の種類:証明書キーまたは非対称キー。 暗号化機能が指定されていない場合、は NULL に設定されます。|  
|encryptor_name|SYSNAME|証明書または非対称キーの名前。 名前が指定されていない場合は、NULL に設定されます。|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 **ALTER ANY CREDENTIAL**権限を持つ**db_backupoperator**データベースロールのメンバーシップが必要です。 ユーザーは、 **VIEW ANY DEFINITION** 権限を拒否することはできません。  
  
## <a name="examples"></a>例  
 次の例では、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 実行されるインスタンスの既定の構成設定が返されます。  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_instance_config ();  
  
```  
  
  
