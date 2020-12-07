---
description: Parse (データベース エンジン)
title: Parse (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Parse
- Parse_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Parse [Database Engine]
ms.assetid: b37e28b6-6e2e-470a-945b-ce5252da743a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8ebfca7738f8310108aab9ba988e658e7a5c1e17
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "92038365"
---
# <a name="parse-database-engine"></a>Parse (データベース エンジン)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

正規文字列形式に変換する **hierarchyid** を **hierarchyid** 値。 解析 から文字列型を変換するとき暗黙的に呼び出されます **hierarchyid** が発生します。 逆の役割を果たします [ToString](../../t-sql/data-types/tostring-database-engine.md)です。 Parse() 静的メソッドです。
  
## <a name="syntax"></a>構文  
  
```sql
-- Transact-SQL syntax  
hierarchyid::Parse ( input )  
-- This is functionally equivalent to the following syntax   
-- which implicitly calls Parse():  
CAST ( input AS hierarchyid )  
```  
  
```csharp
-- CLR syntax  
static SqlHierarchyId Parse ( SqlString input )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
*input*  
[!INCLUDE[tsql](../../includes/tsql-md.md)] : 変換対象となる文字データ型の値。
  
CLR : 評価される String 値。
  
## <a name="return-types"></a>戻り値の型  
**SQL Server の戻り値の型: hierarchyid**
  
**CLR 戻り値の型:SqlHierarchyId**
  
## <a name="remarks"></a>解説  
場合 解析 の有効な文字列表記ではない値を受け取る、 **hierarchyid**, 、例外が発生します。 たとえば場合、 **cha** r データ型には、末尾のスペースが含まれている、例外が発生します。
  
## <a name="examples"></a>例  
  
### <a name="a-converting-transact-sql-values-without-a-table"></a>A. テーブルを使用しない Transact-SQL 値の変換  
次のコード例では、`ToString` を使用して **hierarchyid** 値を文字列に変換し、`Parse` を使用して文字列値を **hierarchyid** に変換します。
  
```sql
DECLARE @StringValue AS NVARCHAR(4000), @hierarchyidValue AS hierarchyid  
SET @StringValue = '/1/1/3/'  
SET @hierarchyidValue = 0x5ADE  
  
SELECT hierarchyid::Parse(@StringValue) AS hierarchyidRepresentation,  
@hierarchyidValue.ToString() AS StringRepresentation ;
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
hierarchyidRepresentation    StringRepresentation
-------------------------    -----------------------
0x5ADE                       /1/1/3/
```
  
### <a name="b-clr-example"></a>B. CLR の例  
次のコード スニペットの呼び出し、 Parse() メソッド。
  
```csharp
string input = "/1/2/";  
SqlHierarchyId.Parse(input);  
```  
  
## <a name="see-also"></a>参照
[hierarchyid データ型メソッド リファレンス](./hierarchyid-data-type-method-reference.md)  
[階層データ (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
