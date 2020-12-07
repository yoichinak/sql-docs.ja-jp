---
description: DROP FUNCTION (Transact-SQL)
title: DROP FUNCTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_FUNCTION_TSQL
- DROP FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined functions [SQL Server], removing
- removing user-defined functions
- DROP FUNCTION statement
- dropping user-defined functions
- deleting user-defined functions
ms.assetid: ee5ad283-9e44-4109-902f-0ce12669ee11
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fb975b9fcceedc74f49b951e7ec2a8b947880047
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2020
ms.locfileid: "91380407"
---
# <a name="drop-function-transact-sql"></a>DROP FUNCTION (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  1 つまたは複数のユーザー定義関数を現在のデータベースから削除します。 ユーザー定義関数は [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) を使って作成し、[ALTER FUNCTION](../../t-sql/statements/alter-function-transact-sql.md) を使って変更します。  
  
 DROP 関数では、ネイティブ コンパイル、スカラー ユーザー定義関数をサポートしています。 詳しくは、「[インメモリ OLTP でのユーザー定義のスカラー関数](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)」をご覧ください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
 -- SQL Server, Azure SQL Database 

DROP FUNCTION [ IF EXISTS ] { [ schema_name. ] function_name } [ ,...n ]   
[;]
```

```syntaxsql
 -- Azure Synapse Analytics, Parallel Data Warehouse 

DROP FUNCTION [IF EXISTS] [ schema_name. ] function_name
[;] 
```  
   
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *IF EXISTS*    
 条件付きでは既に存在する場合にのみ、関数を削除します。 [!INCLUDE[ssnoversion_md](../../includes/ssnoversion-md.md)] 2016 以降および [!INCLUDE[sssds_md](../../includes/sssds-md.md)] で使用できます。
  
 *schema_name*  
 ユーザー定義関数が属するスキーマの名前を指定します。  
  
 *function_name*  
 削除するユーザー定義関数の名前です。 スキーマ名の指定は省略可能です。 サーバー名とデータベース名は指定できません。  
  
## <a name="remarks"></a>注釈  
 データベース内に、この関数を参照し SCHEMABINDING を使って作成された [!INCLUDE[tsql](../../includes/tsql-md.md)] 関数またはビューがある場合、または、この関数を参照する計算列、CHECK 制約、DEFAULT 制約がある場合、DROP FUNCTION は失敗します。  
  
 この関数を参照し、インデックスが作成された計算列がある場合、DROP FUNCTION は失敗します。  
  
## <a name="permissions"></a>アクセス許可  
 DROP FUNCTION を実行するには、少なくとも、関数が属するスキーマに対する ALTER 権限、または関数に対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-dropping-a-function"></a>A. 関数を削除する  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] サンプル データベースの `Sales` スキーマから、`fn_SalesByStore` ユーザー定義関数を削除します。 この関数を作成する方法については、「[CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)」の例 B をご覧ください。  
  
```sql  
DROP FUNCTION Sales.fn_SalesByStore;  
```  
  
## <a name="see-also"></a>関連項目  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)  
  
  
