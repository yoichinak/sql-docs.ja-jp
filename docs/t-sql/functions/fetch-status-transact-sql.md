---
title: "@@FETCH_STATUS (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 09/18/2017
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
- '@@FETCH_STATUS'
- '@@FETCH_STATUS_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- FETCH statement
- status information [SQL Server], FETCH
- '@@FETCH_STATUS function'
ms.assetid: 93659193-e4ff-4dfb-9043-0c4114921b91
caps.latest.revision: "39"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9bc4027eb6be9d79599cb06f7935bd2d052bb2a2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40fetchstatus-transact-sql"></a>@@FETCH_STATUS (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  接続によって現在オープンされているカーソルに対して最後に実行した FETCH ステートメントの状態を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
@@FETCH_STATUS  
```  
  
## <a name="return-type"></a>戻り値の型  
 **integer**  
  
## <a name="return-value"></a>戻り値  
  
|戻り値|説明|  
|------------------|-----------------|  
|0|FETCH ステートメントは正常に実行されました。|  
|-1|FETCH ステートメントが失敗したか、または行が結果セットに収まりません。|  
|-2|取り出した行がありません。|
|-9|カーソルがフェッチ操作を実行しません。|  
  
## <a name="remarks"></a>解説  
 @@FETCH_STATUS は接続上のすべてのカーソルに対してグローバルな変数なので、@@FETCH_STATUS を使用する際は注意してください。FETCH ステートメントを実行した後、別のカーソルに対して他の FETCH ステートメントを実行する前に、@@FETCH_STATUS の値を調べる必要があります。接続時にフェッチが実行されるまで、@@FETCH_STATUS の値は未定義です。  
  
 たとえば、ユーザーがあるカーソルからの FETCH ステートメントを実行します。次に、別のカーソルからの結果を開いて処理するためのストアド プロシージャを呼び出します。呼び出したストアド プロシージャから制御が戻された時点で、@@FETCH_STATUS は、ストアド プロシージャを呼び出す前に実行した FETCH ステートメントではなく、ストアド プロシージャで最後に実行した FETCH ステートメントを反映します。  
  
 特定のカーソルの最後のフェッチの状態を取得するには、動的管理関数 **sys.dm_exec_cursors** の **fetch_status** 列のクエリを実行します。  
  
## <a name="examples"></a>使用例  
 この例では、`@@FETCH_STATUS` を使用して `WHILE` ループでのカーソルの利用状況を制御します。  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT BusinessEntityID, JobTitle  
FROM AdventureWorks2012.HumanResources.Employee;  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [カーソル関数 &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
