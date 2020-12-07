---
description: GetLevel (データベース エンジン)
title: GetLevel (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- GetLevel
- GetLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetLevel [Database Engine]
ms.assetid: 81577d7e-8ff6-4e73-b7f4-94c03d4921e7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f0aa604a88902dc8bfba522556f11b267fa1e184
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "92037165"
---
# <a name="getlevel-database-engine"></a>GetLevel (データベース エンジン)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

ツリー内でのノード *this* の深さを表す整数を返します。
  
## <a name="syntax"></a>構文  
  
```syntaxsql
-- Transact-SQL syntax  
node.GetLevel ( )   
```  
  
```syntaxsql
-- CLR syntax  
SqlInt16 GetLevel ( )   
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型  
**SQL Server の戻り値の型: smallint**
  
**CLR の戻り値の型: SqlInt16**
  
## <a name="remarks"></a>解説  
1 つ以上のノードのレベルを決定したり、指定したレベルのメンバーにノードをフィルタリングしたりするために使用します。 階層のルートはレベル 0 です。
  
GetLevel は、幅優先の検索のインデックスに便利です。 詳しくは、「[階層データ &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)」をご覧ください。
  
## <a name="examples"></a>例  
  
### <a name="a-returning-the-hierarchy-level-as-a-column"></a>A. 階層レベルを列として返す  
次の例のテキスト表現を返します、 **hierarchyid**, 、階層レベル、 **EmpLevel** テーブル内のすべての行の列。
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo;  
```  
  
### <a name="b-returning-all-members-of-a-hierarchy-level"></a>B. 階層レベルのすべてのメンバーを返す  
次の例では、階層レベル 2 のテーブルのすべての行を返します。
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 2;  
```  
  
### <a name="c-returning-the-root-of-the-hierarchy"></a>C. 階層のルートを返す  
次の例では、階層レベルのルートを返します。
  
```sql
SELECT OrgNode.ToString() AS Text_OrgNode,   
OrgNode.GetLevel() AS EmpLevel, *  
FROM HumanResources.EmployeeDemo  
WHERE OrgNode.GetLevel() = 0;  
```  
  
### <a name="d-clr-example"></a>D. CLR の例  
次のコード スニペットの呼び出し、 GetLevel() メソッド。
  
```sql
this.GetLevel()  
```  
  
## <a name="see-also"></a>参照
[hierarchyid データ型メソッド リファレンス](./hierarchyid-data-type-method-reference.md)  
[階層データ (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
