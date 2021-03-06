---
description: sys.fn_trace_getfilterinfo (Transact-sql)
title: sys.fn_trace_getfilterinfo (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- fn_trace_getfilterinfo
- fn_trace_getfilterinfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], filters
- sys.fn_trace_getfilterinfo function
- filters [SQL Server], traces
- fn_trace_getfilterinfo function
ms.assetid: 09fe4a28-ff8a-4655-9da1-4654d5bc514d
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 7e20ee696ab4d371c6b12dfb24bd5433170080ba
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99200369"
---
# <a name="sysfn_trace_getfilterinfo-transact-sql"></a>sys.fn_trace_getfilterinfo (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたトレースに適用されたフィルターに関する情報を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントを使用します。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_trace_getfilterinfo ( trace_id )  
```  
  
## <a name="arguments"></a>引数  
 *trace_id*  
 トレースの ID を示します。 *trace_id* は **int**,、既定値はありません。  
  
## <a name="tables-returned"></a>返されるテーブル  
 次の情報を返します。 列の詳細については、「 [sp_trace_setfilter &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**columnid**|**int**|フィルターが適用される列の ID。|  
|**logical_operator**|**int**|AND または OR 演算子を適用するかどうかを指定します。|  
|**comparison_operator**|**int**|実行する比較の種類を指定します。<br /><br /> 0 = 等しい<br /><br /> 1 = 等しくない<br /><br /> 2 = より大きい<br /><br /> 3 = より小さい<br /><br /> 4 = 以上<br /><br /> 5 = 以下<br /><br /> 6 = 一致<br /><br /> 7 = 一致しない|  
|**value**|**sql_variant**|フィルターを適用するときに使用する値を示します。|  
  
## <a name="remarks"></a>コメント  
 ユーザーは *trace_id* 値を設定して、トレースの識別、変更、および制御を行います。 特定のトレースの ID が渡された場合、 **fn_trace_getfilterinfo** はそのトレースに関するすべてのフィルターに関する情報を返します。 指定されたトレースにフィルターがない場合、空の行セットが返されます。 無効な ID が渡された場合、空の行セットが返されます。 トレースに関する同様の情報については、「 [sys.fn_trace_getinfo &#40;transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する ALTER TRACE 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、トレース番号 2 のすべてのフィルターに関する情報を返します。  
  
```  
SELECT * FROM fn_trace_getfilterinfo(2) ;  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [トレースの作成 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_generateevent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [sys.fn_trace_geteventinfo &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [sys.fn_trace_gettable &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)  
  
  
