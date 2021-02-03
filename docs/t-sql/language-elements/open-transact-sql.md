---
description: OPEN (Transact-SQL)
title: OPEN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- OPEN_TSQL
- OPEN
dev_langs:
- TSQL
helpviewer_keywords:
- opening cursors
- cursors [SQL Server], opening
- populating cursors [SQL Server]
- OPEN statement
- Transact-SQL cursors, opening
ms.assetid: fd1c5e3b-6045-4a42-b646-3fca76e874c1
author: cawrites
ms.author: chadam
ms.openlocfilehash: 23d3a4c306d61f2fdc7f71102a3a786dd9856941
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99191928"
---
# <a name="open-transact-sql"></a>OPEN (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] サーバー カーソルをオープンし、DECLARE CURSOR または SET *cursor_variable* ステートメントで指定される [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行することによって、カーソルを生成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
OPEN { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 GLOBAL  
 *cursor_name* でグローバル カーソルを参照することを指定します。  
  
 *cursor_name*  
 宣言済みのカーソルの名前を指定します。 *cursor_name* という名前のグローバル カーソルとローカル カーソルの両方がある場合、GLOBAL を指定すると、*cursor_name* はグローバル カーソルを参照します。GLOBAL を指定しないと、*cursor_name* はローカル カーソルを参照します。  
  
 *cursor_variable_name*  
 カーソルを参照するカーソル変数の名前を指定します。  
  
## <a name="remarks"></a>解説  
 INSENSITIVE または STATIC オプションと共にカーソルが宣言されている場合、OPEN を実行すると結果セットを格納する一時テーブルが作成されます。 結果セット内の行のサイズが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルの最大行サイズを超えると、OPEN は失敗します。 KEYSET オプションと共にカーソルが宣言されている場合、OPEN を実行するとキーセットを格納する一時テーブルが作成されます。 一時テーブルは tempdb に格納されます。  
  
 カーソルをオープンした後、最後にオープンしたカーソル内の該当する行数を受け取るには、@@CURSOR_ROWS 関数を使用します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、キーセット ドリブン カーソルまたは静的 [!INCLUDE[tsql](../../includes/tsql-md.md)] カーソルの非同期な作成はサポートされません。 [!INCLUDE[tsql](../../includes/tsql-md.md)] カーソル操作はバッチで行われます。したがって、 [!INCLUDE[tsql](../../includes/tsql-md.md)] カーソルを非同期に生成する必要はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 各カーソル操作におけるクライアントのラウンド トリップのため、待機時間が少ない OPEN が問題になるような非同期キーセット ドリブン カーソルまたは静的 API (アプリケーション プログラミング インターフェイス) サーバー カーソルは、 で引き続きサポートされます。  
  
## <a name="examples"></a>例  
 次の例では、カーソルをオープンし、すべての行をフェッチします。  
  
```sql  
DECLARE Employee_Cursor CURSOR FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN Employee_Cursor;  
  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM Employee_Cursor  
END;  
  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
```  
  
## <a name="see-also"></a>参照  
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
