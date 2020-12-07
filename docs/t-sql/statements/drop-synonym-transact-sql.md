---
description: DROP SYNONYM (Transact-SQL)
title: DROP SYNONYM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SYNONYM
- DROP_SYNONYM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting synonyms
- synonyms [SQL Server], removing
- removing synonyms
- DROP SYNONYM statement
- dropping synonyms
ms.assetid: 23578932-e4de-4c39-a5a0-ce45139c4269
author: markingmyname
ms.author: maghan
ms.openlocfilehash: af16b7921358a12b87e9ab2ddbd6acaefee47d13
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379664"
---
# <a name="drop-synonym-transact-sql"></a>DROP SYNONYM (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  指定されたスキーマからシノニムを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
DROP SYNONYM [ IF EXISTS ] [ schema. ] synonym_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *IF EXISTS*  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)
  
 条件付きでは既に存在する場合にのみ、シノニムを削除します。  
  
 *schema*  
 シノニムが存在するスキーマを指定します。 スキーマを指定しない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって現在のユーザーの既定のスキーマが使用されます。  
  
 *synonym_name*  
 削除するシノニムの名前です。  
  
## <a name="remarks"></a>注釈  
 シノニムへの参照はスキーマにバインドされていません。したがってシノニムはいつでも削除できます。 削除したシノニムへの参照は、実行時にのみ検出されます。  
  
 シノニムは、動的な SQL で作成、削除、参照することができます。  
  
## <a name="permissions"></a>アクセス許可  
 シノニムを削除するには、ユーザーは次の条件を少なくとも 1 つ 満たしている必要があります。  
  
-   シノニムの現在の所有者である。  
  
-   シノニムに対する CONTROL を許可されている。  
  
-   シノニムを含むスキーマに対する ALTER SCHEMA 権限を許可されている。  
  
## <a name="examples"></a>例  
 次の例では、まずシノニム `MyProduct` を作成し、その後シノニムを削除します。  
  
```sql  
USE tempdb;  
GO  
-- Create a synonym for the Product table in AdventureWorks2012.  
CREATE SYNONYM MyProduct  
FOR AdventureWorks2012.Production.Product;  
GO  
-- Drop synonym MyProduct.  
USE tempdb;  
GO  
DROP SYNONYM MyProduct;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
