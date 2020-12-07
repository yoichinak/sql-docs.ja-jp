---
description: sp_control_plan_guide (Transact-sql)
title: sp_control_plan_guide (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_control_plan_guide
- sp_control_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_plan_guide
ms.assetid: c96d43d5-6507-4d66-b3f5-f44c0617cb5c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5a66806fa3c4865da7486a7ada3c46a9691be6d7
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753904"
---
# <a name="sp_control_plan_guide-transact-sql"></a>sp_control_plan_guide (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  プランガイドを削除するか、有効または無効にします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_control_plan_guide [ @operation = ] N'<control_option>'  
  [ , [ @name = ] N'plan_guide_name' ]  
  
<control_option>::=  
{   
    DROP   
  | DROP ALL  
  | DISABLE  
  | DISABLE ALL  
  | ENABLE   
  | ENABLE ALL  
}  
```  
  
## <a name="arguments"></a>引数  
 **N '** _plan_guide_name_ **'**  
 削除するか、有効または無効にするプラン ガイドを指定します。 現在のデータベースに対して*plan_guide_name*が解決されます。 指定しない場合、 *plan_guide_name* 既定値は NULL です。  
  
 DROP  
 *Plan_guide_name*によって指定されたプランガイドを削除します。 プランガイドが削除された後、プランガイドによって以前一致したクエリの今後の実行は、プランガイドの影響を受けません。  
  
 DROP ALL  
 現在のデータベースのすべてのプラン ガイドを削除します。 DROP ALL が指定されている場合、 **N '**_plan_guide_name_を指定することはできません。  
  
 DISABLE  
 *Plan_guide_name*によって指定されたプランガイドを無効にします。 プラン ガイドが無効になった後は、そのプラン ガイドに以前一致していたクエリを実行しても、そのプラン ガイドによる影響は受けません。  
  
 DISABLE ALL  
 現在のデータベース内のすべてのプランガイドを無効にします。 **N '**_PLAN_GUIDE_NAME_ は、DISABLE ALL が指定されている場合は指定できません。  
  
 有効化  
 *Plan_guide_name*によって指定されたプランガイドを有効にします。 プラン ガイドが有効になった後は、そのプラン ガイドを適切なクエリと照合できます。 既定では、プランガイドは作成時に有効になります。  
  
 ENABLE ALL  
 現在のデータベース内のすべてのプランガイドを有効にします。 ENABLE ALL が指定されている場合、 **N '**_plan_guide_name_**'** を指定することはできません。  
  
## <a name="remarks"></a>解説  
 有効、無効にする場合のどちらでも、そのプラン ガイドで参照されている関数、ストアド プロシージャ、または DML トリガーを削除または変更しようとすると、エラーが発生します。  
  
 無効なプラン ガイドを無効にする場合や、有効なプラン ガイドを有効にする場合は影響は生じず、エラーなしで実行できます。  
  
 プランガイドは、のすべてのエディションで使用できるわけではありません [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、「[Editions and Supported Features for SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)」 (SQL Server 2016 のエディションとサポートされる機能) を参照してください。 ただし、の任意のエディションの [すべて削除] または [すべて削除] オプションを使用して **sp_control_plan_guide** を実行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="permissions"></a>アクセス許可  
 オブジェクト型 ( ** @type = '** OBJECT **'** を指定して作成) のプランガイドで**sp_control_plan_guide**を実行するには、プランガイドによって参照されるオブジェクトに対する ALTER 権限が必要です。 その他すべてのプラン ガイドでは、ALTER DATABASE 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-enabling-disabling-and-dropping-a-plan-guide"></a>A. プラン ガイドを無効にし、有効にした後、削除する  
 次の例ではプラン ガイドを作成し、それを無効にし、有効にした後、削除します。  
  
```  
--Create a procedure on which to define the plan guide.  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country;  
END  
GO  
--Create the plan guide.  
EXEC sp_create_plan_guide N'Guide3',  
    N'SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country',  
    N'OBJECT',  
    N'Sales.GetSalesOrderByCountry',  
    NULL,  
    N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
GO  
--Disable the plan guide.  
EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
GO  
--Enable the plan guide.  
EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
GO  
--Drop the plan guide.  
EXEC sp_control_plan_guide N'DROP', N'Guide3';  
```  
  
### <a name="b-disabling-all-plan-guides-in-the-current-database"></a>B. 現在のデータベース内のすべてのプランガイドを無効にする  
 次の例では、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースのすべてのプラン ガイドを無効にします。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_control_plan_guide N'DISABLE ALL';  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [プラン ガイド](../../relational-databases/performance/plan-guides.md)  
  
