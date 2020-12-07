---
description: '&#x40;&#x40;FETCH_STATUS (Transact-SQL)'
title: FETCH_STATUS (Transact-SQL)
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@FETCH_STATUS'
- '@@FETCH_STATUS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- FETCH statement
- status information [SQL Server], FETCH
- '@@FETCH_STATUS function'
ms.assetid: 93659193-e4ff-4dfb-9043-0c4114921b91
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4e8e3c851b411be330d60eb5733d94614c644fbb
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91117089"
---
# <a name="x40x40fetch_status-transact-sql"></a>&#x40;&#x40;FETCH_STATUS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

この館数は、接続によって現在オープンされているカーソルに対して最後に実行した FETCH ステートメントの状態を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
@@FETCH_STATUS  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-type"></a>戻り値の型  
 **integer**  
  
## <a name="return-value"></a>戻り値  
  
|戻り値|説明|  
|------------------|-----------------|  
|&nbsp;0|FETCH ステートメントは正常に実行されました。|  
|-1|FETCH ステートメントが失敗したか、または行が結果セットに収まりません。|  
|-2|フェッチした行がありません。|
|-9|カーソルはフェッチ操作を実行しません。|  
  
## <a name="remarks"></a>注釈  
`@@FETCH_STATUS` は接続時のすべてのカーソルに対してグローバルであるため、慎重に使用してください。 FETCH ステートメントを実行した後、別のカーソルに対して他の FETCH ステートメントを実行する前に、`@@FETCH_STATUS` を調べる必要があります。 接続時にフェッチが実行されるまで、`@@FETCH_STATUS` は未定義です。  
  
たとえば、ユーザーがあるカーソルからの FETCH ステートメントを実行します。次に、別のカーソルからの結果を開いて処理するためのストアド プロシージャを呼び出します。 呼び出したストアド プロシージャから制御が戻された時点で、`@@FETCH_STATUS` は、ストアド プロシージャを呼び出す前に実行された FETCH ステートメントではなく、ストアド プロシージャ内で最後に実行された FETCH ステートメントを反映します。  
  
特定のカーソルの最後のフェッチの状態を取得するには、動的管理関数 **sys.dm_exec_cursors** の **fetch_status** 列のクエリを実行します。  
  
## <a name="examples"></a>例  
この例では、`@@FETCH_STATUS` を使用して `WHILE` ループ内のカーソルの動作を制御します。  
  
```sql  
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
  
## <a name="see-also"></a>関連項目  
 [カーソル関数 &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
