---
description: sp_help_jobhistory (Transact-sql)
title: sp_help_jobhistory (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_jobhistory_TSQL
- sp_help_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_jobhistory
ms.assetid: a944d44e-411b-4735-8ce4-73888d4262d7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d805cfb7f6cf682e07e703e6854e25737a82b9cc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547992"
---
# <a name="sp_help_jobhistory-transact-sql"></a>sp_help_jobhistory (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マルチサーバー管理ドメインに所属するサーバーのジョブに関する情報を提供します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_jobhistory [ [ @job_id = ] job_id ]   
     [ , [ @job_name = ] 'job_name' ]   
     [ , [ @step_id = ] step_id ]   
     [ , [ @sql_message_id = ] sql_message_id ]   
     [ , [ @sql_severity = ] sql_severity ]   
     [ , [ @start_run_date = ] start_run_date ]   
     [ , [ @end_run_date = ] end_run_date ]   
     [ , [ @start_run_time = ] start_run_time ]   
     [ , [ @end_run_time = ] end_run_time ]   
     [ , [ @minimum_run_duration = ] minimum_run_duration ]   
     [ , [ @run_status = ] run_status ]   
     [ , [ @minimum_retries = ] minimum_retries ]   
     [ , [ @oldest_first = ] oldest_first ]   
     [ , [ @server = ] 'server' ]   
     [ , [ @mode = ] 'mode' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @job_id = ] job_id` ジョブの識別番号を指定します。 *job_id* は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` ジョブの名前。 *job_name* は **sysname**,、既定値は NULL です。  
  
`[ @step_id = ] step_id` ステップの識別番号。 *step_id* は **int**,、既定値は NULL です。  
  
`[ @sql_message_id = ] sql_message_id` ジョブの実行時に Microsoft SQL Server によって返されるエラーメッセージの識別番号を指定します。 *sql_message_id* は **int**,、既定値は NULL です。  
  
`[ @sql_severity = ] sql_severity` ジョブの実行時に SQL Server によって返されるエラーメッセージの重大度レベル。 *sql_severity* は **int**,、既定値は NULL です。  
  
`[ @start_run_date = ] start_run_date` ジョブが開始された日付。 *start_run_date*は **int**,、既定値は NULL です。 *start_run_date* は、YYYYMMDD 形式で入力する必要があります。ここで、YYYY は4桁の年、MM は2桁の月、DD は2桁の日の名前です。  
  
`[ @end_run_date = ] end_run_date` ジョブが完了した日付。 *end_run_date* は **int**,、既定値は NULL です。 *end_run_date*は、YYYYMMDD 形式で入力する必要があります。ここで、YYYY は4桁の年、MM は2桁の月、DD は2桁の日の名前です。  
  
`[ @start_run_time = ] start_run_time` ジョブが開始された時刻。 *start_run_time* は **int**,、既定値は NULL です。 *start_run_time*は、HHMMSS 形式で入力する必要があります。 HH は、1日の2桁の時、MM は2桁の分、SS は2桁の秒を示します。  
  
`[ @end_run_time = ] end_run_time` ジョブの実行が完了した時刻。 *end_run_time* は **int**,、既定値は NULL です。 *end_run_time*は、HHMMSS 形式で入力する必要があります。 HH は、1日の2桁の時、MM は2桁の分、SS は2桁の秒を示します。  
  
`[ @minimum_run_duration = ] minimum_run_duration` ジョブが完了するまでの時間の最小値です。 *minimum_run_duration* は **int**,、既定値は NULL です。 *minimum_run_duration*は、HHMMSS 形式で入力する必要があります。 HH は、1日の2桁の時、MM は2桁の分、SS は2桁の秒を示します。  
  
`[ @run_status = ] run_status` ジョブの実行状態です。 *run_status* は **int**,、既定値は NULL の場合、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**0**|Failed|  
|**1**|成功|  
|**2**|再試行 (ステップのみ)|  
|**3**|Canceled|  
|**4**|実行中のメッセージ|  
|**5**|Unknown|  
  
`[ @minimum_retries = ] minimum_retries` ジョブの実行を再試行する最小回数。 *minimum_retries* は **int**,、既定値は NULL です。  
  
`[ @oldest_first = ] oldest_first` 最初に最も古いジョブを使用して出力を表示するかどうかを指定します。 *oldest_first* は **int**,、既定値は **0**,、最も新しいジョブを最初に表示します。 **1** まず最も古いジョブを示します。  
  
`[ @server = ] 'server'` ジョブが実行されたサーバーの名前。 *サーバー* は **nvarchar (30)**,、既定値は NULL です。  
  
`[ @mode = ] 'mode'` SQL Server 結果セットのすべての列 (**FULL**) または列の概要を出力するかどうかを指定します。 *モード* は **varchar (7)**,、既定値は **SUMMARY**です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 実際の列の一覧は、 *モード*の値によって異なります。 最も包括的な列のセットを以下に示します。 *モード* がいっぱいになったときに返されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|履歴エントリの識別番号。|  
|**job_id**|**uniqueidentifier**|ジョブの識別番号。|  
|**job_name**|**sysname**|ジョブ名。|  
|**step_id**|**int**|ステップの識別番号 (ジョブ履歴の場合は **0** になります)。|  
|**step_name**|**sysname**|ステップ名。ジョブ履歴の場合は NULL です。|  
|**sql_message_id**|**int**|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステップの場合、コマンドの実行中に最も新しく発生した [!INCLUDE[tsql](../../includes/tsql-md.md)] エラーの番号。|  
|**sql_severity**|**int**|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステップの場合、コマンドの実行中に発生した最も重大な [!INCLUDE[tsql](../../includes/tsql-md.md)] エラーの重大度。|  
|**message**|**nvarchar(1024)**|ジョブまたはステップの履歴メッセージ。|  
|**run_status**|**int**|ジョブまたはステップの結果。|  
|**run_date**|**int**|ジョブまたはステップの実行が開始された日付。|  
|**run_time**|**int**|ジョブまたはステップの実行が開始された時刻。|  
|**run_duration**|**int**|ジョブまたはステップを実行してからの経過時間 (HHMMSS 形式)。|  
|**operator_emailed**|**nvarchar (20)**|このジョブに関して電子メールで送信されたオペレーター (ステップ履歴の場合は NULL)。|  
|**operator_netsent**|**nvarchar (20)**|このジョブに関するネットワークメッセージを送信したオペレーター (ステップ履歴の場合は NULL)。|  
|**operator_paged**|**nvarchar (20)**|このジョブに関してページングされたオペレーター (ステップ履歴の場合は NULL)。|  
|**retries_attempted**|**int**|ステップが再試行された回数 (ジョブ履歴の場合は常に 0)。|  
|**server**|**nvarchar(30)**|ステップまたはジョブを実行するサーバー。 常に (**ローカル**) です。|  
  
## <a name="remarks"></a>解説  
 **sp_help_jobhistory** は、指定したスケジュールされたジョブの履歴を含むレポートを返します。 どのパラメーターも指定しない場合は、レポートにはすべての定期ジョブの履歴が含まれます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
 **SQLAgentUserRole**データベースロールのメンバーは、自分が所有しているジョブの履歴のみを表示できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-all-job-information-for-a-job"></a>A. ジョブのすべてのジョブ情報を一覧表示する  
 次の例では、ジョブのすべてのジョブ情報を一覧表示し `NightlyBackups` ます。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_jobhistory   
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-listing-information-for-jobs-that-match-certain-conditions"></a>B. 一定の条件に一致するジョブに関する情報を一覧表示する  
 次の例では、すべての列と、失敗したジョブのすべてのジョブ情報を出力し `50100` ます。エラーメッセージ (ユーザー定義のエラーメッセージ) と重大度を指定して、失敗したジョブステップを表示し `20` ます。  
  
```  
USE msdb  
GO  
  
EXEC dbo.sp_help_jobhistory  
    @sql_message_id = 50100,  
    @sql_severity = 20,  
    @run_status = 0,  
    @mode = N'FULL' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
