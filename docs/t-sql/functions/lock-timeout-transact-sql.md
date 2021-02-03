---
description: '&#x40;&#x40;LOCK_TIMEOUT (Transact-SQL)'
title: '@@LOCK_TIMEOUT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- '@@LOCK_TIMEOUT'
- '@@LOCK_TIMEOUT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- '@@LOCK_TIMEOUT function'
- current lock time-out setting
- locking [SQL Server], time-outs
ms.assetid: 6bf8bf97-60b8-40c1-b89d-8f5a00bcae2e
author: cawrites
ms.author: chadam
ms.openlocfilehash: 68181dbd097d0f61c8051ef5d3d113360bb52ada
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99200594"
---
# <a name="x40x40lock_timeout-transact-sql"></a>&#x40;&#x40;LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在のセッションの現在のロック タイムアウト設定をミリ秒単位で返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
@@LOCK_TIMEOUT  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 **integer**  
  
## <a name="remarks"></a>解説  
 SET LOCK_TIMEOUT を使用して、使用されないようにブロックされているリソースが使用できるようになるまでのステートメントの最大待ち時間を設定できます。 ステートメントの待機時間が LOCK_TIMEOUT の設定を超えると、ブロックされているステートメントが自動的に取り消され、エラー メッセージがアプリケーションに返されます。  
  
 現在のセッションで SET LOCK_TIMEOUT がまだ実行されていない場合、@@LOCK_TIMEOUT は値 -1 を返します。  
  
## <a name="examples"></a>例  
 この例では、LOCK_TIMEOUT 値が設定されていない場合の結果セットを示します。  
  
```sql  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 結果セットは次のようになります。  
  
```  
Lock Timeout  
------------  
-1  
```  
  
 この例では、LOCK_TIMEOUT を 1,800 ミリ秒に設定し、@@LOCK_TIMEOUT を呼び出します。  
  
```sql  
SET LOCK_TIMEOUT 1800;  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
 結果セットは次のようになります。  
  
```  
Lock Timeout  
------------  
1800          
```  
  
## <a name="see-also"></a>参照  
 [構成関数 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
