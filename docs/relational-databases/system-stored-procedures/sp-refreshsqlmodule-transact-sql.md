---
description: sp_refreshsqlmodule (Transact-SQL)
title: sp_refreshsqlmodule (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_refreshsqlmodule_TSQL
- sp_refreshsqlmodule
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server], stored procedures
- metadata [SQL Server], triggers
- metadata [SQL Server], views
- triggers [SQL Server], refreshing metadata
- views [SQL Server], refreshing metadata
- sp_refreshsqlmodule
- metadata [SQL Server], functions
- stored procedures [SQL Server], refreshing metadata
- user-defined functions [SQL Server], refreshing metadata
ms.assetid: f0022a05-50dd-4620-961d-361b1681d375
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5265d2b38f8d41be321a63b701bb286b3b793e1c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535033"
---
# <a name="sp_refreshsqlmodule-transact-sql"></a>sp_refreshsqlmodule (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  現在のデータベースの、スキーマにバインドされていない指定のストアドプロシージャ、ユーザー定義関数、ビュー、DML トリガー、データベースレベルの DDL トリガー、またはサーバーレベルの DDL トリガーのメタデータを更新します。 これらのオブジェクトの永続メタデータ (パラメーターのデータ型など) は、基になるオブジェクトが変更されたため、古くなる可能性があります。
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_refreshsqlmodule [ @name = ] 'module_name'   
    [ , [ @namespace = ] ' <class> ' ]  
  
<class> ::=  
{  
  | DATABASE_DDL_TRIGGER  
  | SERVER_DDL_TRIGGER  
}  
  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'module\_name'` ストアドプロシージャ、ユーザー定義関数、ビュー、DML トリガー、データベースレベルの DDL トリガー、またはサーバーレベルの DDL トリガーの名前を指定します。 *module_name* を共通言語ランタイム (clr) ストアドプロシージャまたは clr 関数にすることはできません。 *module_name* をスキーマバインドにすることはできません。 *module_name* は **nvarchar**,、既定値はありません。 *module_name* にはマルチパート識別子を指定できますが、参照できるのは現在のデータベース内のオブジェクトだけです。  
  
`[ , @namespace = ] ' \<class> '` は、指定されたモジュールのクラスです。 *Module_name*が DDL トリガーである場合 \<class> は、が必要です。 *\<class>***nvarchar**(20) です。 有効な入力は次のとおりです。  

* DATABASE_DDL_TRIGGER

* SERVER_DDL_TRIGGER-以降 **に適用さ** [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] れます。

## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または0以外の数値 (失敗)  
  
## <a name="remarks"></a>解説  
 定義に影響を与えるモジュールの基になるオブジェクトに変更が加えられたときに、 **sp_refreshsqlmodule**を実行する必要があります。 そうしないと、クエリまたは呼び出されたときに、予期しない結果が生成される可能性があります。 ビューを更新するには、 **sp_refreshsqlmodule** または **sp_refreshview** を同じ結果で使用できます。  
  
 **sp_refreshsqlmodule** は、オブジェクトに関連付けられている権限、拡張プロパティ、または SET オプションには影響しません。  
  
 サーバーレベルの DDL トリガーを更新するには、任意のデータベースのコンテキストからこのストアドプロシージャを実行します。  
  
> [!NOTE]  
>  オブジェクトに関連付けられている署名は、 **sp_refreshsqlmodule**を実行すると削除されます。  
  
## <a name="permissions"></a>アクセス許可  
 モジュールに対する ALTER 権限、およびオブジェクトによって参照される CLR ユーザー定義型と XML スキーマ コレクションに対する REFERENCES 権限が必要です。 指定されたモジュールがデータベース レベルの DDL トリガーである場合は、現在のデータベースに対する ALTER ANY DATABASE DDL TRIGGER 権限が必要です。 指定されたモジュールがサーバーレベルの DDL トリガーである場合、CONTROL SERVER 権限が必要です。  
  
 さらに、EXECUTE AS 句で定義されているモジュールでは、指定したプリンシパルに対して IMPERSONATE 権限が必要です。 通常、オブジェクトを更新しても、モジュールが EXECUTE AS USER を指定して定義された場合を除いて、オブジェクトの EXECUTE AS のプリンシパルは変更されません。プリンシパルのユーザー名は、モジュールが作成された時点とは異なるユーザーに解決されます。  
  
## <a name="examples"></a>例  
  
### <a name="a-refreshing-a-user-defined-function"></a>A. ユーザー定義関数の更新  
 次の例では、ユーザー定義関数を更新します。 この例では、を使用する別名データ型、 `mytype` 、およびユーザー定義関数を作成し `to_upper` `mytype` ます。 次に、を `mytype` に変更し、 `myoldtype` 別の `mytype` 定義を持つ新しいを作成します。 `dbo.to_upper`関数は、古いものではなく、の新しい実装を参照するように更新され `mytype` ます。  
  
```  
-- Create an alias type.  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT 'mytype' FROM sys.types WHERE name = 'mytype')  
DROP TYPE mytype;  
GO  
  
CREATE TYPE mytype FROM nvarchar(5);  
GO  
  
IF OBJECT_ID ('dbo.to_upper', 'FN') IS NOT NULL  
DROP FUNCTION dbo.to_upper;  
GO  
  
CREATE FUNCTION dbo.to_upper (@a mytype)  
RETURNS mytype  
WITH ENCRYPTION  
AS  
BEGIN  
RETURN upper(@a)  
END;  
GO  
  
SELECT dbo.to_upper('abcde');  
GO  
  
-- Increase the length of the alias type.  
sp_rename 'mytype', 'myoldtype', 'userdatatype';  
GO  
  
CREATE TYPE mytype FROM nvarchar(10);  
GO  
  
-- The function parameter still uses the old type.  
SELECT name, type_name(user_type_id)   
FROM sys.parameters   
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh'); -- Fails because of truncation  
GO  
  
-- Refresh the function to bind to the renamed type.  
EXEC sys.sp_refreshsqlmodule 'dbo.to_upper';  
  
-- The function parameters are now bound to the correct type and the statement works correctly.  
SELECT name, type_name(user_type_id) FROM sys.parameters  
WHERE object_id = OBJECT_ID('dbo.to_upper');  
GO  
  
SELECT dbo.to_upper('abcdefgh');  
GO  
```  
  
### <a name="b-refreshing-a-database-level-ddl-trigger"></a>B. データベース レベルの DDL トリガーを更新する  
 次の例では、データベースレベルの DDL トリガーを更新します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddlDatabaseTriggerLog' , @namespace = 'DATABASE_DDL_TRIGGER';  
GO  
```  
  
### <a name="c-refreshing-a-server-level-ddl-trigger"></a>C. サーバー レベルの DDL トリガーを更新する  
 次の例では、サーバーレベルの DDL トリガーを更新します。  
  
||  
|-|  
|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。|  
  
```  
USE master;  
GO  
EXEC sys.sp_refreshsqlmodule @name = 'ddl_trig_database' , @namespace = 'SERVER_DDL_TRIGGER';  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [sp_refreshview &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
