---
description: sp_dropextendedproperty (Transact-SQL)
title: sp_dropextendedproperty (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproperty_TSQL
- sp_dropextendedproperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproperty
ms.assetid: 4851865a-86ca-4823-991a-182dd1934075
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 28a73c5cea3f957c83529de4d452efc88f6a6551
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549800"
---
# <a name="sp_dropextendedproperty-transact-sql"></a>sp_dropextendedproperty (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  既存の拡張プロパティを削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropextendedproperty   
    [ @name = ] { 'property_name' }  
      [ , [ @level0type = ] { 'level0_object_type' }   
        , [ @level0name = ] { 'level0_object_name' }   
            [ , [ @level1type = ] { 'level1_object_type' }   
              , [ @level1name = ] { 'level1_object_name' }   
                [ , [ @level2type = ] { 'level2_object_type' }   
                  , [ @level2name = ] { 'level2_object_name' }   
                ]   
            ]   
        ]   
    ]   
```  
  
## <a name="arguments"></a>引数  
 [ @name =] {'*property_name*'}  
 削除するプロパティの名前を指定します。 *property_name* は **sysname** であり、NULL にすることはできません。  
  
 [ @level0type =] {'*level0_object_type*'}  
 指定したレベル0のオブジェクトの種類の名前を指定します。 *level0_object_type* は **varchar (128)**,、既定値は NULL です。  
  
 有効な入力は、ASSEMBLY、CONTRACT、EVENT NOTIFICATION、FILEGROUP、MESSAGE TYPE、PARTITION FUNCTION、PARTITION SCHEME、REMOTE SERVICE BINDING、ROUTE、SCHEMA、SERVICE、USER、TRIGGER、TYPE、および NULL です。  
  
> [!IMPORTANT]  
>  レベル0のユーザーと型は、今後のバージョンのでは削除される予定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。 USER の代わりに、レベル 0 の種類として SCHEMA を使用してください。 TYPE については、レベル 0 の種類として SCHEMA、レベル 1 の種類として TYPE を使用してください。  
  
 [ @level0name =] {'*level0_object_name*'}  
 指定したレベル0のオブジェクトの種類の名前を指定します。 *level0_object_name* は **sysname** で、既定値は NULL です。  
  
 [ @level1type =] {'*level1_object_type*'}  
 レベル1のオブジェクトの種類を示します。 *level1_object_type* は **varchar (128)** で、既定値は NULL です。 有効な値は、AGGREGATE、DEFAULT、FUNCTION、LOGICAL FILE NAME、PROCEDURE、QUEUE、RULE、シノニム、TABLE、TABLE_TYPE、TYPE、VIEW、XML SCHEMA COLLECTION、および NULL です。  
  
 [ @level1name =] {'*level1_object_name*'}  
 指定したレベル1のオブジェクトの種類の名前を指定します。 *level1_object_name* は **sysname** で、既定値は NULL です。  
  
 [ @level2type =] {'*level2_object_type*'}  
 レベル 2 のオブジェクトの種類です。 *level2_object_type* は **varchar (128)** で、既定値は NULL です。 有効な値は、COLUMN、CONSTRAINT、EVENT NOTIFICATION、INDEX、PARAMETER、TRIGGER、および NULL です。  
  
 [ @level2name =] {'*level2_object_name*'}  
 指定したレベル2のオブジェクトの種類の名前を指定します。 *level2_object_name* は **sysname** で、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 拡張プロパティを指定するために、データベース内のオブジェクト [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、0、1、および2の3つのレベルに分類されます。 レベル0は最上位レベルで、データベーススコープに含まれるオブジェクトとして定義されます。 レベル 1 のオブジェクトはスキーマ スコープまたはユーザー スコープに含まれ、レベル 2 のオブジェクトはレベル 1 のオブジェクトに含まれます。 これら、どのレベルのオブジェクトに対しても、拡張プロパティを定義できます。 あるレベルのオブジェクトを参照する場合は、その上位レベルにあるすべてのオブジェクトの種類と名前で修飾する必要があります。  
  
 有効な *property_name*が指定されている場合、すべてのオブジェクトの種類と名前が null で、プロパティが現在のデータベースに存在すると、そのプロパティは削除されます。 このトピックの例 B を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 固定データベース ロール db_owner および db_ddladmin のメンバーは、任意のオブジェクトの拡張プロパティを削除できます。ただし、例外として、db_ddladmin はデータベース自体、ユーザー、およびロールに対しては、プロパティを追加できません。  
  
 ユーザーは、自身が所有するオブジェクト、および ALTER 権限または CONTROL 権限を持つオブジェクトの拡張プロパティを削除できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-dropping-an-extended-property-on-a-column"></a>A. 列の拡張プロパティを削除する  
 次の例では、スキーマ `caption` に含まれるテーブル `id` 内の列 `T1` からプロパティ `dbo` を削除します。  
  
```  
CREATE TABLE T1 (id int , name char (20));  
GO  
EXEC sp_addextendedproperty   
     @name = 'caption'   
    ,@value = 'Employee ID'   
    ,@level0type = 'schema'   
    ,@level0name = dbo  
    ,@level1type = 'table'  
    ,@level1name = 'T1'  
    ,@level2type = 'column'  
    ,@level2name = id;  
GO  
EXEC sp_dropextendedproperty   
     @name = 'caption'   
    ,@level0type = 'schema'   
    ,@level0name = dbo  
    ,@level1type = 'table'  
    ,@level1name = 'T1'  
    ,@level2type = 'column'  
    ,@level2name = id;  
GO  
DROP TABLE T1;  
GO  
```  
  
### <a name="b-dropping-an-extended-property-on-a-database"></a>B. データベースの拡張プロパティを削除する  
 次の例では、という名前のプロパティを `MS_Description` サンプルデータベースから削除し [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] ます。 これはデータベース自体のプロパティであり、オブジェクトの種類および名前は指定しません。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_dropextendedproperty   
@name = N'MS_Description';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [fn_listextendedproperty &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_updateextendedproperty &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)   
 [extended_properties &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
