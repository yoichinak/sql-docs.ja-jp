---
description: sys.fn_validate_plan_guide (Transact-SQL)
title: fn_validate_plan_guide (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_validate_plan_guide
- sys.fn_validate_plan_guide_TSQL
- fn_validate_plan_guide
- fn_validate_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_validate_plan_guide function
- sys.fn_validate_plan_guide function
ms.assetid: 3af8b47a-936d-4411-91d1-d2d16dda5623
author: rothja
ms.author: jroth
ms.openlocfilehash: b19a3cd2f2ee449780127682555f1ae77fabd5d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88396898"
---
# <a name="sysfn_validate_plan_guide-transact-sql"></a>sys.fn_validate_plan_guide (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたプランガイドの有効性を確認します。 sys.fn_validate_plan_guide 関数では、クエリにプラン ガイドを適用した場合に最初に発生するエラーのメッセージが返されます。 プラン ガイドが有効な場合は空の行セットが返されます。 プランガイドは、データベースの物理デザインに変更が加えられた後に無効になることがあります。 たとえば、プランガイドで特定のインデックスが指定されている場合、そのインデックスが削除されると、クエリはそのプランガイドを使用できなくなります。  
  
 プラン ガイドを検証することで、変更を加えずにオプティマイザーで使用できるかどうかを確認できます。 この関数の結果に基づいて、そのプラン ガイドを削除してクエリを再チューニングするか、データベースのデザインを変更する (プラン ガイドで指定されているインデックスを再作成するなど) かを決定できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sys.fn_validate_plan_guide ( plan_guide_id )  
```  
  
## <a name="arguments"></a>引数  
 *plan_guide_id*  
 [Plan_guides](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)カタログビューで報告されるプランガイドの ID を示します。 *plan_guide_id* は **int** で、既定値はありません。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|msgnum|**int**|エラーメッセージの ID。|  
|severity|**tinyint**|メッセージの重大度レベル (1 ~ 25)。|  
|状態|**smallint**|エラーが発生したコード内の場所を示すエラーの状態番号です。|  
|message|**nvarchar(2048)**|エラーのメッセージテキスト。|  
  
## <a name="permissions"></a>アクセス許可  
 スコープが OBJECT のプラン ガイドでは、参照先オブジェクトに対する VIEW DEFINITION 権限または ALTER 権限と、プラン ガイドに含まれるクエリやバッチをコンパイルするための権限が必要です。 たとえば、バッチに SELECT ステートメントが含まれている場合は、参照先オブジェクトに対する SELECT 権限が必要です。  
  
 スコープが SQL または TEMPLATE のプラン ガイドでは、データベースに対する ALTER 権限と、プラン ガイドに含まれるクエリやバッチをコンパイルするための権限が必要です。 たとえば、バッチに SELECT ステートメントが含まれている場合は、参照先オブジェクトに対する SELECT 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-validating-all-plan-guides-in-a-database"></a>A. データベースのすべてのプラン ガイドの検証をテストする  
 次の例では、現在のデータベースのすべてのプラン ガイドの有効性を確認します。 空の結果セットが返された場合は、すべてのプラン ガイドが有効です。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT plan_guide_id, msgnum, severity, state, message  
FROM sys.plan_guides  
CROSS APPLY fn_validate_plan_guide(plan_guide_id);  
GO  
```  
  
### <a name="b-testing-plan-guide-validation-before-implementing-a-change-to-the-database"></a>B. データベースに変更を実装する前のプランガイド検証のテスト  
 次の例では、明示的なトランザクションを使用してインデックスを削除します。 関数は、 `sys.fn_validate_plan_guide` このアクションによってデータベース内のプランガイドが無効になるかどうかを判断するために実行されます。 この関数の結果に基づいて、`DROP INDEX` ステートメントがコミットされるか、トランザクションがロールバックされます。トランザクションがロールバックされた場合は、インデックスは削除されません。  
  
```sql  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DROP INDEX IX_SalesOrderHeader_CustomerID ON Sales.SalesOrderHeader;  
-- Check for invalid plan guides.  
IF EXISTS (SELECT plan_guide_id, msgnum, severity, state, message  
           FROM sys.plan_guides  
           CROSS APPLY sys.fn_validate_plan_guide(plan_guide_id))  
    ROLLBACK TRANSACTION;  
ELSE  
    COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [プランガイド](../../relational-databases/performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
