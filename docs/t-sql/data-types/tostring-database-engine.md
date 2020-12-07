---
description: ToString (データベース エンジン)
title: ToString (データベース エンジン)
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ToString
- ToString_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ToString [Database Engine]
ms.assetid: 5fc11ca5-c26d-4518-9512-67aa0270f110
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1d1460c83488f7ba708f737e7c9bb7bd46819152
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037465"
---
# <a name="tostring-database-engine"></a>ToString (データベース エンジン)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

*this* の論理的表現に基づく文字列を返します ToString から変換するとき暗黙的に呼び出されます **hierarchyid** を文字列型が発生します。 逆の役割を果たします #40 を[解析する (& a)";"データベース エンジン"&"#41;](../../t-sql/data-types/parse-database-engine.md).
  
## <a name="syntax"></a>構文  

```syntaxsql
-- Transact-SQL syntax
node.ToString  ( )
-- This is functionally equivalent to the following syntax  
-- which implicitly calls ToString():  
CAST(node AS nvarchar(4000))  
```  
  
```syntaxsql
-- CLR syntax
string ToString  ( )
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型

**SQL Server の戻り値の型 :nvarchar(4000)**
  
**CLR の戻り値の型: String**
  
## <a name="remarks"></a>解説  
階層内での論理的な位置を返します。 たとえば、`/2/1/` は、ファイル システムの次の階層構造における 4 行目 ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) を表します。
  
```sql
/        C:\  
/1/      C:\Database Files  
/2/      C:\Program Files  
/2/1/    C:\Program Files\Microsoft SQL Server  
/2/2/    C:\Program Files\Microsoft Visual Studio  
/3/      C:\Windows  
```  
  
## <a name="examples"></a>例  
  
### <a name="a-transact-sql-example-in-a-table"></a>A. テーブルでの Transact-SQL の例  
次の例では、`OrgNode` 列が、**hierarchyid** データ型の読み取り可能な文字列形式で返されます。
  
```sql
SELECT OrgNode,  
OrgNode.ToString() AS Node  
FROM HumanResources.EmployeeDemo  
ORDER BY OrgNode ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
OrgNode   Node  
0x        /  
0x58      /1/  
0x5AC0    /1/1/  
0x5B40    /1/2/  
0x5BC0    /1/3/  
0x5C20    /1/4/  
...  
```  
  
### <a name="b-converting-transact-sql-values-without-a-table"></a>B. テーブルを使用しない Transact-SQL 値の変換  
次のコード例では、`ToString` を使用して **hierarchyid** 値を文字列に変換し、`Parse` を使用して文字列値を **hierarchyid** に変換します。
  
```sql
DECLARE @StringValue AS nvarchar(4000), @hierarchyidValue AS hierarchyid  
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
  
### <a name="c-clr-example"></a>C. CLR の例  
次のコード スニペットの呼び出し、 ToString() メソッド。
  
```sql
this.ToString()  
```  
  
## <a name="see-also"></a>参照
[hierarchyid データ型メソッド リファレンス](./hierarchyid-data-type-method-reference.md)  
[階層データ (SQL Server)](../../relational-databases/hierarchical-data-sql-server.md)  
[hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
  
