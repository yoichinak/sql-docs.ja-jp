---
description: DROP CERTIFICATE (Transact-SQL)
title: DROP CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/18/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP CERTIFICATE
- DROP_CERTIFICATE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- certificates [SQL Server], removing
- removing certificates
- dropping certificates
- DROP CERTIFICATE statement
- deleting certificates
ms.assetid: 5704aa04-68a3-4b29-b62b-8868af487817
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 63c58c8528929c3a90a289f99d793a6fb91f4112
ms.sourcegitcommit: 894c1a23e922dc29b82c1d2c34c7b0ff28b38654
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93067486"
---
# <a name="drop-certificate-transact-sql"></a>DROP CERTIFICATE (Transact-SQL)
[!INCLUDE [sql-asdb-asa-pdw](../../includes/applies-to-version/sql-asdb-asa-pdw.md)]

  データベースから証明書を削除します。  
  
> [!IMPORTANT]  
>  データベースの暗号化に使用された証明書のバックアップは、データベースで暗号化を無効にした後も保持しておく必要があります。 データベースが暗号化されなくなっても、トランザクション ログの一部はまだ保護されたままの場合があるため、データベースの完全バックアップが実行されるまでは、一部の操作で証明書が必要になることがあります。 証明書は、データベースが暗号化されていたときに作成されたバックアップから復元する場合にも必要です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md) 

  
> [!Note]
> [!INCLUDE [Synapse preview note](../../includes/synapse-preview-note.md)]
  
## <a name="syntax"></a>構文  
  
```synaxsql  
DROP CERTIFICATE certificate_name  
```  
[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *certificate_name*  
 データベースに認識される証明書の一意な名前を指定します。  
  
## <a name="remarks"></a>注釈  
 エンティティが関連付けられていない場合にのみ、証明書は削除できます。  
  
## <a name="permissions"></a>アクセス許可  
 証明書に対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、証明書 `Shipping04` をデータベース `AdventureWorks` から削除します。  
  
```sql  
USE AdventureWorks2012;  
DROP CERTIFICATE Shipping04;  
```  
  
## <a name="examples-sspdw"></a>例: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 次の例では、証明書 `Shipping04` を削除します。  
  
```sql
USE master;  
DROP CERTIFICATE Shipping04;  
```  
  
## <a name="see-also"></a>参照  
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
