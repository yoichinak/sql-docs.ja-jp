---
description: DBCC TRACESTATUS (Transact-SQL)
title: DBCC TRACESTATUS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_TRACESTATUS_TSQL
- DBCC TRACESTATUS
- TRACESTATUS_TSQL
- TRACESTATUS
dev_langs:
- TSQL
helpviewer_keywords:
- global trace flags [SQL Server]
- status information [SQL Server], trace flags
- trace flags [SQL Server], status information
- DBCC TRACESTATUS statement
- session trace flags [SQL Server]
- displaying trace flag status
ms.assetid: 9be51199-78b4-4b87-ae6e-557246b7e29a
author: pmasl
ms.author: umajay
ms.openlocfilehash: 046c8fa60fc4bc4930089d8c7e9a87a3480bff23
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126270"
---
# <a name="dbcc-tracestatus-transact-sql"></a>DBCC TRACESTATUS (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

トレース フラグの状態を表示します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```syntaxsql
DBCC TRACESTATUS ( [ [ trace# [ ,...n ] ] [ , ] [ -1 ] ] )   
[ WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
*trace#*  
状態を表示するトレース フラグの番号です。 場合 *trace #*、-1 が指定されていない場合は、セッションが有効になっているすべてのトレース フラグが表示されます。
  
*n*  
複数のトレース フラグを指定できることを示すプレースホルダーです。
  
-1  
グローバルに有効化されているトレース フラグの状態を表示します。 -1 がなく指定され、*trace #* がない場合、有効になっているすべてのグローバル トレース フラグが表示されます。
  
WITH NO_INFOMSGS  
重大度レベル 0 から 10 のすべての情報メッセージを表示しないようにします。
  
## <a name="result-sets"></a>結果セット  
次の表では、結果セットに表示される情報について説明します。
  
|列名|説明|  
|---|---|
|**TraceFlag**|トレース フラグの名前です。|  
|**状態**|トレース フラグがグローバルまたはセッションごとに ON または OFF に設定されているかどうかを示します。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|**グローバル**|トレース フラグがグローバルに設定されているかどうかを示します。<br /><br /> 1 = True<br /><br /> 0 = False|  
|**セッション**|トレース フラグがセッションに対して設定されているかどうかを示します。<br /><br /> 1 = True<br /><br /> 0 = False|  
  
DBCC TRACESTATUS はトレース フラグ番号の列と状態の列を返します。 これは、トレース フラグがオン (1)、オフ (0) のどちらになっているかを示します。 グローバル トレース フラグまたはセッション トレース フラグのどちらの状態を確認するかに応じて、トレース フラグ番号の列ヘッダーが **Global Trace Flag** または **Session Trace Flag** に設定されます。
  
## <a name="remarks"></a>解説  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、セッションとグローバルという 2 種類のトレース フラグがあります。 セッション トレース フラグは、1 つの接続についてアクティブで、その接続に対してのみ表示可能です。 グローバル トレース フラグは、サーバー レベルで設定され、サーバー上のすべての接続に対して表示可能です。
  
## <a name="permissions"></a>アクセス許可  
ロール **public** のメンバーシップが必要です。
  
## <a name="examples"></a>例  
次の例は、現在グローバルに有効化されているすべてのトレース フラグの状態を表示します。
  
```sql  
DBCC TRACESTATUS(-1);  
GO  
```  
  
次の例では、トレース フラグ `2528` と `3205` の状態を表示します。
  
```sql  
DBCC TRACESTATUS (2528, 3205);  
GO  
```  
  
次の例では、トレース フラグ `3205` がグローバルに有効になっているかどうかを表示します。
  
```sql  
DBCC TRACESTATUS (3205, -1);  
GO  
```  
  
次の例では、現在のセッションに対して有効になっているすべてのトレース フラグを一覧表示します。
  
```sql  
DBCC TRACESTATUS();  
GO  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
  
  
