---
description: SQL Server システム カタログに対するクエリに関してよく寄せられる質問
title: SQL Server システムカタログに対するクエリについてよく寄せられる質問 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- catalog views [SQL Server], examples
- metadata [SQL Server], frequently asked questions
- metadata [SQL Server], example queries
- system catalogs [SQL Server], example queries
- catalog views [SQL Server], frequently asked questions
ms.assetid: ca202580-c37e-4ccd-9275-77ce79481f64
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 346ae709b81c1d5f3892a7e7b5acfd98c3ff7d3b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539787"
---
# <a name="querying-the-sql-server-system-catalog-faq"></a>SQL Server システム カタログに対するクエリに関してよく寄せられる質問
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  このトピックには、よく寄せられる質問の一覧が含まれています。 これらの質問に対する答えは、カタログビューに基づくクエリです。  
  
##  <a name="frequently-asked-questions"></a><a name="_TOP"></a> よく寄せられる質問  
 以下のセクションでは、よく寄せられる質問をカテゴリ別に示します。  
  
### <a name="data-types"></a>データの種類  
  
-   [指定されたテーブルの列のデータ型を検索操作方法には、](#_FAQ7)  
  
-   [指定されたテーブルの LOB データ型を検索操作方法には](#_FAQ14)  
  
-   [指定されたデータ型に依存する列を見つけるにはどのようにすればよいですか。](#_FAQ22)  
  
-   [指定された CLR ユーザー定義型または別名データ型に依存する計算列を見つけるにはどのようにすればよいですか。](#_FAQ23)  
  
-   [指定された CLR ユーザー定義型または別名型に依存するパラメーターを検索操作方法には](#_FAQ24)  
  
-   [指定された CLR ユーザー定義型に依存する CHECK 制約を検索操作方法には、](#_FAQ25)  
  
-   [指定された CLR ユーザー定義型または別名データ型に依存するビュー、Transact-SQL 関数、Transact-SQL ストアド プロシージャを見つけるにはどのようにすればよいですか。](#_FAQ26)  
  
### <a name="tables-indexes-views-and-constraints"></a>テーブル、インデックス、ビュー、および制約  
  
-   [指定されたデータベースでユーザー定義型のテーブルをすべて見つけるにはどのようにすればよいですか。](#_FAQ31)  
  
-   [指定したデータベース中でクラスター化インデックスを持たないテーブルをすべて見つけるにはどのようにすればよいですか。](#_FAQ1)  
  
-   [インデックスを持たないすべてのテーブルを検索操作方法には](#_FAQ4)  
  
-   [主キーを持たないすべてのテーブルを見つけるにはどのようにすればよいですか。](#_FAQ3)  
  
-   [Id 列を含むすべてのテーブルを検索操作方法には、](#_FAQ5)  
  
-   [パーティション分割されたテーブルとインデックスをすべて見つけるにはどのようにすればよいですか。](#_FAQ32)  
  
-   [データベース内のすべてのビューを見つけるにはどのようにすればよいですか。](#_FAQ13)  
  
-   [ビューの定義を見つけるにはどのようにすればよいですか。](#_FAQ35)  
  
-   [過去 n 日間に変更されたすべてのエンティティを見つけるにはどのようにすればよいですか。](#_FAQ6)  
  
-   [指定されたテーブルの主キーの列を検索操作方法には、次のようにします。](#_FAQ16)  
  
-   [指定されたテーブルの外部キーの列を検索操作方法には](#_FAQ17)  
  
-   [計算列の式で使われている列を判断するにはどのようにすればよいですか。](#_FAQ20)  
  
-   [計算列の式で使用されているすべての列を検索操作方法には、](#_FAQ21)  
  
-   [指定されたテーブルのすべての制約を検索操作方法には](#_FAQ27)  
  
-   [指定されたテーブルのインデックスをすべて見つけるにはどのようにすればよいですか。](#_FAQ28)  
  
-   [指定された列名を持つすべてのテーブルを検索操作方法には](#_FAQ30)  
  
-   [指定されたオブジェクトの統計情報をすべて見つけるにはどのようにすればよいですか。](#_FAQ33)  
  
-   [指定されたオブジェクトのすべての統計列と統計列を検索操作方法には](#_FAQ34)  
  
### <a name="modules-stored-procedures-user-defined-functions-and-triggers"></a>モジュール (ストアド プロシージャ、ユーザー定義関数、およびトリガー)  
  
-   [データベース内のすべてのストアドプロシージャを検索操作方法には、](#_FAQ9)  
  
-   [データベース内のすべてのユーザー定義関数を検索操作方法には](#_FAQ12)  
  
-   [指定されたストアドプロシージャまたは関数のパラメーターを検索操作方法には](#_FAQ10)  
  
-   [指定した関数に対する依存関係を知るにはどのようにすればよいですか。](#_FAQ8)  
  
-   [モジュールの定義を表示操作方法には](#_FAQ15)  
  
-   [サーバー レベルのトリガーの定義を表示するにはどのようにすればよいですか。](#_FAQ19)  
  
### <a name="schemas-users-roles-and-permissions"></a>スキーマ、ユーザー、ロール、およびアクセス許可  
  
-   [指定したスキーマに含まれるエンティティのすべての所有者を検索操作方法には、](#_FAQ2)  
  
-   [指定されたプリンシパルに付与または定義された権限を見つけるにはどのようにすればよいですか。](#_FAQ18)  
  
## <a name="answers"></a>回答  
  
###  <a name="how-do-i-find-all-the-tables-that-do-not-have-a-clustered-index-in-a-specified-database"></a><a name="_FAQ1"></a> 指定されたデータベースにクラスター化インデックスがないすべてのテーブルを検索操作方法には、  
 次のクエリを実行する前に、を `<database_name>` 有効なデータベース名に置き換えます。  
  
```  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name, t.name AS table_name  
FROM sys.tables AS t  
WHERE NOT EXISTS   
   (  
     SELECT * FROM sys.indexes AS i  
     WHERE i.object_id = t.object_id  
     AND i.type = 1  -- or type_desc = 'CLUSTERED'  
   )  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 または、 `OBJECTPROPERTY` 次の例に示すように、関数を使用することもできます。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name, name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasClustIndex') = 0  
ORDER BY schema_id, name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-owners-of-entities-contained-in-a-specified-schema"></a><a name="_FAQ2"></a> 指定したスキーマに含まれるエンティティのすべての所有者を検索操作方法には、  
 次のクエリを実行する前に、 `<database_name>` とを `<schema_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT 'OBJECT' AS entity_type  
    ,USER_NAME(OBJECTPROPERTY(object_id, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.objects WHERE SCHEMA_NAME(schema_id) = '<schema_name>'  
UNION   
SELECT 'TYPE' AS entity_type  
    ,USER_NAME(TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId')) AS owner_name  
    ,name   
FROM sys.types WHERE SCHEMA_NAME(schema_id) = '<schema_name>'   
UNION  
SELECT 'XML SCHEMA COLLECTION' AS entity_type   
    ,COALESCE(USER_NAME(xsc.principal_id),USER_NAME(s.principal_id)) AS owner_name  
    ,xsc.name   
FROM sys.xml_schema_collections AS xsc JOIN sys.schemas AS s  
    ON s.schema_id = xsc.schema_id  
WHERE s.name = '<schema_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-tables-that-do-not-have-a-primary-key"></a><a name="_FAQ3"></a> 主キーを持たないすべてのテーブルを検索操作方法には  
 次のクエリを実行する前に、を `<database_name>` 有効なデータベース名に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(t.schema_id) AS schema_name  
    ,t.name AS table_name  
FROM sys.tables t   
WHERE object_id NOT IN   
   (  
    SELECT parent_object_id   
    FROM sys.key_constraints   
    WHERE type_desc = 'PRIMARY_KEY_CONSTRAINT' -- or type = 'PK'  
    );  
GO  
  
```  
  
 または、次のクエリを実行することもできます。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasPrimaryKey') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-tables-that-do-not-have-an-index"></a><a name="_FAQ4"></a> インデックスを持たないすべてのテーブルを検索操作方法には  
 次のクエリを実行する前に、を `<database_name>` 有効なデータベース名に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name  
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'IsIndexed') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-tables-that-have-an-identity-column"></a><a name="_FAQ5"></a> Id 列を含むすべてのテーブルを検索操作方法には、  
 次のクエリを実行する前に、を `<database_name>` 有効なデータベース名に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    , t.name AS table_name  
    , c.name AS column_name  
FROM sys.tables AS t  
JOIN sys.identity_columns c ON t.object_id = c.object_id  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 または、次のクエリを実行することもできます。  
  
> [!NOTE]  
>  このクエリでは、列の名前は返されません。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasIdentity') = 1  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-data-types-of-the-columns-of-a-specified-table"></a><a name="_FAQ7"></a> 指定されたテーブルの列のデータ型を検索操作方法には、  
 次のクエリを実行する前に、 `<database_name>` とを `<schema_name.table_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT c.name AS column_name  
    ,c.column_id  
    ,SCHEMA_NAME(t.schema_id) AS type_schema  
    ,t.name AS type_name  
    ,t.is_user_defined  
    ,t.is_assembly_type  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
FROM sys.columns AS c   
JOIN sys.types AS t ON c.user_type_id=t.user_type_id  
WHERE c.object_id = OBJECT_ID('<schema_name.table_name>')  
ORDER BY c.column_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-dependencies-on-a-specified-function"></a><a name="_FAQ8"></a> 指定された関数の依存関係を検索操作方法には  
 次のクエリを実行する前に、 `<database_name>` とを `<schema_name.function_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS referencing_object_name  
    ,COALESCE(COL_NAME(object_id, column_id), '(n/a)') AS referencing_column_name  
    ,*  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.function_name>')  
ORDER BY OBJECT_NAME(object_id), COL_NAME(object_id, column_id);  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-stored-procedures-in-a-database"></a><a name="_FAQ9"></a> データベース内のすべてのストアドプロシージャを検索操作方法には、  
 次のクエリを実行する前に、を `<database_name>` 有効な名前に置き換えます。  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS procedure_name   
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
FROM sys.procedures;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-parameters-for-a-specified-stored-procedure-or-function"></a><a name="_FAQ10"></a> 指定されたストアドプロシージャまたは関数のパラメーターを検索操作方法には  
 次のクエリを実行する前に、 `<database_name>` とを `<schema_name.object_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,o.name AS object_name  
    ,o.type_desc  
    ,p.parameter_id  
    ,p.name AS parameter_name  
    ,TYPE_NAME(p.user_type_id) AS parameter_type  
    ,p.max_length  
    ,p.precision  
    ,p.scale  
    ,p.is_output  
FROM sys.objects AS o  
INNER JOIN sys.parameters AS p ON o.object_id = p.object_id  
WHERE o.object_id = OBJECT_ID('<schema_name.object_name>')  
ORDER BY schema_name, object_name, p.parameter_id;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-user-defined-functions-in-a-database"></a><a name="_FAQ12"></a> データベース内のすべてのユーザー定義関数を検索操作方法には  
 次のクエリを実行する前に、を `<database_name>` 有効なデータベース名に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT name AS function_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE type_desc LIKE '%FUNCTION%';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-views-in-a-database"></a><a name="_FAQ13"></a> データベース内のすべてのビューを検索操作方法には  
 次のクエリを実行する前に、を `<database_name>` 有効なデータベース名に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT name AS view_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,OBJECTPROPERTYEX(object_id,'IsIndexed') AS IsIndexed  
  ,OBJECTPROPERTYEX(object_id,'IsIndexable') AS IsIndexable  
  ,create_date  
  ,modify_date  
FROM sys.views;  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-entities-that-have-been-modified-in-the-last-n-days"></a><a name="_FAQ6"></a> 過去 N 日間に変更されたすべてのエンティティを検索操作方法には、  
 次のクエリの `<database_name>` と `<n_days>` を有効な値に置き換えてから、クエリを実行します。  
  
```  
USE <database_name>;  
GO  
SELECT name AS object_name   
  ,SCHEMA_NAME(schema_id) AS schema_name  
  ,type_desc  
  ,create_date  
  ,modify_date  
FROM sys.objects  
WHERE modify_date > GETDATE() - <n_days>  
ORDER BY modify_date;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-lob-data-types-of-a-specified-table"></a><a name="_FAQ14"></a> 指定されたテーブルの LOB データ型を検索操作方法には  
 次のクエリを実行する前に、 `<database_name>` とを `<schema_name.table_name>` 有効な名前に置き換えます。  
  
```  
  
USE <database_name>;  
GO  
SELECT name AS column_name   
    ,column_id   
    ,TYPE_NAME(user_type_id) AS type_name  
    ,max_length  
    ,CASE   
       WHEN max_length = -1 AND TYPE_NAME(user_type_id) <> 'xml'  
            THEN 1  
            ELSE 0  
     END AS [(max)]  
FROM sys.columns  
WHERE object_id=OBJECT_ID('<schema_name.table_name>')   
    AND ( TYPE_NAME(user_type_id) IN ('xml','text', 'ntext','image')  
         OR (TYPE_NAME(user_type_id) IN ('varchar','nvarchar','varbinary')  
         AND max_length = -1)  
        );  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-view-the-definition-of-a-module"></a><a name="_FAQ15"></a> モジュールの定義を表示操作方法には  
 次のクエリを実行する前に、 `<database_name>` とを `<schema_name.object_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 または、 `OBJECT_DEFINITION` 次の例に示すように、関数を使用することもできます。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-view-the-definition-of-a-server-level-trigger"></a><a name="_FAQ19"></a> サーバーレベルのトリガーの定義を表示操作方法には  
  
```  
SELECT definition  
FROM sys.server_sql_modules;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-columns-of-a-primary-key-for-a-specified-table"></a><a name="_FAQ16"></a> 指定されたテーブルの主キーの列を検索操作方法には、次のようにします。  
 次のクエリを実行する前に、 `<database_name>` とを `<schema_name.table_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,ic.index_column_id  
    ,key_ordinal  
    ,c.name AS column_name  
    ,TYPE_NAME(c.user_type_id)AS column_type   
    ,is_identity  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
INNER JOIN sys.columns AS c   
    ON ic.object_id = c.object_id AND c.column_id = ic.column_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 または、 `COL_NAME` 次の例に示すように、関数を使用することもできます。  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,key_ordinal  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic   
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.is_primary_key = 1   
    AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-columns-of-a-foreign-key-for-a-specified-table"></a><a name="_FAQ17"></a> 指定されたテーブルの外部キーの列を検索操作方法には  
 次のクエリを実行する前に、 `<database_name>` とを `<schema_name.table_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT   
    f.name AS foreign_key_name  
   ,OBJECT_NAME(f.parent_object_id) AS table_name  
   ,COL_NAME(fc.parent_object_id, fc.parent_column_id) AS constraint_column_name  
   ,OBJECT_NAME (f.referenced_object_id) AS referenced_object  
   ,COL_NAME(fc.referenced_object_id, fc.referenced_column_id) AS referenced_column_name  
   ,is_disabled  
   ,delete_referential_action_desc  
   ,update_referential_action_desc  
FROM sys.foreign_keys AS f  
INNER JOIN sys.foreign_key_columns AS fc   
   ON f.object_id = fc.constraint_object_id   
WHERE f.parent_object_id = OBJECT_ID('<schema_name.table_name>');  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-permissions-granted-or-denied-to-a-specified-principal"></a><a name="_FAQ18"></a> 指定したプリンシパルに対して許可または拒否されたアクセス許可を検索操作方法には  
 次の例では、アクセス許可がチェックされるエンティティの名前を返す関数を作成します。 関数は、次のクエリで呼び出されます。 この関数は権限を確認する各データベースに作成する必要があります。  
  
```  
-- Create a function to return the name of the entity on which the permissions are checked.  
IF OBJECT_ID (N'dbo.entity_instance_name', N'FN') IS NOT NULL  
    DROP FUNCTION dbo.entity_instance_name;  
GO  
CREATE FUNCTION dbo.entity_instance_name(@class_desc nvarchar(60), @major_id int)   
RETURNS sysname AS  
BEGIN  
    DECLARE @the_entity_name sysname  
    SELECT @the_entity_name = CASE  
        WHEN @class_desc = 'DATABASE' THEN DB_NAME()  
        WHEN @class_desc = 'SCHEMA' THEN SCHEMA_NAME(@major_id)  
        WHEN @class_desc = 'OBJECT_OR_COLUMN' THEN OBJECT_NAME(@major_id)  
        WHEN @class_desc = 'DATABASE_PRINCIPAL' THEN USER_NAME(@major_id)  
        WHEN @class_desc = 'ASSEMBLY' THEN   
            (SELECT name FROM sys.assemblies WHERE assembly_id=@major_id)  
        WHEN @class_desc = 'TYPE' THEN TYPE_NAME(@major_id)  
        WHEN @class_desc = 'XML_SCHEMA_COLLECTION' THEN   
            (SELECT name FROM sys.xml_schema_collections  
              WHERE xml_collection_id=@major_id)  
        WHEN @class_desc = 'MESSAGE_TYPE' THEN   
            (SELECT name FROM sys.service_message_types WHERE message_type_id=@major_id)  
        WHEN @class_desc = 'SERVICE_CONTRACT' THEN   
           (SELECT name FROM sys.service_contracts  
              WHERE service_contract_id=@major_id)  
        WHEN @class_desc = 'SERVICE' THEN  
          (SELECT name FROM sys.services WHERE service_id=@major_id)  
        WHEN @class_desc = 'REMOTE_SERVICE_BINDING' THEN  
          (SELECT name FROM sys.remote_service_bindings  
             WHERE remote_service_binding_id=@major_id)  
        WHEN @class_desc = 'ROUTE' THEN  
          (SELECT name FROM sys.routes WHERE route_id=@major_id)  
        WHEN @class_desc = 'FULLTEXT_CATALOG' THEN  
          (SELECT name FROM sys.fulltext_catalogs WHERE fulltext_catalog_id=@major_id)  
        WHEN @class_desc = 'SYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.symmetric_keys WHERE symmetric_key_id=@major_id)  
        WHEN @class_desc = 'CERTIFICATE' THEN  
          (SELECT name FROM sys.certificates WHERE certificate_id=@major_id)  
        WHEN @class_desc = 'ASYMMETRIC_KEY' THEN  
          (SELECT name FROM sys.asymmetric_keys WHERE asymmetric_key_id=@major_id)  
        WHEN @class_desc = 'SERVER' THEN   
             (SELECT name FROM sys.servers WHERE server_id=@major_id)  
        WHEN @class_desc = 'SERVER_PRINCIPAL' THEN SUSER_NAME(@major_id)  
        WHEN @class_desc = 'ENDPOINT' THEN   
             (SELECT name FROM sys.endpoints WHERE endpoint_id=@major_id)        
        ELSE '?'  
    END  
    RETURN @the_entity_name  
END;  
GO  
-- Return server-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc, major_id) AS entity_name   
    ,minor_id  
    ,SUSER_NAME(grantee_principal_id) AS grantee  
    ,SUSER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc   
FROM sys.server_permissions   
WHERE grantee_principal_id = SUSER_ID('public');  
GO  
-- Return database-level permissions for the user.  
SELECT class  
    ,class_desc  
    ,dbo.entity_instance_name(class_desc , major_id) AS entity_name   
    ,minor_id  
    ,USER_NAME(grantee_principal_id) AS grantee  
    ,USER_NAME(grantor_principal_id) AS grantor  
    ,type  
    ,permission_name  
    ,state_desc     
FROM  sys.database_permissions   
WHERE grantee_principal_id = DATABASE_PRINCIPAL_ID('public');  
GO  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-determine-if-a-column-is-used-in-a-computed-column-expression"></a><a name="_FAQ20"></a> 列が計算列の式で使用されているかどうかを判断操作方法には  
 次のクエリを実行する前に、、、 `<database_name>` `<schema_name.table_name>` および `<column_name`> を有効な名前に置き換えてください。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS computed_column   
    ,class_desc  
    ,is_selected  
    ,is_updated  
    ,is_select_all  
FROM sys.sql_dependencies  
WHERE referenced_major_id = OBJECT_ID('<schema_name.table_name>')  
    AND referenced_minor_id = COLUMNPROPERTY(referenced_major_id, '<column_name>', 'ColumnId')  
    AND class = 1;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-columns-that-are-used-in-a-computed-column-expression"></a><a name="_FAQ21"></a> 計算列の式で使用されているすべての列を検索操作方法には、  
 次のクエリを実行する前に、を `<database_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(d.referenced_major_id) AS object_name  
    ,COL_NAME(d.referenced_major_id, d.referenced_minor_id) AS column_name  
    ,OBJECT_NAME(referenced_major_id) AS dependent_object_name   
    ,COL_NAME(d.object_id, d.column_id) AS dependent_computed_column  
    ,cc.definition AS computed_column_definition  
FROM sys.sql_dependencies AS d  
JOIN sys.computed_columns AS cc   
    ON cc.object_id = d.object_id AND cc.column_id = d.column_id AND d.object_id=d.referenced_major_id       
WHERE d.class = 1  
ORDER BY object_name, column_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-columns-that-depend-on-a-specified-clr-user-defined-type-or-alias-type"></a><a name="_FAQ22"></a> 指定された CLR ユーザー定義型または別名型に依存する列を検索操作方法には  
 次のクエリを実行する前に、を有効な名前に置き換え、を `<database_name>` `<schema_name.data_type_name>` スキーマ修飾の CLR ユーザー定義型またはスキーマ修飾された別名型の名前に置き換えます。 次のクエリでは、 **db_owner** ロールのメンバーシップ、またはデータベース内のすべての依存列および計算列のメタデータを表示する権限が必要です。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,c.name AS column_name   
    ,SCHEMA_NAME(t.schema_id) AS schema_name  
    ,TYPE_NAME(c.user_type_id) AS user_type_name  
    ,c.max_length  
    ,c.precision  
    ,c.scale  
    ,c.is_nullable  
    ,c.is_computed  
FROM sys.columns AS c  
INNER JOIN sys.types AS t ON c.user_type_id = t.user_type_id  
WHERE c.user_type_id = TYPE_ID('<schema_name.data_type_name>');   
GO  
  
```  
  
 次のクエリは、CLR ユーザー定義型または別名に依存する列の制限されたビューを返しますが、結果セットは **public** ロールで参照できます。 このクエリは、ユーザー定義型に対する参照権限を他のユーザーに許可していて、その型を使用する他のユーザーが作成したオブジェクトのメタデータを表示する権限がない場合に使用できます。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name   
    ,COL_NAME(object_id, column_id) AS column_name  
    ,TYPE_NAME(user_type_id) AS user_type  
FROM sys.column_type_usages  
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-computed-columns-that-depend-on-a-specified-clr-user-defined-type-or-alias-type"></a><a name="_FAQ23"></a> 指定された CLR ユーザー定義型または別名型に依存する計算列を検索操作方法には  
 次のクエリの `<database_name>` を有効な名前に置き換え、`<schema_name.data_type_name>` をスキーマ修飾の CLR ユーザー定義型または別名型の有効な名前に置き換えてから、クエリを実行します。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,COL_NAME(object_id, column_id) AS column_name  
FROM sys.sql_dependencies  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(object_id, 'IsTable') = 1;   -- exclude non-table dependencies  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-parameters-that-depend-on-a-specified-clr-user-defined-type-or-alias-type"></a><a name="_FAQ24"></a> 指定された CLR ユーザー定義型または別名型に依存するパラメーターを検索操作方法には  
 次のクエリの `<database_name>` を有効な名前に置き換え、`<schema_name.data_type_name>` をスキーマ修飾の CLR ユーザー定義型または別名型の有効な名前に置き換えてから、クエリを実行します。 次のクエリでは、 **db_owner** ロールのメンバーシップ、またはデータベース内のすべての依存列および計算列のメタデータを表示する権限が必要です。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,NULL AS procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
UNION   
SELECT OBJECT_NAME(object_id) AS object_name  
    ,procedure_number  
    ,name AS param_name  
    ,parameter_id AS param_num  
    ,TYPE_NAME(p.user_TYPE_ID) AS type_name  
FROM sys.numbered_procedure_parameters AS p  
WHERE p.user_TYPE_ID = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY object_name, procedure_number, param_num;  
GO  
  
```  
  
 次のクエリは、CLR ユーザー定義型または別名に依存するパラメーターの制限されたビューを返しますが、結果セットは **public** ロールから参照できます。 このクエリは、ユーザー定義型に対する参照権限を他のユーザーに許可していて、その型を使用する他のユーザーが作成したオブジェクトのメタデータを表示する権限がない場合に使用できます。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) AS object_name  
    ,parameter_id  
    ,TYPE_NAME(user_type_id) AS type_name  
FROM sys.parameter_type_usages   
WHERE user_type_id = TYPE_ID('<schema_name.data_type_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-check-constraints-that-depend-on-a-specified-clr-user-defined-type"></a><a name="_FAQ25"></a> 指定された CLR ユーザー定義型に依存する CHECK 制約を検索操作方法には、  
 次のクエリを実行する前に、を有効な名前に置き換え、を `<database_name>` `<schema_name.data_type_name>` スキーマ修飾の CLR ユーザー定義型の有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(o.parent_object_id) AS table_name  
    ,OBJECT_NAME(o.object_id) AS constraint_name  
FROM sys.sql_dependencies AS d  
JOIN sys.objects AS o ON o.object_id = d.object_id  
WHERE referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
    AND class = 2 -- schema-bound references to type  
    AND OBJECTPROPERTY(o.object_id, 'IsCheckCnst') = 1; -- exclude non-CHECK dependencies  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-views-transact-sql-functions-and-transact-sql-stored-procedures-that-depend-on-a-specified-clr-user-defined-type-or-alias-type"></a><a name="_FAQ26"></a> 指定した CLR ユーザー定義型または別名型に依存するビュー、Transact-sql 関数、および Transact-sql ストアドプロシージャを検索操作方法には、以下を参照してください。  
 次のクエリの `<database_name>` を有効な名前に置き換え、`<schema_name.data_type_name>` をスキーマ修飾の CLR ユーザー定義型または別名型の有効な名前に置き換えてから、クエリを実行します。  
  
 関数またはプロシージャで定義されているパラメーターは、暗黙的にスキーマにバインドされます。 したがって、CLR ユーザー定義型または別名型に依存するパラメーターは、 [sql_dependencies](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md) カタログビューを使用して表示できます。 プロシージャとトリガーはスキーマバインドされていません。 つまり、プロシージャやトリガーの本体で定義されている式と、CLR ユーザー定義型または別名型の間の依存関係は保守されません。 CLR ユーザー定義型または別名型に依存する式を持つスキーマバインドビューおよびスキーマバインドユーザー定義関数は、 **sql_dependencies** カタログビューで保持されます。 型と CLR 関数と CLR プロシージャの間の依存関係は保持されません。  
  
 次のクエリは、指定された CLR ユーザー定義型または別名型に関して、ビュー、[!INCLUDE[tsql](../../includes/tsql-md.md)] 関数、および [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャ内でスキーマにバインドされた依存関係をすべて返します。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS dependent_object_schema  
  ,OBJECT_NAME(o.object_id) AS dependent_object_name  
  ,o.type_desc AS dependent_object_type  
  ,d.class_desc AS kind_of_dependency  
  ,TYPE_NAME (d.referenced_major_id) AS type_name  
FROM sys.sql_dependencies AS d   
JOIN sys.objects AS o  
  ON d.object_id = o.object_id  
  AND o.type IN ('FN','IF','TF', 'V', 'P')  
WHERE d.class = 2 -- dependencies on types  
  AND d.referenced_major_id = TYPE_ID('<schema_name.data_type_name>')  
ORDER BY dependent_object_schema, dependent_object_name;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-constraints-for-a-specified-table"></a><a name="_FAQ27"></a> 指定されたテーブルのすべての制約を検索操作方法には  
 次のクエリを実行する前に、 `<database_name>` とを `<schema_name.table_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id) as constraint_name  
    ,SCHEMA_NAME(schema_id) AS schema_name  
    ,OBJECT_NAME(parent_object_id) AS table_name  
    ,type_desc  
    ,create_date  
    ,modify_date  
    ,is_ms_shipped  
    ,is_published  
    ,is_schema_published  
FROM sys.objects  
WHERE type_desc LIKE '%CONSTRAINT'   
    AND parent_object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-indexes-for-a-specified-table"></a><a name="_FAQ28"></a> 指定されたテーブルのすべてのインデックスを検索操作方法には  
 次のクエリを実行する前に、 `<database_name>` とを `<schema_name.table_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('<schema_name.table_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-objects-that-have-a-specified-column-name"></a><a name="_FAQ30"></a> 指定された列名を持つすべてのオブジェクトを検索操作方法には  
 次のクエリを実行する前に、 `<database_name>` とを `<column_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_NAME(object_id)  
FROM sys.columns  
WHERE name = '<column_name>';  
GO  
  
```  
  
 または  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name   
    ,o.name AS object_name  
    ,type_desc  
FROM sys.objects AS o  
INNER JOIN sys.columns AS c ON o.object_id = c.object_id  
WHERE c.name = '<column_name>';  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-user-defined-tables-in-a-specified-database"></a><a name="_FAQ31"></a> 指定されたデータベース内のすべてのユーザー定義テーブルを検索操作方法には  
 次のクエリを実行する前に、を `<database_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT *   
FROM sys.tables;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-tables-and-indexes-that-are-partitioned"></a><a name="_FAQ32"></a> パーティション分割されているすべてのテーブルとインデックスを検索操作方法には  
 次のクエリを実行する前に、を `<database_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT SCHEMA_NAME(o.schema_id) AS schema_name  
    ,OBJECT_NAME(p.object_id) AS table_name  
    ,i.name AS index_name  
    ,p.partition_number  
    ,rows   
FROM sys.partitions AS p  
INNER JOIN sys.indexes AS i ON p.object_id = i.object_id AND p.index_id = i.index_id  
INNER JOIN sys.partition_schemes ps ON i.data_space_id=ps.data_space_id  
INNER JOIN sys.objects AS o ON o.object_id = i.object_id  
ORDER BY index_name, partition_number;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-statistics-on-a-specified-object"></a><a name="_FAQ33"></a> 指定されたオブジェクトのすべての統計を検索操作方法には  
 次のクエリを実行する前に、を有効な名前に置き換え、を `<database_name>` `<schema_name.object_name>` 有効なテーブル、インデックス付きビュー、またはテーブル値関数の名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT name AS statistics_name  
    ,stats_id  
    ,auto_created  
    ,user_created  
    ,no_recompute  
FROM sys.stats  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-all-the-statistics-and-statistics-columns-on-a-specified-object"></a><a name="_FAQ34"></a> 指定されたオブジェクトのすべての統計列と統計列を検索操作方法には  
 次のクエリを実行する前に、を有効な名前に置き換え、を `<database_name>` `<schema_name.object_name>` 有効なテーブル、インデックス付きビュー、またはテーブル値関数の名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT s.name AS statistics_name  
    ,c.name AS column_name  
    ,sc.stats_column_id  
FROM sys.stats AS s  
INNER JOIN sys.stats_columns AS sc   
    ON s.object_id = sc.object_id AND s.stats_id = sc.stats_id  
INNER JOIN sys.columns AS c   
    ON sc.object_id = c.object_id AND c.column_id = sc.column_id  
WHERE s.object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 [TOP](#_TOP)  
  
###  <a name="how-do-i-find-the-definition-of-a-view"></a><a name="_FAQ35"></a> ビューの定義を検索操作方法には  
 次のクエリを実行する前に、 `<database_name>` とを `<schema_name.object_name>` 有効な名前に置き換えます。  
  
```  
USE <database_name>;  
GO  
SELECT definition  
FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('<schema_name.object_name>');  
GO  
  
```  
  
 または、 `OBJECT_DEFINITION` 次の例に示すように、関数を使用することもできます。  
  
```  
USE <database_name>;  
GO  
SELECT OBJECT_DEFINITION (OBJECT_ID('<schema_name.object_name>')) AS ObjectDefinition;  
GO  
  
```  
  
 [TOP](#_TOP)  
  
## <a name="see-also"></a>参照  
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
