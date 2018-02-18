---
title: "@@LOCK_TIMEOUT (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 09/19/2017
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
- '@@LOCK_TIMEOUT'
- '@@LOCK_TIMEOUT_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- timeout options [SQL Server], locks
- '@@LOCK_TIMEOUT function'
- current lock time-out setting
- locking [SQL Server], time-outs
ms.assetid: 6bf8bf97-60b8-40c1-b89d-8f5a00bcae2e
caps.latest.revision: "31"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 84b885d21e5d940e3c532eef43040ba29c2b45ea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40locktimeout-transact-sql"></a>&#x40;&#x40;LOCK_TIMEOUT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在のセッションの現在のロック タイムアウト設定をミリ秒単位で返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
@@LOCK_TIMEOUT  
```  
  
## <a name="return-types"></a>戻り値の型  
 **integer**  
  
## <a name="remarks"></a>解説  
 SET LOCK_TIMEOUT を使用して、使用されないようにブロックされているリソースが使用できるようになるまでのステートメントの最大待ち時間を設定できます。 待ち時間が LOCK_TIMEOUT の設定を超える場合、ブロックされているステートメントは自動的に取り消され、エラー メッセージがアプリケーションに返されます。  
  
 現在のセッションで SET LOCK_TIMEOUT がまだ実行されていない場合、@@LOCK_TIMEOUT は値 -1 を返します。  
  
## <a name="examples"></a>使用例  
 この例では、LOCK_TIMEOUT 値が設定されていない場合の結果セットを表示します。  
  
```  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Lock Timeout  
------------  
-1  
```  
  
 この例では、LOCK_TIMEOUT を 1,800 ミリ秒に設定し、@@LOCK_TIMEOUT を呼び出します。  
  
```  
SET LOCK_TIMEOUT 1800;  
SELECT @@LOCK_TIMEOUT AS [Lock Timeout];  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Lock Timeout  
------------  
1800          
```  
  
## <a name="see-also"></a>参照  
 [構成関数 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
