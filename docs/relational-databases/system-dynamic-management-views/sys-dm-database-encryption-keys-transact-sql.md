---
description: sys.dm_database_encryption_keys (Transact-SQL)
title: sys.dm_database_encryption_keys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_database_encryption_keys
- sys.dm_database_encryption_keys_TSQL
- dm_database_encryption_keys
- dm_database_encryption_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_database_encryption_keys dynamic management view
ms.assetid: 56fee8f3-06eb-4fff-969e-abeaa0c4b8e4
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b876db6159985e600536439f587004b33fd6fc6f
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834285"
---
# <a name="sysdm_database_encryption_keys-transact-sql"></a>sys.dm_database_encryption_keys (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  データベースの暗号化の状態と、それに関連付けられているデータベース暗号化キーに関する情報を返します。 データベース暗号化の詳細については、「[Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)」を参照してください。  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|database_id|**int**|データベースの ID です。|  
|encryption_state|**int**|データベースが暗号化されているかどうかを示します。<br /><br /> 0 = データベース暗号化キーは存在しません。暗号化は行われません。<br /><br /> 1 = 暗号化されていない<br /><br /> 2 = 暗号化が進行中<br /><br /> 3 = 暗号化<br /><br /> 4 = キーの変更中<br /><br /> 5 = 暗号化解除中<br /><br /> 6 = 保護の変更中 (データベース暗号化キーを暗号化する証明書または非対称キーが変更されています)|  
|create_date|**datetime**|暗号化キーが作成された日付 (UTC) が表示されます。|  
|regenerate_date|**datetime**|暗号化キーが再生成された日付 (UTC) が表示されます。|  
|modify_date|**datetime**|暗号化キーが変更された日付 (UTC) が表示されます。|  
|set_date|**datetime**|暗号化キーがデータベースに適用された日付 (UTC) が表示されます。|  
|opened_date|**datetime**|データベースキーが最後に開かれた日時を示します。|  
|key_algorithm|**nvarchar(32)**|キーに使用されるアルゴリズムが表示されます。|  
|key_length|**int**|キーの長さを表示します。|  
|encryptor_thumbprint|**varbinary(20)**|暗号化のサムプリントを表示します。|  
|encryptor_type|**nvarchar(32)**|**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [現在のバージョン](../../sql-server/what-s-new-in-sql-server-2016.md)まで)。<br /><br /> 暗号化機能について説明します。|  
|percent_complete|**real**|データベース暗号化状態の変更の完了率。 状態の変更がない場合、これは0になります。|
|encryption_state_desc|**nvarchar(32)**|**適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。<br><br> データベースが暗号化されているか、暗号化されていないかを示す文字列。<br><br>NONE<br><br>暗号化<br><br>暗号<br><br>DECRYPTION_IN_PROGRESS<br><br>ENCRYPTION_IN_PROGRESS<br><br>KEY_CHANGE_IN_PROGRESS<br><br>PROTECTION_CHANGE_IN_PROGRESS|
|encryption_scan_state|**int**|**適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。<br><br>暗号化スキャンの現在の状態を示します。 <br><br>0 = スキャンが開始されていません。 TDE が有効になっていません。<br><br>1 = スキャンが進行中です。<br><br>2 = スキャンは実行中ですが、中断されているため、ユーザーは再開できます。<br><br>3 = 何らかの理由でスキャンが中止されました。手動介入が必要です。 詳細については、Microsoft サポートにお問い合わせください。<br><br>4 = スキャンが正常に完了し、TDE が有効になり、暗号化が完了しました。|
|encryption_scan_state_desc|**nvarchar(32)**|**適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。<br><br>暗号化スキャンの現在の状態を示す文字列。<br><br> NONE<br><br>RUNNING<br><br>SUSPENDED<br><br>ABORTED<br><br>完了|
|encryption_scan_modify_date|**datetime**|**適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。<br><br> 暗号化スキャンの状態が最後に変更された日付 (UTC) が表示されます。|
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="see-also"></a>参照  

 [セキュリティ関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [透過的なデータ暗号化 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server の暗号化](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL Server とデータベースの暗号化キー &#40;データベース エンジン&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
