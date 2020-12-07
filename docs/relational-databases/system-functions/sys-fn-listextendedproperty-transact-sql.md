---
description: sys.fn_listextendedproperty (Transact-SQL)
title: fn_listextendedproperty (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_listextendedproperty
- fn_listextendedproperty_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_listextendedproperty function
- displaying extended properties
- database extended properties [SQL Server]
- viewing extended properties
- column extended properties [SQL Server]
- sys.fn_listextendedproperties function
- database objects [SQL Server], extended properties
- extended properties [SQL Server], columns
- table extended properties [SQL Server]
ms.assetid: 59bbb91f-a277-4a35-803e-dcb91e847a49
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dd891bcfdaddfb42e2b55e1b69e3f320563c1ba7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427824"
---
# <a name="sysfn_listextendedproperty-transact-sql"></a>sys.fn_listextendedproperty (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  データベースオブジェクトの拡張プロパティ値を返します。  
 
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_listextendedproperty (   
    { default | 'property_name' | NULL }   
  , { default | 'level0_object_type' | NULL }   
  , { default | 'level0_object_name' | NULL }   
  , { default | 'level1_object_type' | NULL }   
  , { default | 'level1_object_name' | NULL }   
  , { default | 'level2_object_type' | NULL }   
  , { default | 'level2_object_name' | NULL }   
  )   
```  
  
## <a name="arguments"></a>引数  
 { default | '*property_name*' | NULL}  
 プロパティ名を指定します。 *property_name* は **sysname**です。 有効な入力は、default、NULL、またはプロパティ名です。  
  
 { default | '*level0_object_type*' | NULL}  
 ユーザーまたはユーザー定義型を指定します。 *level0_object_type* は **varchar (128)**,、既定値は NULL です。 有効な入力は、ASSEMBLY、CONTRACT、EVENT NOTIFICATION、FILEGROUP、MESSAGE TYPE、PARTITION FUNCTION、PARTITION SCHEME、REMOTE SERVICE BINDING、ROUTE、SCHEMA、SERVICE、TRIGGER、TYPE、USER、および NULL です。  
  
> [!IMPORTANT]  
>  レベル0のユーザーと型は、今後のバージョンのでは削除される予定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。 USER の代わりに、レベル 0 の種類として SCHEMA を使用してください。 TYPE については、レベル 0 の種類として SCHEMA、レベル 1 の種類として TYPE を使用してください。  
  
 { default | '*level0_object_name*' | NULL }  
 指定したレベル0のオブジェクトの種類の名前を指定します。 *level0_object_name* は **sysname** で、既定値は NULL です。 有効な入力は、default、NULL、またはオブジェクト名です。  
  
 { default | '*level1_object_type*' | NULL }  
 レベル1のオブジェクトの種類を示します。 *level1_object_type* は **varchar (128)** で、既定値は NULL です。 有効な値は、AGGREGATE、DEFAULT、FUNCTION、LOGICAL FILE NAME、PROCEDURE、QUEUE、RULE、シノニム、TABLE、TYPE、VIEW、XML SCHEMA COLLECTION、および NULL です。  
  
> [!NOTE]  
>  既定値は NULL にマップされ、' default ' はオブジェクト型 DEFAULT にマップされます。  
  
 {default | '*level1_object_name*' |NULL }  
 指定したレベル1のオブジェクトの種類の名前を指定します。 *level1_object_name* は **sysname** で、既定値は NULL です。 有効な入力は、default、NULL、またはオブジェクト名です。  
  
 { default | '*level2_object_type*' |NULL }  
 レベル 2 のオブジェクトの種類です。 *level2_object_type* は **varchar (128)** で、既定値は NULL です。 有効な入力は、DEFAULT、default (NULL にマップ)、および NULL です。 *Level2_object_type*の有効な入力値は、COLUMN、CONSTRAINT、EVENT NOTIFICATION、INDEX、PARAMETER、TRIGGER、および NULL です。  
  
 { default | '*level2_object_name*' |NULL }  
 指定したレベル2のオブジェクトの種類の名前を指定します。 *level2_object_name* は **sysname** で、既定値は NULL です。 有効な入力は、default、NULL、またはオブジェクト名です。  
  
## <a name="tables-returned"></a>返されるテーブル  
 次の表は、fn_listextendedproperty が返すテーブルの形式です。  
  
|列名|データ型|  
|-----------------|---------------|  
|objtype|**sysname**|  
|objname|**sysname**|  
|name|**sysname**|  
|value|**sql_variant**|  
  
 返されたテーブルが空の場合、オブジェクトに拡張プロパティがないか、ユーザーにオブジェクトの拡張プロパティを一覧表示する権限がありません。 データベース自体の拡張プロパティを返す場合、objtype および objname 列は NULL になります。  
  
## <a name="remarks"></a>解説  
 *Property_name*の値が NULL または default の場合、fn_listextendedproperty 指定されたオブジェクトのすべてのプロパティを返します。  
  
 オブジェクトの種類が指定され、対応するオブジェクト名の値が NULL または default である場合、fn_listextendedproperty は、指定された型のすべてのオブジェクトのすべての拡張プロパティを返します。  
  
 オブジェクトはレベルに従って区別されます。レベル0は最上位、レベル2は最下位です。 下位レベルであるレベル 1 または 2 のオブジェクトの種類および名前を指定する場合、親オブジェクトの種類と名前を、NULL または default 以外の値で指定する必要があります。 それ以外の場合は、空のセットを返します。  
  
 **objname** は Latin1_General_CI_AI として固定されています。 ただし、比較で照合順序をオーバーライドすることによって回避できます。  
  
```  
SELECT o.[object_id] AS 'table_id', o.[name] 'table_name',  
0 AS 'column_order', NULL AS 'column_name', NULL AS 'column_datatype',  
NULL AS 'column_length', Cast(e.value AS varchar(500)) AS 'column_description'  
FROM AdventureWorks.sys.objects AS o  
LEFT JOIN sys.fn_listextendedproperty(N'MS_Description', N'user',N'HumanResources',N'table', N'Employee', null, default) AS e  
    ON o.name = e.objname COLLATE SQL_Latin1_General_CP1_CI_AS  
WHERE o.name = 'Employee';  
```  
  
## <a name="permissions"></a>アクセス許可  
 オブジェクトの拡張プロパティを一覧表示する権限は、オブジェクトの種類によって異なります。  
  
## <a name="examples"></a>例  
  
### <a name="a-displaying-extended-properties-on-a-database"></a>A. データベースの拡張プロパティを表示する  
 次の例では、データベースオブジェクト自体に設定されているすべての拡張プロパティを表示します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT objtype, objname, name, value  
FROM fn_listextendedproperty(default, default, default, default, default, default, default);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `objtype    objname     name            value`  
  
 `---------  ---------   -----------     ----------------------------`  
  
 `NULL       NULL        MS_Description  AdventureWorks2008 Sample OLTP Database`  
  
 `(1 row(s) affected)`  
  
### <a name="b-displaying-extended-properties-on-all-columns-in-a-table"></a>B. テーブル内のすべての列の拡張プロパティの表示  
 次の例では、テーブル内の列の拡張プロパティを一覧表示し `ScrapReason` ます。 これは、スキーマに含まれてい `Production` ます。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT objtype, objname, name, value  
FROM fn_listextendedproperty (NULL, 'schema', 'Production', 'table', 'ScrapReason', 'column', default);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `objtype objname      name            value`  
  
 `------- -----------  -------------   ------------------------`  
  
 `COLUMN ScrapReasonID MS_Description  Primary key for ScrapReason records.`  
  
 `COLUMN Name          MS_Description  Failure description.`  
  
 `COLUMN ModifiedDate  MS_Description  Date the record was last updated.`  
  
 `(3 row(s) affected)`  
  
### <a name="c-displaying-extended-properties-on-all-tables-in-a-schema"></a>C. スキーマ内のすべてのテーブルの拡張プロパティを表示する  
 次の例では、スキーマに含まれるすべてのテーブルの拡張プロパティを一覧表示し `Sales` ます。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT objtype, objname, name, value  
FROM fn_listextendedproperty (NULL, 'schema', 'Sales', 'table', default, NULL, NULL);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_addextendedproperty &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sp_updateextendedproperty &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)   
 [extended_properties &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
