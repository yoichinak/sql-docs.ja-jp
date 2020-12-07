---
description: sp_trace_create (Transact-SQL)
title: sp_trace_create (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_create_TSQL
- sp_trace_create
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_create
ms.assetid: f3a43597-4c5a-4520-bcab-becdbbf81d2e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 47e16f40b7cdd9ea9c65d3262487a7a68c8cb6ff
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547332"
---
# <a name="sp_trace_create-transact-sql"></a>sp_trace_create (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  トレース定義を作成します。 新しいトレースは停止状態になります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに拡張イベントを使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_trace_create [ @traceid = ] trace_id OUTPUT   
          , [ @options = ] option_value   
          , [ @tracefile = ] 'trace_file'   
     [ , [ @maxfilesize = ] max_file_size ]  
     [ , [ @stoptime = ] 'stop_time' ]  
     [ , [ @filecount = ] 'max_rollover_files' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @traceid = ] trace_id` によって新しいトレースに割り当てられた番号を指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 ユーザー指定の入力はすべて無視されます。 *trace_id* は **int**,、既定値は NULL です。 ユーザーは、 *trace_id* 値を使って、このストアドプロシージャで定義されているトレースを識別、変更、および制御します。  
  
`[ @options = ] option_value` トレースに対して設定されたオプションを指定します。 *option_value* は **int**,、既定値はありません。 ユーザーは複数のオプションの組み合わせを選択することもできます。これにはオプションの合計値を指定します。 たとえば、TRACE_FILE_ROLLOVER と SHUTDOWN_ON_ERROR の両方のオプションをオンにするには、 *option_value*に**6**を指定します。  
  
 次の表に、オプション、説明、およびそれらの値を示します。  
  
|オプション名|オプション値|説明|  
|-----------------|------------------|-----------------|  
|TRACE_FILE_ROLLOVER|**2**|*Max_file_size*に達すると、現在のトレースファイルが閉じられ、新しいファイルが作成されることを指定します。 新しいレコードはすべて新しいファイルに書き込まれます。 新しいファイルは前のファイルと同じ名前になりますが、シーケンスを示すために整数が追加されます。 たとえば、元のトレース ファイルの名前が filename.trc の場合、次のトレース ファイルの名前は順に filename_1.trc、filename_2.trc となります。<br /><br /> ロールオーバートレースファイルがさらに作成されると、ファイル名に付加された整数値が順番に増加します。<br /><br /> *Max_file_size*の値を指定せずにこのオプションを指定した場合、SQL Server は*MAX_FILE_SIZE* (5 MB) の既定値を使用します。|  
|SHUTDOWN_ON_ERROR|**4**|なんらかの理由によりトレースをファイルに書き込めない場合、SQL Server はシャットダウンします。 このオプションは、セキュリティ監査トレースを実行するときに役立ちます。|  
|TRACE_PRODUCE_BLACKBOX|**8**|サーバーによって生成されるトレース情報のうち、最後の 5 MB のレコードをサーバーが保存するように指定します。 TRACE_PRODUCE_BLACKBOX は、他のすべてのオプションと互換性がありません。|  
  
`[ @tracefile = ] 'trace_file'` トレースを書き込む場所とファイル名を指定します。 *trace_file* は **nvarchar (245)** で、既定値はありません。 *trace_file*は、ローカルディレクトリ (n ' C:\MSSQL\Trace\trace.trc ' など)、または共有またはパスへの UNC (n ' \\ \\ *Servername* \\ *Sharename* \\ *directory*/.trc ') のいずれかになります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、すべてのトレースファイル名に **.trc** 拡張子が追加されます。 TRACE_FILE_ROLLOVER オプションと *max_file_size* を指定した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元のトレースファイルのサイズが最大値に達すると、によって新しいトレースファイルが作成されます。 新しいファイルには元のファイルと同じ名前が付けられますが、_*n* が追加され、そのシーケンスが **1**から始まります。 たとえば、最初のトレースファイルの名前が**filename .trc**の場合、2番目のトレースファイルには filename_1 .trc という名前が付けられ**ます。**  
  
 TRACE_FILE_ROLLOVER オプションを使用する場合、元のトレース ファイル名にアンダースコア文字を使用しないことをお勧めします。 アンダースコアを使用する場合、次の動作が発生します。  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、ロールオーバーファイルを自動的に読み込むことも、プロンプトを表示することもありません (これらのファイルのロールオーバーオプションのいずれかが構成されている場合)。  
  
-   Fn_trace_gettable 関数は、元のファイル名がアンダースコアと数値で終わる、ロールオーバーファイル ( *number_files* 引数を使用して指定されている場合) を読み込みません。 ただし、この状況は、ファイルがロールオーバーされるときに自動的に追加されたアンダースコアおよび数値については該当しません。  
  
> [!NOTE]  
>  このような動作に対処するには、元のファイル名のアンダースコアを削除してトレース ファイルの名前を変更します。 たとえば、元のファイルに**my_trace .trc**という名前が付けられ、ロールオーバーファイルに**my_trace_1 .trc**という名前が付けられている場合は、でファイルを開く前に、ファイルの名前を**mytrace. .trc**と**mytrace_1 .trc**に変更できます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]  
  
 TRACE_PRODUCE_BLACKBOX オプションを使用する場合、 *trace_file*を指定することはできません。  
  
`[ @maxfilesize = ] max_file_size` トレースファイルが拡張できる最大サイズを mb 単位で指定します。 *max_file_size* は **bigint**,、既定値は **5**です。  
  
 TRACE_FILE_ROLLOVER オプションを指定せずにこのパラメーターを指定した場合、使用されたディスク領域が *max_file_size*で指定した量を超えると、トレースによってファイルへの記録が停止します。  
  
`[ @stoptime = ] 'stop_time'` トレースを停止する日付と時刻を指定します。 *stop_time* は **datetime**,、既定値は NULL です。 この値を NULL にすると、トレースを手動で停止するか、サーバーがシャットダウンするまで、トレースは実行されます。  
  
 *Stop_time*と*max_file_size*の両方が指定され、TRACE_FILE_ROLLOVER が指定されていない場合、指定された停止時刻または最大ファイルサイズに達したときに、トレースの最上部に達します。 *Stop_time*、 *max_file_size*、および TRACE_FILE_ROLLOVER を指定した場合、トレースはドライブをいっぱいにしないと仮定して、指定した停止時刻にトレースが停止します。  
  
`[ @filecount = ] 'max_rollover_files'` 同じ基本ファイル名で保持する最大数またはトレースファイルを指定します。 *max_rollover_files* は **int**で、1より大きい値です。 このパラメーターは、TRACE_FILE_ROLLOVER オプションを指定した場合のみ有効です。 *Max_rollover_files*が指定されている場合、では、新しいトレースファイル [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を開く前に最も古いトレースファイルを削除することで、 *max_rollover_files*のトレースファイルを保持しません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ベースファイル名に番号を追加して、トレースファイルの経過期間を追跡します。  
  
 たとえば、 *trace_file* パラメーターが "c:\mytrace" として指定されている場合、"c:\ mytrace_123 .trc" という名前のファイルは、"c:\ mytrace_124 .trc" という名前のファイルよりも古いものになります。 *Max_rollover_files*が2に設定されている場合、トレースファイル "c:\ mytrace_125 .trc" を作成する前に、SQL Server ファイル "c:\ mytrace_123" を削除します。  
  
 では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、各ファイルの削除のみが試行され、別のプロセスによって使用されているファイルは削除できないことに注意してください。 このため、トレースの実行中に別のアプリケーションによってトレース ファイルが使用されている場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではそれらのトレース ファイルがファイル システムに残されることがあります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 次の表は、このストアド プロシージャの完了時に返されるコード値を示しています。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|0|エラーなし。|  
|1|不明なエラー。|  
|10|オプションが無効です。 指定したオプションが一致しない場合に返されます。|  
|12|ファイルが作成されていない。|  
|13|メモリが不足しています。 指定されたアクションを実行するのに十分なメモリがない場合に返されます。|  
|14|停止時刻が無効です。 指定された停止時刻が既に発生した場合に返されます。|  
|15|パラメーターが無効。 ユーザーが互換性のないパラメーターを指定した場合に返されます。|  
  
## <a name="remarks"></a>解説  
 **sp_trace_create**は、以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンの SQL Server で使用できる拡張ストアドプロシージャ**xp_trace_ \* **によって以前に実行された操作の多くを実行するストアドプロシージャです。 ではなく **sp_trace_create** を使用します。  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_setqueuecreateinfo**  
  
-   **xp_trace_setqueuedestination**  
  
 **sp_trace_create** では、トレース定義のみが作成されます。 このストアド プロシージャを使用してトレースを開始したり変更することはできません。  
  
 すべての SQL トレースストアドプロシージャ (**sp_trace_xx**) のパラメーターは厳密に型指定されます。 これらのパラメーターを、引数の説明で指定されている正しいデータ型で指定しないと、このストアド プロシージャではエラーが返されます。  
  
 **Sp_trace_create**の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスアカウントには、トレースファイルフォルダーに対する書き込みアクセス許可が必要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービスアカウントが、トレースファイルが配置されているコンピューターの管理者でない場合は、サービスアカウントに対する書き込み権限を明示的に付与する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
> [!NOTE]  
>  **Fn_trace_gettable**システム関数を使用すると、 **sp_trace_create**で作成されたトレースファイルをテーブルに自動的に読み込むことができます。 このシステム関数の使用方法の詳細については、「 [sys. fn_trace_gettable &#40;transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)」を参照してください。  
  
 トレース ストアド プロシージャを使用した例については、「[トレースの作成 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)」を参照してください。  
  
 **TRACE_PRODUCE_BLACKBOX** には次の特性があります。  
  
-   ロールオーバートレースです。 既定の *file_count* は2ですが、 *filecount* オプションを使用してユーザーがオーバーライドできます。  
  
-   他のトレースと同様に既定の *file_size* は 5 MB であり、変更できます。  
  
-   ファイル名を指定することはできません。 ファイルは次の形式で保存されます: **N '%SQLDIR%\MSSQL\DATA\blackbox.trc '**  
  
-   トレースには、次のイベントとその列のみが含まれています。  
  
    -   **RPC starting**  
  
    -   **バッチの開始**  
  
    -   **Exception**  
  
    -   **気**  
  
-   このトレースからイベントまたは列を追加または削除することはできません。  
  
-   このトレースにフィルターを指定することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは ALTER TRACE 権限を持っている必要があります。  
  
## <a name="see-also"></a>参照  
 [sp_trace_generateevent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [SQL トレース (SQL Trace)](../../relational-databases/sql-trace/sql-trace.md)  
  
  
