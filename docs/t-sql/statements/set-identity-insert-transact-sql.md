---
title: SET IDENTITY_INSERT (Transact-SQL) | Microsoft Docs
description: SET IDENTITY_INSERT ステートメントの Transact-SQL リファレンス。 ON に設定すると、テーブルの ID 列に明示的な値を挿入することが許可されます。
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET IDENTITY_INSERT
- SET_IDENTITY_INSERT_TSQL
- IDENTITY_INSERT_TSQL
- IDENTITY_INSERT
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY_INSERT option
- SET IDENTITY_INSERT statement
- identity values [SQL Server], explicit values
- identity columns [SQL Server], explicit values
ms.assetid: a5dd49f2-45c7-44a8-b182-e0a5e5c373ee
author: markingmyname
ms.author: maghan
monkerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||=azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: 08c8fd59e702d668f7218757021f415b0bea3e39
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544252"
---
# <a name="set-identity_insert-transact-sql"></a>SET IDENTITY_INSERT (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

テーブルの ID 列に明示的な値を追加することを許可します。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
  
SET IDENTITY_INSERT [ [ database_name . ] schema_name . ] table_name { ON | OFF }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *database_name*  
 指定したテーブルが含まれているデータベースの名前を指定します。  
  
 *schema_name*  
 テーブルが所属するスキーマの名前を指定します。  
  
 *table_name*  
 ID 列があるテーブルの名前です。  
  
## <a name="remarks"></a>解説  
 いかなる場合も、IDENTITY_INSERT プロパティを ON に設定できるのはセッション内の 1 つのテーブルのみです。 1 つのテーブルで既にこのプロパティが ON に設定されている状態で、別のテーブルに対して SET IDENTITY_INSERT ON ステートメントを実行すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では SET IDENTITY_INSERT が既に ON であるというエラー メッセージが返され、このプロパティが ON に設定されているテーブルがレポートされます。  
  
 挿入する値がテーブルの現在の ID 値よりも大きい場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では新しく挿入された値が現在の ID 値として自動的に使用されます。  
  
 SET IDENTITY_INSERT は、解析時ではなく実行時に設定されます。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーはテーブルを所有しているか、テーブルに対する ALTER 権限を持っている必要があります。  
  
## <a name="examples"></a>例  
 次の例では、ID 列を含むテーブルを作成した後、`SET IDENTITY_INSERT` ステートメントによって ID 値に発生したギャップを、`DELETE` の設定を使用して調整しています。  
  
```sql
USE AdventureWorks2012;  
GO  
-- Create tool table.  
CREATE TABLE dbo.Tool(  
   ID INT IDENTITY NOT NULL PRIMARY KEY,   
   Name VARCHAR(40) NOT NULL  
);  
GO  
-- Inserting values into products table.  
INSERT INTO dbo.Tool(Name)   
VALUES ('Screwdriver')  
        , ('Hammer')  
        , ('Saw')  
        , ('Shovel');  
GO  
  
-- Create a gap in the identity values.  
DELETE dbo.Tool  
WHERE Name = 'Saw';  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
  
-- Try to insert an explicit ID value of 3;  
-- should return an error:
-- An explicit value for the identity column in table 'AdventureWorks2012.dbo.Tool' can only be specified when a column list is used and IDENTITY_INSERT is ON.
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
-- SET IDENTITY_INSERT to ON.  
SET IDENTITY_INSERT dbo.Tool ON;  
GO  
  
-- Try to insert an explicit ID value of 3.  
INSERT INTO dbo.Tool (ID, Name) VALUES (3, 'Garden shovel');  
GO  
  
SELECT *   
FROM dbo.Tool;  
GO  
-- Drop products table.  
DROP TABLE dbo.Tool;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENTITY &#40;Property&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
