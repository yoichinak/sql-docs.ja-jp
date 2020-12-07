---
description: GetRoot (データベース エンジン)
title: GetRoot (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetRoot
- GetRoot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetRoot [Database Engine]
ms.assetid: 240b70f1-eeda-44ab-b4bb-9e4af80fa7c0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 645c39d8108ba52212788a65ae2d6116ee629e34
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "92037134"
---
# <a name="getroot-database-engine"></a>GetRoot (データベース エンジン)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

階層ツリーのルートを返します。 GetRoot() 静的メソッドです。
  
## <a name="syntax"></a>構文  
  
```syntaxsql
-- Transact-SQL syntax  
hierarchyid::GetRoot ( )   
```  
  
```syntaxsql
-- CLR syntax  
static SqlHierarchyId GetRoot ( )   
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型  
**SQL Server の戻り値の型: hierarchyid**
  
**CLR 戻り値の型:SqlHierarchyId**
  
## <a name="remarks"></a>解説  
階層ツリー内のルート ノードを決定するために使用されます。
  
## <a name="examples"></a>例  
  
### <a name="a-transact-sql-example"></a>A. Transact-SQL の例  
次の例では、階層ツリーのルートを返します。
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode = hierarchyid::GetRoot()  
```  
  
### <a name="b-clr-example"></a>B. CLR の例  
次のコード スニペットの呼び出し、 GetRoot() メソッド。
  
```sql
SqlHierarchyId.GetRoot()  
```  
  
## <a name="see-also"></a>参照
[hierarchyid データ型メソッド リファレンス](./hierarchyid-data-type-method-reference.md)  
[階層データ (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
