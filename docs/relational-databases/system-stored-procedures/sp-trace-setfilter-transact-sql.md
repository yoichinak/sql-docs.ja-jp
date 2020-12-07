---
description: sp_trace_setfilter (Transact-SQL)
title: sp_trace_setfilter (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_setfilter
- sp_trace_setfilter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setfilter
ms.assetid: 11e7c7ac-a581-4a64-bb15-9272d5c1f7ac
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8edccbecb7d5a44b2fc8a5eed2297498c0f94bae
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547844"
---
# <a name="sp_trace_setfilter-transact-sql"></a>sp_trace_setfilter (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  トレースにフィルターを適用します。 **sp_trace_setfilter** は、停止している既存のトレースに対してのみ実行できます (*状態* は **0**)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] このストアドプロシージャが存在しないトレースに対して実行されるか、 *状態* が **0**ではない場合、はエラーを返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントを使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_trace_setfilter [ @traceid = ] trace_id   
          , [ @columnid = ] column_id  
          , [ @logical_operator = ] logical_operator  
          , [ @comparison_operator = ] comparison_operator  
          , [ @value = ] value  
```  
  
## <a name="arguments"></a>引数  
`[ @traceid = ] trace_id` フィルターが設定されるトレースの ID を指定します。 *trace_id* は **int**,、既定値はありません。 ユーザーは、この *trace_id* 値を採用して、トレースの識別、変更、および制御を行います。  
  
`[ @columnid = ] column_id` フィルターが適用される列の ID を指定します。 *column_id* は **int**,、既定値はありません。 *Column_id*が NULL の場合、は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指定されたトレースのすべてのフィルターをクリアします。  
  
`[ @logical_operator = ] logical_operator` AND (**0**) または or (**1**) 演算子を適用するかどうかを指定します。 *logical_operator* は **int**,、既定値はありません。  
  
`[ @comparison_operator = ] comparison_operator` 実行する比較の種類を指定します。 *comparison_operator* は **int**,、既定値はありません。 このテーブルには、比較演算子とその代表的な値が含まれています。  
  
|[値]|比較演算子|  
|-----------|-------------------------|  
|**0**|= (等しい)|  
|**1**|<>  (等しくない)|  
|**2**|> (より大きい)|  
|**3**|< (より小さい)|  
|**4**|>= (以上)|  
|**5**|<= (以下)|  
|**6**|LIKE|  
|**7**|パターンに一致しない|  
  
`[ @value = ] value` フィルター処理の対象となる値を指定します。 *値*のデータ型は、フィルター選択する列のデータ型と一致している必要があります。 たとえば、フィルターが **int** データ型のオブジェクト ID 列に設定されている場合、 *値* は **int**である必要があります。 *値* が **nvarchar** または **varbinary**の場合、最大長は8000です。  
  
 比較演算子が like または NOT LIKE の場合、論理演算子には、LIKE 演算に適した "%" またはその他のフィルターを含めることができます。  
  
 *値*に null を指定すると、null 列の値を持つイベントを除外できます。 NULL では、 **0** (= equal) と **1** (<> 等しくない) 演算子のみが有効です。 この場合、これらの演算子は、[!INCLUDE[tsql](../../includes/tsql-md.md)] の IS NULL 演算子および IS NOT NULL 演算子と等価です。  
  
 列の値の範囲の間にフィルターを適用するには、 **sp_trace_setfilter** を2回実行する必要があります。これには、不等号 (' >= ') 比較演算子を使用し、もう1回は不等号 (' <= ') 演算子を使用します。  
  
 データ列のデータ型の詳細については、「 [SQL Server イベントクラスのリファレンス](../../relational-databases/event-classes/sql-server-event-class-reference.md)」を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 次の表は、このストアド プロシージャの完了時に返されるコード値を示しています。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|0|エラーなし。|  
|1|不明なエラー。|  
|2|トレースは現在実行中です。 この時点でトレースを変更すると、エラーが発生します。|  
|4|指定された列は無効です。|  
|5|指定した列にはフィルターを適用できません。 この値は **sp_trace_setfilter**からのみ返されます。|  
|6|指定した比較演算子は無効です。|  
|7|指定した論理演算子は無効です。|  
|9|指定されたトレースハンドルは無効です。|  
|13|メモリが不足しています。 指定されたアクションを実行するのに十分なメモリがない場合に返されます。|  
|16|関数は、このトレースに対して無効です。|  
  
## <a name="remarks"></a>解説  
 **sp_trace_setfilter** は、以前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンので使用できる拡張ストアドプロシージャによって以前に実行された操作の多くを実行するストアドプロシージャです [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 トレースのフィルターを作成、適用、削除、または操作するには、 **xp_trace_set \* フィルター**拡張ストアドプロシージャの代わりに**sp_trace_setfilter**を使用します。 詳細については、「 [トレースのフィルター処理](../../relational-databases/sql-trace/filter-a-trace.md)」を参照してください。  
  
 **Sp_trace_setfilter**の1回の実行で、特定の列のすべてのフィルターを同時に有効にする必要があります。 たとえば、ユーザーが [アプリケーション名] 列に2つのフィルターを適用し、[ユーザー名] 列に1つのフィルターを適用する場合、ユーザーはアプリケーション名に対して順番にフィルターを指定する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーが1つのストアドプロシージャ呼び出しでアプリケーション名に対してフィルターを指定し、その後にユーザー名のフィルターを指定した後、アプリケーション名に対して別のフィルターを指定しようとすると、エラーが返されます。  
  
 すべての SQL トレースストアドプロシージャ (**sp_trace_xx**) のパラメーターは厳密に型指定されます。 これらのパラメーターが、引数の説明で指定されている正しいデータ型で呼び出されないと、このストアド プロシージャではエラーが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは ALTER TRACE 権限を持っている必要があります。  
  
## <a name="examples"></a>例  
 次の例では、トレースに対して3つのフィルターを設定し `1` ます。 フィルター処理 `N'SQLT%'` と `N'MS%'` 操作は、 `AppName` `10` "" 比較演算子を使用して1つの列 (、値) に対して行われ `LIKE` ます。 フィルター `N'joe'` は、"`UserName`" 比較演算子を使用して別の列 (`11`、値 `EQUAL`) に適用されます。  
  
```  
sp_trace_setfilter  1, 10, 0, 6, N'SQLT%';  
sp_trace_setfilter  1, 10, 0, 6, N'MS%';  
sp_trace_setfilter  1, 11, 0, 0, N'joe';  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [SQL トレース (SQL Trace)](../../relational-databases/sql-trace/sql-trace.md)  
  
  
