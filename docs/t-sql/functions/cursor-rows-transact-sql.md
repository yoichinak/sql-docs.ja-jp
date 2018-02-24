---
title: "@@CURSOR_ROWS (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@CURSOR_ROWS'
- '@@CURSOR_ROWS_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- '@@CURSOR_ROWS function'
- cursors [SQL Server], last-opened
- last-opened cursor
- asynchronous cursors [SQL Server]
ms.assetid: 31bd7a97-7f28-42a8-ba24-24d16d22973d
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8c4c1fac4c5d9dacddfb942a3e5b9238e5be16a4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40cursorrows-transact-sql"></a>@@CURSOR_ROWS (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

接続で最後にオープンされたカーソルに現在取得されている行数を返します。パフォーマンスを向上させるために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、大きなキーセットと静的カーソルを非同期に作成できます。@@CURSOR_ROWS を呼び出すと、カーソルに取得されている行が呼び出し時にいくつ検索されたかを判別できます。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```
@@CURSOR_ROWS  
```  
  
## <a name="return-types"></a>戻り値の型
**integer**
  
## <a name="return-value"></a>戻り値  
  
|戻り値|説明|  
|---|---|
|-*m*|行がカーソルに非同期的に登録されている場合に返されます。 返される値 (-*m*) は、現在キーセットに行の数。|  
|-1|カーソルが動的な場合に返されます。 動的カーソルはすべての変更を反映するので、そのカーソルに登録されている行数は常に変化します。 したがって、登録されているすべての行を検索したかどうかは断定できません。|  
|0|オープンされているカーソルがない場合、最後にオープンされたカーソルに行が登録されていない場合、または最後にオープンされたカーソルがクローズまたは割り当てを解除されている場合に返されます。|  
|*n*|カーソルに行がすべて完全に登録されている場合に返されます。 返される値 (*n*) は、カーソルに含まれる行数の合計です。|  
  
## <a name="remarks"></a>解説  
最後のカーソルが非同期にオープンされている場合、@@CURSOR_ROWS からの戻り値は負になります。sp_configure cursor threshold が 0 より大きく、カーソル結果セットの行数がカーソルのしきい値を超える場合、キーセット カーソルまたは静的カーソルは非同期にオープンされます。
  
## <a name="examples"></a>使用例  
次の例では、カーソルを宣言し、`SELECT` を使用して `@@CURSOR_ROWS` の値を表示します。 カーソルをオープンする前の値は `0` に設定されています。`-1` の値は、カーソルのキーセットが非同期に作成されることを示します。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@CURSOR_ROWS;  
DECLARE Name_Cursor CURSOR FOR  
SELECT LastName ,@@CURSOR_ROWS FROM Person.Person;  
OPEN Name_Cursor;  
FETCH NEXT FROM Name_Cursor;  
SELECT @@CURSOR_ROWS;  
CLOSE Name_Cursor;  
DEALLOCATE Name_Cursor;  
GO             
```  
  
以下に結果セットを示します。
  
```
-----------
0  
```

```
LastName
---------------
Sanchez
```

```
-----------
-1
```  
  
## <a name="see-also"></a>参照
[カーソル関数 &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)
  
  
