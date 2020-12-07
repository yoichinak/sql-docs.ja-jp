---
description: sp_add_jobstep (Transact-SQL)
title: sp_add_jobstep (Transact-SQL)
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobstep_TSQL
- sp_add_jobstep
helpviewer_keywords:
- sp_add_jobstep
ms.assetid: 97900032-523d-49d6-9865-2734fba1c755
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 03/15/2017
ms.openlocfilehash: 8e4b24e5fcab13083c06f53868f462c3b45cc497
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753804"
---
# <a name="sp_add_jobstep-transact-sql"></a>sp_add_jobstep (Transact-SQL)

[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

SQL エージェントジョブにステップ (操作) を追加します。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

> [!IMPORTANT]
> [AZURE SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)では、ほとんどの SQL Server エージェントジョブの種類はサポートされていません。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

## <a name="syntax"></a>構文

```sql
sp_add_jobstep [ @job_id = ] job_id | [ @job_name = ] 'job_name'
     [ , [ @step_id = ] step_id ]
     { , [ @step_name = ] 'step_name' }
     [ , [ @subsystem = ] 'subsystem' ]
     [ , [ @command = ] 'command' ]
     [ , [ @additional_parameters = ] 'parameters' ]
          [ , [ @cmdexec_success_code = ] code ]
     [ , [ @on_success_action = ] success_action ]
          [ , [ @on_success_step_id = ] success_step_id ]
          [ , [ @on_fail_action = ] fail_action ]
          [ , [ @on_fail_step_id = ] fail_step_id ]
     [ , [ @server = ] 'server' ]
     [ , [ @database_name = ] 'database' ]
     [ , [ @database_user_name = ] 'user' ]
     [ , [ @retry_attempts = ] retry_attempts ]
     [ , [ @retry_interval = ] retry_interval ]
     [ , [ @os_run_priority = ] run_priority ]
     [ , [ @output_file_name = ] 'file_name' ]
     [ , [ @flags = ] flags ]
     [ , { [ @proxy_id = ] proxy_id
         | [ @proxy_name = ] 'proxy_name' } ]
```  
  
## <a name="arguments"></a>引数

`[ @job_id = ] job_id` ステップを追加するジョブの識別番号を指定します。 *job_id* は **uniqueidentifier**,、既定値は NULL です。

`[ @job_name = ] 'job_name'` ステップを追加するジョブの名前を指定します。 *job_name* は **sysname**,、既定値は NULL です。

> [!NOTE]
> *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。

`[ @step_id = ] step_id` ジョブステップのシーケンス識別番号を指定します。 ステップの識別番号は **1** から始まり、ギャップなしで増分されます。 既存のシーケンスにステップを挿入すると、シーケンス番号が自動的に調整されます。 *Step_id*が指定されていない場合は、値が指定されます。 *step_id* は **int**,、既定値は NULL です。

`[ @step_name = ] 'step_name'` ステップの名前。 *step_name* は **sysname**であり、既定値はありません。

`[ @subsystem = ] 'subsystem'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントサービスが*コマンド*を実行するために使用するサブシステム。 *サブシステム* は **nvarchar (40)**,、これらの値のいずれかを指定することができます。

|値|説明|
|-----------|-----------------|
|'**ActiveScripting**'|アクティブスクリプト<br /><br /> **\*\* 重要 \*\*** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|
|'**CmdExec**'|オペレーティング システム コマンドまたは実行可能なプログラム|
|'**Distribution**'|レプリケーションディストリビューションエージェントジョブ|
|'**Snapshot**'|レプリケーションスナップショットエージェントジョブ|
|"**ログリーダー**"|レプリケーションログリーダーエージェントジョブ|
|'**Merge**'|レプリケーション マージ エージェント ジョブ|
|'**QueueReader**'|レプリケーションキューリーダーエージェントジョブ|
|'**ANALYSISQUERY**'|Analysis Services クエリ (MDX、DMX)。|
|'**ANALYSISCOMMAND**'|Analysis Services コマンド (XMLA)|
|'**SSIS**'|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ実行|  
|'**PowerShell**'|PowerShell スクリプト|  
|'**TSQL**' (既定値)|[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント|

`[ @command = ] 'command'`*サブシステム*を介して**SQLServerAgent**サービスによって実行されるコマンドです。 *コマンド* は **nvarchar (max)**,、既定値は NULL です。 SQL Server エージェントでは、ソフトウェア プログラムを記述するときの変数と同じような柔軟性を持つトークン置換を使用できます。

> [!IMPORTANT]
> エスケープマクロには、ジョブステップで使用されるすべてのトークンが含まれている必要があります。そうでない場合、これらのジョブステップは失敗します。 さらに、トークン名をかっこで囲み、 `$` トークン構文の先頭にドル記号 () を付ける必要があります。 次に例を示します。
>
> `$(ESCAPE_` *マクロ名* `(DATE))`  

これらのトークンの詳細と、新しいトークン構文を使用するジョブステップの更新については、「 [ジョブステップでのトークンの使用](../../ssms/agent/use-tokens-in-job-steps.md)」を参照してください。

> [!IMPORTANT]
> Windows イベント ログに対して書き込みのアクセス許可を持っている Windows ユーザーであればだれでも、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの警告または WMI 警告によってアクティブ化されるジョブ ステップにアクセスできます。 このセキュリティ上のリスクを避けるために、警告によってアクティブになるジョブで使用できる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント トークンは、既定で無効になっています。 このようなトークンには、**A-DBN**、**A-SVR**、**A-ERR**、**A-SEV**、**A-MSG**、**WMI(** _property_ **)** があります。 このリリースでは、トークンの使用はすべての警告に拡張されていることに注意してください。
>
> これらのトークンを使用する必要がある場合は、まず、Administrators グループなどの信頼されている Windows セキュリティ グループのメンバーのみが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が存在するコンピューターのイベント ログに対して書き込みのアクセス許可を持っていることを確認してください。 確認したら、[オブジェクト エクスプローラー] で **[SQL Server エージェント]** を右クリックし、 **[プロパティ]** をクリックします。次に、 **[警告システム]** ページで、 **[警告に応答するすべてのジョブのトークンを置き換える]** チェック ボックスをオンにして、これらのトークンを有効にします。

`[ @additional_parameters = ] 'parameters'`[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]*パラメーター*は**ntext**,、既定値は NULL です。

`[ @cmdexec_success_code = ] code`*コマンド*が正常に実行されたことを示すために、 **CmdExec**サブシステムコマンドによって返される値。 *コード* は **int**,、既定値は **0**です。

`[ @on_success_action = ] success_action` ステップが成功した場合に実行するアクション。 *success_action* は **tinyint**で、次のいずれかの値を指定できます。
  
|値|説明 (アクション)|  
|-----------|----------------------------|  
|**1** (既定値)|成功時に終了|  
|**2**|失敗した状態で終了します。|  
|**3**|次のステップに進みます。|  
|**4**|手順に進む *on_success_step_id*|  

`[ @on_success_step_id = ] success_step_id` ステップが成功し *success_action* が **4**の場合に実行する、このジョブのステップの ID。 *success_step_id* は **int**,、既定値は **0**です。

`[ @on_fail_action = ] fail_action` ステップが失敗した場合に実行するアクション。 *fail_action* は **tinyint**で、次のいずれかの値を指定できます。

|値|説明 (アクション)|  
|-----------|----------------------------|  
|**1**|成功時に終了|  
|**2** (既定値)|失敗した状態で終了します。|  
|**3**|次のステップに進みます。|  
|**4**|手順に進む *on_fail_step_id*|  

`[ @on_fail_step_id = ] fail_step_id` ステップが失敗し、 *fail_action* が **4**の場合に実行する、このジョブのステップの ID。 *fail_step_id* は **int**,、既定値は **0**です。  

`[ @server = ] 'server'`[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]*サーバー*は**nvarchar (30)**,、既定値は NULL です。  

`[ @database_name = ] 'database'` ステップを実行するデータベースの名前です [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 *データベースのデータ* 型は **sysname**で、既定値は NULL です。この場合、 **master** データベースが使用されます。 角かっこ ([]) で囲まれた名前は使用できません。 ActiveX ジョブステップの場合、 *データベース* は、ステップで使用するスクリプト言語の名前です。  

`[ @database_user_name = ] 'user'` ステップの実行時に使用するユーザーアカウントの名前 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 *user* の部分は **sysname**で、既定値は NULL です。 *ユーザー*が NULL の場合、ステップは*データベース*のジョブ所有者のユーザーコンテキストで実行されます。  このパラメーターは、ジョブの所有者が SQL Server sysadmin である場合にのみ SQL Server エージェントに含まれます。 その場合、指定された Transact-sql ステップは、指定された SQL Server ユーザー名のコンテキストで実行されます。 ジョブの所有者が SQL Server sysadmin でない場合、Transact-sql ステップは常にこのジョブを所有するログインのコンテキストで実行され、 @database_user_name パラメーターは無視されます。  

`[ @retry_attempts = ] retry_attempts` このステップが失敗した場合に使用する再試行回数。 *retry_attempts* は **int**,、既定値は **0**,、これは再試行がないことを示します。  

`[ @retry_interval = ] retry_interval` 再試行の間隔 (分) です。 *retry_interval* は **int**,、既定値は **0,、** **0**分間隔を示します。  

`[ @os_run_priority = ] run_priority` 確保.

`[ @output_file_name = ] 'file_name'` このステップの出力が保存されるファイルの名前。 *file_name* は **nvarchar (200)**,、既定値は NULL です。 *file_name* には、[ *コマンド*] に一覧表示されているトークンを1つ以上含めることができます。 このパラメーターは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 、 **CmdExec**、 **PowerShell**、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 、またはサブシステムで実行されているコマンドでのみ有効です [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。  

`[ @flags = ] flags` は、動作を制御するオプションです。 *フラグ* は **int**,、これらの値のいずれかを指定できます。  

|値|説明|  
|-----------|-----------------|  
|**0** (既定値)|出力ファイルを上書きする|  
|**2**|出力ファイルに追加|  
|**4**|[!INCLUDE[tsql](../../includes/tsql-md.md)]ジョブステップの出力をステップ履歴に書き込む|  
|**8**|テーブルにログを書き込む (既存の履歴を上書きする)|  
|**16**|ログをテーブルに書き込む (既存の履歴に追加する)|  
|**32**|すべての出力をジョブ履歴に書き込みます。|  
|**64**|Windows イベントを作成して、Cmd jobstep が中止するシグナルとして使用する|  

`[ @proxy_id = ] proxy_id` ジョブステップを実行するプロキシの id 番号を指定します。 *proxy_id* の型は **int**で、既定値は NULL です。 *Proxy_id*が指定されておらず、 *proxy_name*が指定されておらず、 *user_name*が指定されていない場合、ジョブステップはエージェントのサービスアカウントとして実行され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  

`[ @proxy_name = ] 'proxy_name'` ジョブステップを実行するプロキシの名前を指定します。 *proxy_name* の型は **sysname**で、既定値は NULL です。 *Proxy_id*が指定されておらず、 *proxy_name*が指定されておらず、 *user_name*が指定されていない場合、ジョブステップはエージェントのサービスアカウントとして実行され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  

## <a name="return-code-values"></a>リターン コードの値

**0** (成功) または **1** (失敗)

## <a name="result-sets"></a>結果セット

なし

## <a name="remarks"></a>解説

**sp_add_jobstep** は、 **msdb** データベースから実行する必要があります。  

SQL Server Management Studio は、簡単かつ直観的な方法でジョブを管理するためのツールで、ジョブ体系の作成および管理に最適です。  

既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 別のプロキシが指定されていない限り、ジョブステップはエージェントのサービスアカウントとして実行されます。 このアカウントの要件は、 **sysadmin** 固定セキュリティロールのメンバーである必要があります。

プロキシは *proxy_name* または *proxy_id*によって識別できます。

## <a name="permissions"></a>アクセス許可

 既定では、このストアド プロシージャを実行できるのは、 **sysadmin** 固定サーバー ロールのメンバーです。 他のユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **データベースの次のいずれかの** エージェント固定データベース ロールが許可されている必要があります。

- **SQLAgentUserRole**

- **SQLAgentReaderRole**

- **SQLAgentOperatorRole**

これらのロールの権限の詳細については、「 [SQL Server エージェントの固定データベース ロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。

ジョブステップの作成者は、ジョブステップのプロキシへのアクセス権を持っている必要があります。 **Sysadmin**固定サーバーロールのメンバーは、すべてのプロキシにアクセスできます。 他のユーザーには、明示的にプロキシへのアクセスを許可する必要があります。

## <a name="examples"></a>例

次の例では、Sales データベースのデータベースアクセスを読み取り専用に変更するジョブステップを作成します。 さらに、この例では、5分間待機した後に再試行が5回発生する5回の再試行が指定されています。

> [!NOTE]
> この例では、ジョブが既に存在していることを前提としてい `Weekly Sales Data Backup` ます。  

```sql
USE msdb;
GO
EXEC sp_add_jobstep
    @job_name = N'Weekly Sales Data Backup',
    @step_name = N'Set database to read only',
    @subsystem = N'TSQL',
    @command = N'ALTER DATABASE SALES SET READ_ONLY',
    @retry_attempts = 5,
    @retry_interval = 5 ;
GO
```

## <a name="next-steps"></a>次のステップ

- [ジョブの表示または変更](../../ssms/agent/view-or-modify-jobs.md)
- [sp_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-job-transact-sql.md)
- [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)
- [sp_delete_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)
- [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)
- [sp_help_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md)
- [sp_update_jobstep &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)
- [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)