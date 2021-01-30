---
description: sp_trace_setstatus (Transact-sql)
title: sp_trace_setstatus (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_trace_setstatus_TSQL
- sp_trace_setstatus
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setstatus
ms.assetid: 29e7a7d7-b9c1-414a-968a-fc247769750d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 69090ce81bf7a70d28cf12959c412d88f270cfdd
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99209704"
---
# <a name="sp_trace_setstatus-transact-sql"></a>sp_trace_setstatus (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定したトレースの現在の状態を変更します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントを使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_trace_setstatus [ @traceid = ] trace_id , [ @status = ] status  
```  
  
## <a name="arguments"></a>引数  
`[ @traceid = ] trace_id` 変更するトレースの ID を指定します。 *trace_id* は **int**,、既定値はありません。 ユーザーは、この *trace_id* 値を採用して、トレースの識別、変更、および制御を行います。 *Trace_id* の取得の詳細については、「 [transact-sql&#41;&#40;sys.fn_trace_getinfo](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)」を参照してください。  
  
`[ @status = ] status` トレースに実装するアクションを指定します。 *状態* は **int**,、既定値はありません。  
  
 次の表に、指定できる状態を示します。  
  
|状態|説明|  
|------------|-----------------|  
|**0**|指定されたトレースを停止します。|  
|**1**|指定されたトレースを開始します。|  
|**2**|指定されたトレースを閉じ、その定義をサーバーから削除します。|  
  
> [!NOTE]  
>  トレースを閉じるには、最初にそのトレースを停止する必要があります。 トレースを表示するには、最初にそのトレースを停止して閉じる必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 次の表は、このストアド プロシージャの完了時に返されるコード値を示しています。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|**0**|エラーなし。|  
|**1**|不明なエラー。|  
|**8**|指定した状態は無効です。|  
|**9**|指定されたトレースハンドルは無効です。|  
|**13**|メモリが不足しています。 指定されたアクションを実行するのに十分なメモリがない場合に返されます。|  
  
 トレースが既に指定された状態にある場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は **0** を返します。  
  
## <a name="remarks"></a>コメント  
 すべての SQL トレースストアドプロシージャ (**sp_trace_xx**) のパラメーターは厳密に型指定されます。 これらのパラメーターを、引数の説明で指定されている正しいデータ型で指定しないと、このストアド プロシージャではエラーが返されます。  
  
 トレース ストアド プロシージャを使用した例については、「[トレースの作成 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは ALTER TRACE 権限を持っている必要があります。  
  
## <a name="see-also"></a>参照  
 [sys.fn_trace_geteventinfo &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sp_trace_generateevent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [SQL トレース (SQL Trace)](../../relational-databases/sql-trace/sql-trace.md)  
  
  
