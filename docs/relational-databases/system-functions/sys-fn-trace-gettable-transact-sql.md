---
description: fn_trace_gettable (Transact-sql)
title: fn_trace_gettable (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_trace_gettable
- fn_trace_gettable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_trace_gettable function
- sys.fn_trace_gettable function
ms.assetid: c2590159-6ec5-4510-81ab-e935cc4216cd
author: rothja
ms.author: jroth
ms.openlocfilehash: 85ffb20fb0ead23c8027ab9b4ba45f906fe8c097
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464749"
---
# <a name="sysfn_trace_gettable-transact-sql"></a>fn_trace_gettable (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  1つ以上のトレースファイルの内容を表形式で返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントを使用します。  
   
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_trace_gettable ( 'filename' , number_files )  
```  
  
## <a name="arguments"></a>引数  
 '*filename*'  
 読み取る最初のトレースファイルを指定します。 *ファイル名* は **nvarchar (256)**,、既定値はありません。  
  
 *number_files*  
 読み取るロールオーバーファイルの数を指定します。 この数値には、 *filename*で指定された初期ファイルが含まれます。 *number_files* は **int**です。  
  
## <a name="remarks"></a>解説  
 *Number_files*が**default**として指定されている場合、 **fn_trace_gettable**はトレースの最後に達するまですべてのロールオーバーファイルを読み取ります。 **fn_trace_gettable** は、指定されたトレースに対して有効なすべての列を含むテーブルを返します。 詳細については、「 [sp_trace_setevent &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)」を参照してください。  
  
 Fn_trace_gettable 関数はロールオーバーファイルを読み込まないことに注意してください (このオプションが *number_files* 引数を使用して指定されている場合)。元のトレースファイル名の末尾には、アンダースコアと数値が使用されます。 (これは、ファイルのロールオーバー時に自動的に追加されるアンダースコアと数字には適用されません)。回避策として、トレースファイルの名前を変更して、元のファイル名のアンダースコアを削除することができます。 たとえば、元のファイルに **Trace_Oct_5 .trc** という名前が付けられていて、ロールオーバーファイルに **Trace_Oct_5_1 .trc**という名前が付けられている場合は、ファイルの名前を **TraceOct5** と **TraceOct5_1**に変更できます。  
  
 この関数は、関数が実行されるインスタンス上でアクティブになっているトレースを読み取ることができます。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する ALTER TRACE 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-using-fn_trace_gettable-to-import-rows-from-a-trace-file"></a>A. Fn_trace_gettable を使用したトレースファイルからの行のインポート  
 次の例では、 `fn_trace_gettable` ステートメントの句内でを呼び出し `FROM` `SELECT...INTO` ます。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
### <a name="b-using-fn_trace_gettable-to-return-a-table-with-an-identity-column-that-can-be-loaded-into-a-sql-server-table"></a>B. fn_trace_gettable を使用して、SQL Server テーブルに読み込むことができる IDENTITY 列を含むテーブルを返す  
 次の例では、ステートメントの一部として関数を呼び出し `SELECT...INTO` 、 `IDENTITY` テーブルに読み込むことのできる列を含むテーブルを返し `temp_trc` ます。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENTITY(int, 1, 1) AS RowNumber, * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_trace_generateevent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
