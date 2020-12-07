---
title: TDE で保護されたデータベースの復元
description: 次の手順を使用して、Analytics Platform System Parallel Data Warehouse での transparent data encryption を使用して暗号化されたデータベースを復元します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: bfd345ff4f55311de41140d5675809838eb06297
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766721"
---
# <a name="restore-a-database-protected-by-tde-in-parallel-data-warehouse"></a>Parallel Data Warehouse で TDE によって保護されているデータベースを復元する
Transparent data encryption を使用して暗号化されたデータベースを復元するには、次の手順に従います。  
  
[Transparent Data Encryption の使用](transparent-data-encryption.md#using-tde)例には、データベースで tde を有効にするコードが含まれてい `AdventureWorksPDW2012` ます。 次のコードでは、元の Analytics Platform System (APS) アプライアンスでデータベースのバックアップを作成し、証明書とデータベースを別のアプライアンスに復元することによって、この例を続けています。  
  
最初の手順では、ソースデータベースのバックアップを作成します。  
  
```sql  
BACKUP DATABASE AdventureWorksPDW2012   
TO DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
マスターキーを作成し、暗号化を有効にし、ネットワーク資格情報を作成することによって、TDE の新しい SQL Server PDW を準備します。  
  
```sql  
USE master;  
GO  
  
-- Create a database master key in the master database  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';  
GO  
  
-- Enable encryption for PDW  
EXEC sp_pdw_database_encryption 1;  
GO  
  
EXEC sp_pdw_add_network_credentials 'SECURE_SERVER', '<domain>\<Windows_user>', '<password>';  
```  
  
最後の2つの手順では、元の SQL Server PDW からのバックアップを使用して証明書を再作成します。 証明書のバックアップを作成したときに使用したパスワードを使用します。  
  
```sql  
-- Create certificate in master  
CREATE CERTIFICATE MyServerCert  
    FROM FILE = '\\SECURE_SERVER\cert\MyServerCert.cer'   
    WITH PRIVATE KEY (FILE = '\\SECURE_SERVER\cert\MyServerCert.key',   
    DECRYPTION BY PASSWORD = '<password>');  
  
RESTORE DATABASE AdventureWorksPDW2012   
    FROM DISK = '\\SECURE_SERVER\Backups\AdventureWorksPDW2012';  
```  
  
## <a name="see-also"></a>参照  
[BACKUP DATABASE](../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016)  
[マスターキー](../t-sql/statements/create-master-key-transact-sql.md)  
 の作成[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
[sp_pdw_database_encryption](../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
[CREATE CERTIFICATE](../t-sql/statements/create-certificate-transact-sql.md)  
[データベースの復元](../t-sql/statements/restore-statements-transact-sql.md?view=aps-pdw-2016)
