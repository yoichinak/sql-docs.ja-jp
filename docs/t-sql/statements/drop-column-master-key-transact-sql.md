---
description: DROP COLUMN MASTER KEY (Transact-SQL)
title: DROP COLUMN MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP COLUMN MASTER KEY
- DROP_COLUMN_MASTER_KEY_TSQL
- DROP COLUMN MASTER
- DROP_COLUMN_MASTER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_keys catalog view
ms.assetid: fd5e77c8-a3ae-4795-bb46-b322c0500041
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: 1e2b72e3b398f5b79f1467530b589853f7f67781
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2020
ms.locfileid: "91380139"
---
# <a name="drop-column-master-key-transact-sql"></a>DROP COLUMN MASTER KEY (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  データベースから、列のマスター キーを削除します。 これはメタデータの操作です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
DROP COLUMN MASTER KEY key_name;  
```  

## <a name="arguments"></a>引数
 *key_name*  
 列のマスター キーの名前です。  
  
## <a name="remarks"></a>注釈
 列マスター キーできるのは、その列マスター キーを使用して暗号化された列暗号化キー値がない場合に限られます。 列の暗号化キーの値を削除するには、[DROP COLUMN ENCRYPTION KEY](../../t-sql/statements/drop-column-encryption-key-transact-sql.md) ステートメントを使います。  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する **ALTER ANY COLUMN MASTER KEY** 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-dropping-a-column-master-key"></a>A. 列のマスター キーを削除します  
 次の例では、`MyCMK` という名前の列マスター キーを削除します。  
  
```sql  
DROP COLUMN MASTER KEY MyCMK;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [sys.column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [セキュリティで保護されたエンクレーブが設定された Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Always Encrypted のキー管理の概要](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [セキュリティで保護されたエンクレーブが設定された Always Encrypted のキーを管理する](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
  
  
