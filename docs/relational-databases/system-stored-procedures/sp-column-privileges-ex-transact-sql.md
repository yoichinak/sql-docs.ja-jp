---
description: sp_column_privileges_ex (Transact-SQL)
title: sp_column_privileges_ex (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_column_privileges_ex
- sp_column_privileges_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_column_privileges_ex
ms.assetid: 98cb6e58-4007-40fc-b048-449fb2e7e6be
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 05b7bfa0815cd7c210b960e46192ada6b6225c4f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543689"
---
# <a name="sp_column_privileges_ex-transact-sql"></a>sp_column_privileges_ex (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたリンク サーバー上の指定されたテーブルの列の特権を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_column_privileges_ex [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @table_server = ] 'table_server'` 情報を返すリンクサーバーの名前を指定します。 *table_server* は **sysname**であり、既定値はありません。  
  
`[ @table_name = ] 'table_name'` 指定した列を含むテーブルの名前を指定します。 *table_name* は **sysname**,、既定値は NULL です。  
  
`[ @table_schema = ] 'table_schema'` テーブルスキーマを示します。 *table_schema* は **sysname**,、既定値は NULL です。  
  
`[ @table_catalog = ] 'table_catalog'` 指定した *table_name* が存在するデータベースの名前を指定します。 *table_catalog* は **sysname**,、既定値は NULL です。  
  
`[ @column_name = ] 'column_name'` 特権情報を提供する列の名前を指定します。 *column_name* は **sysname**,、既定値は NULL (すべて共通) です。  
  
## <a name="result-sets"></a>結果セット  
 次の表は結果セットの列を示しています。 返される結果は、 **TABLE_QUALIFIER**、 **TABLE_OWNER**、 **TABLE_NAME**、 **COLUMN_NAME**、および **特権**によって並べ替えられます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|テーブル修飾子の名前。 さまざまな DBMS 製品では、3つの要素で構成するテーブル (_修飾子_) がサポート**しています。**_所有者_**。**_名前_)。 では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、この列はデータベース名を表します。 一部の製品では、テーブルのデータベース環境のサーバー名を表します。 このフィールドは NULL にすることができます。|  
|**TABLE_SCHEM**|**sysname**|テーブル所有者の名前。 では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] この列は、テーブルを作成したデータベースユーザーの名前を表します。 このフィールドは常に値を返します。|  
|**TABLE_NAME**|**sysname**|テーブル名。 このフィールドは常に値を返します。|  
|**COLUMN_NAME**|**sysname**|返される **TABLE_NAME** の各列の列名。 このフィールドは常に値を返します。|  
|**権限**|**sysname**|**一覧表示された**権限付与対象ユーザーに対し、この**COLUMN_NAME**に対する権限を許可したデータベースユーザー名です。 で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、この列は常に **TABLE_OWNER**と同じです。 このフィールドは常に値を返します。<br /><br /> 権限 **の許可者の列に** は、データベース所有者 (**TABLE_OWNER**)、またはデータベース所有者が GRANT ステートメントで WITH GRANT OPTION 句を使用して権限を許可したユーザーのいずれかを指定できます。|  
|**GRANTEE**|**sysname**|**一覧表示された**権限付与者によって、この**COLUMN_NAME**に対する権限が許可されたデータベースユーザー名。 このフィールドは常に値を返します。|  
|**持っ**|**varchar (** 32 **)**|使用可能な列権限の1つ。 列権限は、次の値のいずれかになります (または、実装が定義されている場合に、データソースによってサポートされるその他の値)。<br /><br /> SELECT = 権限付与対象ユーザーは、列の **データを取得** できます。<br /><br /> 挿入 = 権限付与対象 **ユーザーは、** テーブルに新しい行 (権限付与対象ユーザー **が挿入) を**挿入するときに、この列にデータを提供できます。<br /><br /> UPDATE = 権限付与対象ユーザーは、列内の既存の **データを変更** できます。<br /><br /> REFERENCES = 権限付与対象ユーザーは、主キー/外部キーのリレーションシップで外部テーブルの列を参照**できます。** 主キー/外部キーのリレーションシップはテーブル制約で定義されます。|  
|**IS_GRANTABLE**|**varchar (** 3 **)**|権限付与対象ユーザーに対し、他のユーザーに対する権限の許可を許可するかどうかを示します ("grant with grant" 権限と **呼ばれること** もあります)。 YES、NO、または NULL を指定できます。 不明な値 (つまり NULL) は、"許可の許可" 権限が適用されないデータ ソースを示します。|  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、`HumanResources.Department` リンク サーバーにある [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの `Seattle1` テーブルの列特権情報を返します。  
  
```  
EXEC sp_column_privileges_ex @table_server = 'Seattle1',   
   @table_name = 'Department',   
   @table_schema = 'HumanResources',  
   @table_catalog ='AdventureWorks2012';  
```  
  
## <a name="see-also"></a>参照  
 [sp_table_privileges_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-ex-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
