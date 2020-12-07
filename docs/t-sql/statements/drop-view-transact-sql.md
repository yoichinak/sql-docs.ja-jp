---
description: DROP VIEW (Transact-SQL)
title: DROP VIEW (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_VIEW_TSQL
- DROP VIEW
dev_langs:
- TSQL
helpviewer_keywords:
- dropping views
- DROP VIEW statement
- deleting views
- indexed views [SQL Server], removing
- views [SQL Server], removing
- removing views
ms.assetid: 03cea355-e39c-46e1-b7db-8832038669dd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 21dd4a4aac028f06d6c4f8902d7d7ec93a87e083
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990093"
---
# <a name="drop-view-transact-sql"></a>DROP VIEW (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  1 つまたは複数のビューを現在のデータベースから削除します。 DROP VIEW は、インデックス付きビューに対して実行できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
-- Syntax for SQL Server, Azure SQL Database, and Azure Synapse Analytics
  
DROP VIEW [ IF EXISTS ] [ schema_name . ] view_name [ ...,n ] [ ; ]  
```  
  
```syntaxsql
-- Syntax for Parallel Data Warehouse  
  
DROP VIEW [ schema_name . ] view_name [ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *IF EXISTS*  
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで、[!INCLUDE[sssds](../../includes/sssds-md.md)])。|  
  
 条件付きでは既に存在する場合にのみ、ビューを削除します。  
  
 *schema_name*  
 ビューが所属するスキーマの名前を指定します。  
  
 *view_name*  
 削除するビューの名前を指定します。  
  
## <a name="remarks"></a>注釈  
 ビューを削除すると、ビューの定義やビューに関するその他の情報がシステム カタログから削除されます。 ビューに対する権限もすべて削除されます。  
  
 DROP TABLE を使用して削除されたテーブルのすべてのビューは、DROP VIEW を使用して明示的に削除する必要があります。  
  
 DROP VIEW をインデックス付きビューに対して実行すると、ビューのすべてのインデックスが自動的に削除されます。 ビューのすべてのインデックスを表示するには、[sp_helpindex](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md) を使います。  
  
 ビューからクエリを実行すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では、ステートメントで参照されているデータベース オブジェクトがすべて存在すること、データベース オブジェクトがステートメントのコンテキストで有効であること、およびデータ変更ステートメントがデータの整合性規則に違反していないことが確認されます。 確認に失敗すると、エラー メッセージが返されます。 確認に成功すると、そのアクションが、基になるテーブルに対するアクションに変換されます。 ビューが作成された後で基になるテーブルやビューが変更された場合は、ビューを削除して再作成することが適切な場合があります。  
  
 特定のビューの依存関係を確認する方法について詳しくは、「[sys.sql_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)」をご覧ください。  
  
 ビューのテキストを表示する方法について詳しくは、「[sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)」をご覧ください。  
  
## <a name="permissions"></a>アクセス許可  
 ビューの **CONTROL** 権限、ビューを含んでいるスキーマの **ALTER** 権限、または **db_ddladmin** 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-drop-a-view"></a>A. ビューを削除する  
 次の例では、ビュー `Reorder` を削除します。  
  
```sql
DROP VIEW IF EXISTS dbo.Reorder ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
 
