---
description: managed_backup。 sp_backup_config_advanced (Transact-sql)
title: managed_backup。 sp_backup_config_advanced (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_optional
- sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional
dev_langs:
- TSQL
helpviewer_keywords:
- sp_backup_config_optional
- managed_backup.sp_backup_config_optional
ms.assetid: 4fae8193-1f88-48fd-a94a-4786efe8d6af
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 877b9d2db59ba060c766a27b6b040a6b0f48dc73
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89529485"
---
# <a name="managed_backupsp_backup_config_advanced-transact-sql"></a>managed_backup。 sp_backup_config_advanced (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  の詳細設定を構成 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
EXEC managed_backup.sp_backup_config_advanced   
    [@database_name = ] 'database_name'  
    ,[@encryption_algorithm = ] 'name of the encryption algorithm'  
    ,[@encryptor_type = ] {'CERTIFICATE' | 'ASYMMETRIC_KEY'}  
    ,[@encryptor_name = ] 'name of the certificate or asymmetric key'  
    ,[@local_cache_path = ] 'NOT AVAILABLE'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引数  
 @database_name  
 特定のデータベースでマネージバックアップを有効にするためのデータベース名。 NULL または * の場合、このマネージバックアップはサーバー上のすべてのデータベースに適用されます。  
  
 @encryption_algorithm  
 バックアップ中にバックアップファイルを暗号化するために使用される暗号化アルゴリズムの名前。 @encryption_algorithmは**SYSNAME**です。 データベースに対して初めて [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を構成する場合の必須パラメーターです。 バックアップファイルを暗号化しない場合は、 **NO_ENCRYPTION** を指定します。 構成設定を変更する場合 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 、このパラメーターは省略可能です。パラメーターが指定されていない場合は、既存の構成値が保持されます。 このパラメーターに指定できる値は次のとおりです。  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 暗号化アルゴリズムの詳細については、「 [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)」をご覧ください。  
  
 @encryptor_type  
 暗号化機能の種類。 "CERTIFICATE" または "ASYMMETRIC_KEY" のいずれかになります。 @encryptor_typeは**nvarchar (32)** です。 パラメーターに NO_ENCRYPTION を指定した場合、このパラメーターは省略可能です @encryption_algorithm 。  
  
 @encryptor_name  
 バックアップの暗号化に使用する既存の証明書または非対称キーの名前。 @encryptor_nameは**SYSNAME**です。 非対称キーを使用する場合は、拡張キー管理 (EKM) を使用して構成する必要があります。 パラメーターに NO_ENCRYPTION を指定した場合、このパラメーターは省略可能です @encryption_algorithm 。  
  
 詳細については、「 [拡張キー管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)」を参照してください。  
  
 @local_cache_path  
 このパラメーターは、まだサポートされていません。  
  
## <a name="return-code-value"></a>リターン コード値  
 0 (成功) または 1 (失敗)  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 **Db_backupoperator**データベースロールのメンバーシップ、 **ALTER ANY CREDENTIAL**権限、および**Sp_delete_backuphistory**ストアドプロシージャに対する**EXECUTE**権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、SQL Server のインスタンスのの詳細な構成オプションを設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] します。  
  
```sql
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_advanced  
                @encryption_algorithm ='AES_128'  
                ,@encryptor_type = 'CERTIFICATE'  
                ,@encryptor_name = 'MyTestDBBackupEncryptCert'  
GO  
```  
  
## <a name="see-also"></a>参照  
 [managed_backup。 sp_backup_config_basic (Transact-sql)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
