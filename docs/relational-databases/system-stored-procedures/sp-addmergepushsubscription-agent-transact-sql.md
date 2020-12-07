---
description: sp_addmergepushsubscription_agent (Transact-sql)
title: sp_addmergepushsubscription_agent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergepushsubscription_agent_TSQL
- sp_addmergepushsubscription_agent
helpviewer_keywords:
- sp_addmergepushsubscription_agent
ms.assetid: 808a1925-be46-4999-8d69-b3a83010ec81
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 91131da8fe1102edf1c2d6f890ece76be440d1ff
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89529488"
---
# <a name="sp_addmergepushsubscription_agent-transact-sql"></a>sp_addmergepushsubscription_agent (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  マージパブリケーションに対するプッシュサブスクリプションの同期をスケジュールするために使用する、新しいエージェントジョブを追加します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
> [!IMPORTANT]  
>  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addmergepushsubscription_agent [ @publication =] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]   
    [ , [ @subscriber_db = ] 'subscriber_db' ]   
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]   
    [ , [ @subscriber_login = ] 'subscriber_login' ]   
    [ , [ @subscriber_password = ] 'subscriber_password' ]   
    [ , [ @publisher_security_mode = ] publisher_security_mode ]   
    [ , [ @publisher_login = ] 'publisher_login' ]   
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
    [ , [ @frequency_type = ] frequency_type ]   
    [ , [ @frequency_interval = ] frequency_interval ]   
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]   
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]   
    [ , [ @frequency_subday = ] frequency_subday ]   
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]   
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]   
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]   
    [ , [ @active_start_date = ] active_start_date ]   
    [ , [ @active_end_date = ] active_end_date ]   
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前を指定します。 *サブスクライバー* の **sysname**,、既定値は NULL です。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクリプションデータベースの名前を指定します。 *subscriber_db* は **sysname**,、既定値は NULL です。  
  
`[ @subscriber_security_mode = ] subscriber_security_mode` 同期時にサブスクライバーに接続するときに使用するセキュリティモードを示します。 *subscriber_security_mode* は **int**,、既定値は1です。 **0**の場合、認証を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 **1**の場合、Windows 認証を指定します。  
  
`[ @subscriber_login = ] 'subscriber_login'` サブスクライバーに接続して同期するときに使用するサブスクライバーログインを示します。 *subscriber_security_mode*が**0**に設定されている場合は*subscriber_login*が必要です。 *subscriber_login* は **sysname**,、既定値は NULL です。  
  
`[ @subscriber_password = ] 'subscriber_password'` 認証用のサブスクライバーパスワードを入力し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *subscriber_security_mode*が**0**に設定されている場合は*subscriber_password*が必要です。 *subscriber_password* は **sysname**,、既定値は NULL です。 サブスクライバーパスワードが使用されている場合は、自動的に暗号化されます。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @publisher_security_mode = ] publisher_security_mode` 同期時にパブリッシャーに接続するときに使用するセキュリティモードを示します。 *publisher_security_mode* は **int**,、既定値は1です。 **0**の場合、認証を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 **1**の場合、Windows 認証を指定します。  
  
`[ @publisher_login = ] 'publisher_login'` 同期時にパブリッシャーに接続するときに使用するログインを示します。 *publisher_login* は **sysname**,、既定値は NULL です。  
  
`[ @publisher_password = ] 'publisher_password'` パブリッシャーに接続するときに使用するパスワードを入力します。 *publisher_password* は **sysname**,、既定値は NULL です。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @job_login = ] 'job_login'` エージェントを実行する Windows アカウントのログインを指定します。 *job_login* は **nvarchar (257)** で、既定値は NULL です。 この Windows アカウントは、Windows 統合認証を使用する場合に、ディストリビューターへのエージェント接続、およびサブスクライバーとパブリッシャーへの接続に常に使用されます。  
  
`[ @job_password = ] 'job_password'` エージェントを実行する Windows アカウントのパスワードを指定します。 *job_password* は **sysname**であり、既定値はありません。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @job_name = ] 'job_name'` 既存のエージェントジョブの名前を指定します。 *job_name* は **sysname**で、既定値は NULL です。 このパラメーターは、新しく作成されたジョブ (既定値) ではなく、既存のジョブを使用してサブスクリプションを同期する場合にのみ指定します。 **Sysadmin**固定サーバーロールのメンバーでない場合は、 *job_name*を指定するときに*job_login*と*job_password*を指定する必要があります。  
  
`[ @frequency_type = ] frequency_type` マージエージェントをスケジュールする頻度を指定します。 *frequency_type* は **int**,、値は次のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 回|  
|**2**|オン デマンド|  
|**4**|毎日|  
|**8**|週次|  
|**16**|月単位|  
|**32**|月単位の相対|  
|**64**|自動開始|  
|**128**|繰り返し|  
|NULL (既定値)||  
  
> [!NOTE]  
>  値 **64** を指定すると、マージエージェントが連続モードで実行されます。 これは、エージェントの **-Continuous** パラメーターの設定に対応しています。 詳細については、「 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)」を参照してください。  
  
`[ @frequency_interval = ] frequency_interval` マージエージェントを実行する曜日。 *frequency_interval* は **int**,、値は次のいずれかを指定することができます。  
  
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
  
`[ @frequency_relative_interval = ] frequency_relative_interval` マージエージェントの日付を指定します。 このパラメーターは、 *frequency_type* が **32** (月単位) に設定されている場合に使用されます。 *frequency_relative_interval* は **int**,、値は次のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|First|  
|**2**|秒|  
|**4**|Third|  
|**8**|4 番目|  
|**16**|Last (最後へ)|  
|NULL (既定値)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数です。 *frequency_recurrence_factor* は **int**,、既定値は NULL です。  
  
`[ @frequency_subday = ] frequency_subday` 定義した期間中に再スケジュールする頻度を指定します。 *frequency_subday* は **int**,、値は次のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 度|  
|**2**|秒|  
|**4**|分|  
|**8**|時間|  
|NULL (既定値)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*の間隔を指定します。 *frequency_subday_interval* は **int**,、既定値は NULL です。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` マージエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day* は **int**,、既定値は NULL です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` マージエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day* は **int**,、既定値は NULL です。  
  
`[ @active_start_date = ] active_start_date` マージエージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date* は **int**,、既定値は NULL です。  
  
`[ @active_end_date = ] active_end_date` マージエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date* は **int**,、既定値は NULL です。  
  
`[ @enabled_for_syncmgr = ] 'enabled_for_syncmgr'` Windows 同期マネージャーを使用してサブスクリプションを同期できるかどうかを指定します。 *enabled_for_syncmgr* は **nvarchar (5)**,、既定値は FALSE です。 **False**の場合、サブスクリプションは同期マネージャーに登録されていません。 **True**の場合、サブスクリプションは同期マネージャーに登録され、を起動せずに同期でき [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_addmergepushsubscription_agent** は、マージレプリケーションで使用され、 [sp_addpushsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)と同様の機能を使用します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addmergepushsubscript_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addmergepushsubscription_agent**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)  
  
  
