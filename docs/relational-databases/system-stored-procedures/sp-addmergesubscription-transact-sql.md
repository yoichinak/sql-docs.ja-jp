---
description: sp_addmergesubscription (Transact-sql)
title: sp_addmergesubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergesubscription_TSQL
- sp_addmergesubscription
helpviewer_keywords:
- sp_addmergesubscription
ms.assetid: a191d817-0132-49ff-93ca-76f13e609b38
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d89340dfb073548378e8d4a9eb4929f836a2bbb9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89529865"
---
# <a name="sp_addmergesubscription-transact-sql"></a>sp_addmergesubscription (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  プッシュ マージ サブスクリプションまたはプル マージ サブスクリプションを作成します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addmergesubscription [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @subscriber_type= ] 'subscriber_type' ]  
    [ , [ @subscription_priority= ] subscription_priority ]  
    [ , [ @sync_type= ] 'sync_type' ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @optional_command_line= ] 'optional_command_line' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @enabled_for_syncmgr= ] 'enabled_for_syncmgr' ]  
    [ , [ @offloadagent= ] remote_agent_activation]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @use_interactive_resolver= ] 'use_interactive_resolver' ]  
    [ , [ @merge_job_name= ] 'merge_job_name' ]  
    [ , [ @hostname = ] 'hostname'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。 パブリケーションは既に存在している必要があります。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前を指定します。 *サブスクライバー* の **sysname**,、既定値は NULL です。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクリプションデータベースの名前を指定します。 *subscriber_db*は **sysname**,、既定値は NULL です。  
  
`[ @subscription_type = ] 'subscription_type'` サブスクリプションの種類を示します。 *subscription_type*は **nvarchar (15)**,、既定値は PUSH です。 **プッシュ**の場合、プッシュサブスクリプションが追加され、マージエージェントがディストリビューターに追加されます。 **プル**の場合、ディストリビューターでマージエージェントを追加せずにプルサブスクリプションが追加されます。  
  
> [!NOTE]  
>  匿名サブスクリプションでは、このストアドプロシージャを使用する必要はありません。  
  
`[ @subscriber_type = ] 'subscriber_type'` サブスクライバーの種類を示します。 *subscriber_type*は **nvarchar (15)** で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**local** (既定値)|パブリッシャーだけが認識しているサブスクライバー。|  
|**global**|すべてのサーバーが認識しているサブスクライバー。|  
  
 以降のバージョンでは [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 、ローカルサブスクリプションはクライアントサブスクリプションと呼ばれ、グローバルサブスクリプションはサーバーサブスクリプションと呼ばれます。  
  
`[ @subscription_priority = ] subscription_priority` サブスクリプションの優先度を示す数値です。 *subscription_priority*は **real**で、既定値は NULL です。 ローカルサブスクリプションと匿名サブスクリプションの場合、優先度は0.0 です。 グローバル サブスクリプションの場合は、優先度を 100.0 未満にする必要があります。  
  
`[ @sync_type = ] 'sync_type'` サブスクリプションの同期の種類を示します。 *sync_type*は **nvarchar (15)**,、既定値は **automatic**です。 **Automatic**または**none**を指定できます。 **自動**の場合、パブリッシュされたテーブルのスキーマと初期データが最初にサブスクライバーに転送されます。 存在しない場合は、パブリッシュされたテーブルのスキーマと初期データがサブスクライバーに既に存在し **ていると**見なされます。 システム テーブルとデータは常に転送されます。  
  
> [!NOTE]  
>  値を **none**に指定しないことをお勧めします。  
  
`[ @frequency_type = ] frequency_type` マージエージェントがいつ実行されるかを示す値です。 *frequency_type* は **int**,、値は次のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 度|  
|**4**|毎日|  
|**8**|週次|  
|"**10**"|月単位|  
|**20**|frequency_interval を基準とした月単位|  
|**40**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの起動時|  
|NULL (既定値)||  
  
`[ @frequency_interval = ] frequency_interval` マージエージェントが実行される日または日。 *frequency_interval* は **int**,、値は次のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|土曜日|  
|**2**|月曜日|  
|**3**|Tuesday|  
|**4**|水曜日|  
|**5**|Thursday|  
|**6**|金曜日|  
|**7**|土曜日|  
|**8**|日間|  
|**9**|平日|  
|"**10**"|週末|  
|NULL (既定値)||  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` スケジュールされたマージの実行間隔を月単位で指定します。 *frequency_relative_interval* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|First|  
|**2**|秒|  
|**4**|Third|  
|**8**|4 番目|  
|**16**|Last (最後へ)|  
|NULL (既定値)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数です。 *frequency_recurrence_factor*は **int**,、既定値は NULL です。  
  
`[ @frequency_subday = ] frequency_subday`*Frequency_subday_interval*の単位です。 *frequency_subday* は **int**,、値は次のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 度|  
|**2**|秒|  
|**4**|分|  
|**8**|時間|  
|NULL (既定値)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 各マージ間で *frequency_subday* が発生する頻度を示します。 *frequency_subday_interval* は **int**,、既定値は NULL です。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` マージエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day* は **int**,、既定値は NULL です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` マージエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day* は **int**,、既定値は NULL です。  
  
`[ @active_start_date = ] active_start_date` マージエージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date* は **int**,、既定値は NULL です。  
  
`[ @active_end_date = ] active_end_date` マージエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date* は **int**,、既定値は NULL です。  
  
`[ @optional_command_line = ] 'optional_command_line'` 実行するオプションのコマンドプロンプトを指定します。 *optional_command_line*は **nvarchar (4000)**,、既定値は NULL です。 このパラメーターを使用して、出力をキャプチャしてファイルに保存するコマンドを追加したり、構成ファイルや属性を指定できます。  
  
`[ @description = ] 'description'` このマージサブスクリプションの簡単な説明を示します。 *説明*は **nvarchar (255)**,、既定値は NULL です。 この値は、レプリケーションモニターの [ **フレンドリ名** ] 列に表示されます。この列を使用して、監視されるパブリケーションのサブスクリプションを並べ替えることができます。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'` Windows 同期マネージャーを使用してサブスクリプションを同期できるかどうかを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] ます。 *enabled_for_syncmgr* は **nvarchar (5)**,、既定値は FALSE です。 **False**の場合、サブスクリプションは同期マネージャーに登録されていません。 **True**の場合、サブスクリプションは同期マネージャーに登録され、を起動せずに同期でき [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。  
  
`[ @offloadagent = ] remote_agent_activation` エージェントをリモートでアクティブ化できることを指定します。 *remote_agent_activation* の部分は **bit** で、既定値は **0**です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のためだけに保持されています。  
  
`[ @offloadserver = ] 'remote_agent_server_name'` リモートエージェントのアクティブ化に使用するサーバーのネットワーク名を指定します。 *remote_agent_server_name*は **sysname**,、既定値は NULL です。  
  
`[ @use_interactive_resolver = ] 'use_interactive_resolver'` 対話的な解決を可能にするすべてのアーティクルについて、対話形式で競合を解決できます。 *use_interactive_resolver* は **nvarchar (5)**,、既定値は FALSE です。  
  
`[ @merge_job_name = ] 'merge_job_name'`* \@ Merge_job_name*パラメーターは推奨されていないため、設定できません。 *merge_job_name* は **sysname**,、既定値は NULL です。  
  
`[ @hostname = ] 'hostname'` パラメーター化されたフィルターの WHERE 句でこの関数を使用する場合に、 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) によって返される値をオーバーライドします。 *Hostname* は **sysname**,、既定値は NULL です。  
  
> [!IMPORTANT]  
>  パラメーター化された行フィルター句では列名に関数を適用しないことをお勧めします。これは、 `LEFT([MyColumn]) = SUSER_SNAME()`のように指定すると、パフォーマンスに問題が生じるためです。 フィルター句で [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) を使用し、HOST_NAME の値をオーバーライドする場合は、 [convert](../../t-sql/functions/cast-and-convert-transact-sql.md)を使用してデータ型を変換する必要がある場合があります。 このようなケースの推奨事項の詳細については、「[Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」の「HOST_NAME() 値のオーバーライド」をご覧ください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_addmergesubscription** は、マージレプリケーションで使用します。  
  
 プッシュサブスクリプションを作成するために**sysadmin**固定サーバーロールのメンバーによって**sp_addmergesubscription**が実行されると、マージエージェントジョブが暗黙的に作成され、エージェントサービスアカウントで実行され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 [Sp_addmergepushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)を実行し、 ** \@ job_login**と** \@ job_password**のために、エージェント固有の別の Windows アカウントの資格情報を指定することをお勧めします。 詳細については、「 [レプリケーション エージェント セキュリティ モデル](../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergesubscription-_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addmergesubscription**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [インタラクティブな競合解決](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_changemergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
