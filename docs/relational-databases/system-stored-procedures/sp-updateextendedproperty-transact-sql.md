---
description: sp_updateextendedproperty (Transact-sql)
title: sp_updateextendedproperty (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updateextendedproperty_TSQL
- sp_updateextendedproperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updateextendedproperty
ms.assetid: 7f02360f-cb9e-48b4-b75f-29b4bc9ea304
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 52c91c09c440402df383253996e660d7abdb317c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551166"
---
# <a name="sp_updateextendedproperty-transact-sql"></a>sp_updateextendedproperty (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  既存の拡張プロパティの値を更新します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_updateextendedproperty  
    [ @name = ]{ 'property_name' }   
    [ , [ @value = ]{ 'value' }  
        [, [ @level0type = ]{ 'level0_object_type' }  
         , [ @level0name = ]{ 'level0_object_name' }  
              [, [ @level1type = ]{ 'level1_object_type' }  
               , [ @level1name = ]{ 'level1_object_name' }  
                     [, [ @level2type = ]{ 'level2_object_type' }  
                      , [ @level2name = ]{ 'level2_object_name' }  
                     ]  
              ]  
        ]  
    ]  
```  
  
## <a name="arguments"></a>引数  
 [ @name =] {'*property_name*'}  
 更新するプロパティの名前です。 *property_name* は **sysname**であり、NULL にすることはできません。  
  
 [ @value =] {'*値*'}  
 プロパティに関連付けられている値を指定します。 *値* は **sql_variant**,、既定値は NULL です。 *値*のサイズは7500バイト以下である必要があります。  
  
 [ @level0type =] {'*level0_object_type*'}  
 ユーザーまたはユーザー定義型を指定します。 *level0_object_type* は **varchar (128)**,、既定値は NULL です。 有効な入力は、ASSEMBLY、CONTRACT、EVENT NOTIFICATION、FILEGROUP、MESSAGE TYPE、PARTITION FUNCTION、PARTITION SCHEME、PLAN GUIDE、REMOTE SERVICE BINDING、ROUTE、SCHEMA、SERVICE、USER、TRIGGER、TYPE、および NULL です。  
  
> [!IMPORTANT]  
>  レベル0のユーザーと型は、今後のバージョンのでは削除される予定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。 USER の代わりに、レベル 0 の種類として SCHEMA を使用してください。 TYPE については、レベル 0 の種類として SCHEMA、レベル 1 の種類として TYPE を使用してください。  
  
 [ @level0name =] {'*level0_object_name*'}  
 指定したレベル1のオブジェクトの種類の名前を指定します。 *level0_object_name* は **sysname** で、既定値は NULL です。  
  
 [ @level1type =] {'*level1_object_type*'}  
 レベル1のオブジェクトの種類を示します。 *level1_object_type* は **varchar (128)** で、既定値は NULL です。 有効な値は、AGGREGATE、DEFAULT、FUNCTION、LOGICAL FILE NAME、PROCEDURE、QUEUE、RULE、シノニム、TABLE、TABLE_TYPE、TYPE、VIEW、XML SCHEMA COLLECTION、および NULL です。  
  
 [ @level1name =] {'*level1_object_name*'}  
 指定したレベル1のオブジェクトの種類の名前を指定します。 *level1_object_name* は **sysname** で、既定値は NULL です。  
  
 [ @level2type =] {'*level2_object_type*'}  
 レベル 2 のオブジェクトの種類です。 *level2_object_type* は **varchar (128)** で、既定値は NULL です。 有効な値は、COLUMN、CONSTRAINT、EVENT NOTIFICATION、INDEX、PARAMETER、TRIGGER、および NULL です。  
  
 [ @level2name =] {'*level2_object_name*'}  
 指定したレベル2のオブジェクトの種類の名前を指定します。 *level2_object_name* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 拡張プロパティを指定するために、データベース内のオブジェクト [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は3つのレベル (0、1、および 2) に分類されます。 レベル0は最上位レベルで、データベーススコープに含まれるオブジェクトとして定義されます。 レベル 1 のオブジェクトはスキーマ スコープまたはユーザー スコープに含まれ、レベル 2 のオブジェクトはレベル 1 のオブジェクトに含まれます。 これら、どのレベルのオブジェクトに対しても、拡張プロパティを定義できます。 1 つのレベルにあるオブジェクトを参照する場合は、そのオブジェクトを所有または格納する上位レベルのオブジェクトの名前で修飾する必要があります。  
  
 有効な *property_name* と *値*が指定されている場合、すべてのオブジェクトの種類と名前が null の場合、更新されたプロパティは現在のデータベースに属します。  
  
## <a name="permissions"></a>アクセス許可  
 固定データベース ロール db_owner および db_ddladmin のメンバーは、任意のオブジェクトの拡張プロパティを更新できます。ただし、例外として、db_ddladmin はデータベース自体、ユーザー、およびロールに対しては、プロパティを追加できません。  
  
 ユーザーは、自分が所有しているオブジェクト、または ALTER 権限または CONTROL 権限を持つオブジェクトに対して、拡張プロパティを更新できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-updating-an-extended-property-on-a-column"></a>A. 列の拡張プロパティの更新  
 次の例では、テーブルの列のプロパティの値を更新し `Caption` `ID` `T1` ます。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE T1 (id int , name char (20));  
GO  
EXEC sp_addextendedproperty   
    @name = N'Caption'  
    ,@value = N'Employee ID'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
--Update the extended property.  
EXEC sp_updateextendedproperty   
    @name = N'Caption'  
    ,@value = 'Employee ID must be unique.'  
    ,@level0type = N'Schema', @level0name = dbo  
    ,@level1type = N'Table',  @level1name = T1  
    ,@level2type = N'Column', @level2name = id;  
GO  
```  
  
### <a name="b-updating-an-extended-property-on-a-database"></a>B. データベースの拡張プロパティの更新  
 次の例では、最初にサンプルデータベースに拡張プロパティを作成し、その [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] プロパティの値を更新します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_addextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample OLTP Database';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_updateextendedproperty   
@name = N'NewCaption', @value = 'AdventureWorks2012 Sample Database';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [fn_listextendedproperty &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [extended_properties &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)  
  
  
