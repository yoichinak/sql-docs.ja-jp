---
title: sp_MSchange_snapshot_agent_properties (T-sql)
description: SQL Server レプリケーションに使用するスナップショットエージェントのプロパティを変更するために使用される sp_MSchange_snapshot_agent_properties ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_snapshot_agent_properties_TSQL
- sp_MSchange_snapshot_agent_properties
helpviewer_keywords:
- sp_MSchange_snapshot_agent_properties
ms.assetid: 7947a788-3fd7-469f-84db-b03ba89a153c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2baf36e4f2eb4d4b16fa441969fdbbb6ba4f1e10
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535079"
---
# <a name="sp_mschange_snapshot_agent_properties-transact-sql"></a>sp_MSchange_snapshot_agent_properties (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  以降のバージョンのディストリビューターで実行されるスナップショットエージェントジョブのプロパティを変更し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ます。 このストアドプロシージャは、パブリッシャーがのインスタンスで実行されている場合に、プロパティを変更するために使用し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ます。 このストアドプロシージャは、ディストリビューター側のディストリビューションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_MSchange_snapshot_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @frequency_type= ] frequency_type  
        , [ @frequency_interval= ] frequency_interval  
        , [ @frequency_subday= ] frequency_subday  
        , [ @frequency_subday_interval= ] frequency_subday_interval  
        , [ @frequency_relative_interval= ] frequency_relative_interval  
        , [ @frequency_recurrence_factor= ] frequency_recurrence_factor  
        , [ @active_start_date= ] active_start_date  
        , [ @active_end_date= ] active_end_date  
        , [ @active_start_time_of_day= ] active_start_time_of_day  
        , [ @active_end_time_of_day= ] active_end_time_of_day  
        , [ @snapshot_job_name = ] 'snapshot_agent_name'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher* は **sysname**で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` パブリケーションデータベースの名前を指定します。 *publisher_db* は **sysname**であり、既定値はありません。  
  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @frequency_type = ] frequency_type` スナップショットエージェントを実行する頻度を指定します。 *frequency_type* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 度|  
|**2**|オン デマンド|  
|**4**|毎日|  
|**8**|週次|  
|"**10**"|月単位|  
|**20**|frequency_interval を基準とした月単位|  
|**40**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの起動時|  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*によって設定された頻度に適用する値を指定します。 *frequency_interval* は **int**,、既定値はありません。  
  
`[ @frequency_subday = ] frequency_subday`*Freq_subday_interval*の単位です。 *frequency_subday* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 度|  
|**2**|秒|  
|**4**|分|  
|**8**|時間|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*の間隔を指定します。 *frequency_subday_interval* は **int**,、既定値はありません。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` スナップショットエージェントが実行される日付を指定します。 *frequency_relative_interval* は **int**,、既定値はありません。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数です。 *frequency_recurrence_factor* は **int**,、既定値はありません。  
  
`[ @active_start_date = ] active_start_date` スナップショットエージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date* は **int**,、既定値はありません。  
  
`[ @active_end_date = ] active_end_date` スナップショットエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date* は **int**,、既定値はありません。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` スナップショットエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day* は **int**,、既定値はありません。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` スナップショットエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day* は **int**,、既定値はありません。  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'` 既存のジョブが使用されている場合は、既存のスナップショットエージェントジョブ名の名前を指定します。 *snapshot_agent_name* は **nvarchar (100)**,、既定値はありません。  
  
`[ @publisher_security_mode = ] publisher_security_mode` パブリッシャーに接続するときにエージェントが使用するセキュリティモードを示します。 *publisher_security_mode* は **int**,、既定値はありません。 **0** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は認証を、 **1** は Windows 認証を指定します。 以外のパブリッシャーには、値 **0** を指定する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` パブリッシャーに接続するときに使用するログインを示します。 *publisher_login* は **sysname**であり、既定値はありません。 *publisher_security_mode*が**0**の場合は*publisher_login*を指定する必要があります。 *Publisher_login*が NULL で、パブリッシャー *_ * * security_mode*が**1**の場合、 *job_login*で指定された Windows アカウントがパブリッシャーに接続するときに使用されます。  
  
`[ @publisher_password = ] 'publisher_password'` パブリッシャーに接続するときに使用するパスワードを入力します。 *publisher_password* は **nvarchar (524)**,、既定値はありません。  
  
> [!IMPORTANT]  
>  認証情報をスクリプトファイルに保存しないでください。 セキュリティを強化するために、実行時にログイン名とパスワードを指定することをお勧めします。  
  
`[ @job_login = ] 'job_login'` エージェントを実行する Windows アカウントのログインを指定します。 *job_login* は **nvarchar (257)**,、既定値はありません。 この Windows アカウントは、ディストリビューターへのエージェント接続に常に使用されます。 新しいスナップショットエージェントジョブを作成するときに、このパラメーターを指定する必要があります。 *これは、以外* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のでは変更できません。*パブリッシャー。*  
  
`[ @job_password = ] 'job_password'` エージェントを実行する Windows アカウントのパスワードを指定します。 *job_password* は **sysname**であり、既定値はありません。 新しいスナップショットエージェントジョブを作成するときに、このパラメーターを指定する必要があります。  
  
> [!IMPORTANT]  
>  認証情報をスクリプトファイルに保存しないでください。 セキュリティを強化するために、実行時にログイン名とパスワードを指定することをお勧めします。  
  
`[ @publisher_type = ] 'publisher_type'` パブリッシャーがのインスタンスで実行されていない場合のパブリッシャーの種類を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher_type* は **sysname**で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**MSSQLSERVER**|パブリッシャーを指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**ORACLE11I**|標準の Oracle パブリッシャーを指定します。|  
|**ORACLE GATEWAY **|Oracle ゲートウェイ パブリッシャーを指定します。|  
  
 Oracle パブリッシャーと Oracle ゲートウェイパブリッシャーの相違点の詳細については、「 [Oracle パブリッシングの概要](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)」を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_MSchange_snapshot_agent_properties** は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
 **Sp_MSchange_snapshot_agent_properties**を実行するときは、すべてのパラメーターを指定する必要があります。 [Sp_helppublication_snapshot](../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md)を実行して、スナップショットエージェントジョブの現在のプロパティを返します。  
  
 パブリッシャーが以降のバージョンのインスタンスで実行されている場合は [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 、 [sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md) を使用してスナップショットエージェントジョブのプロパティを変更する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_MSchange_snapshot_agent_properties**を実行できるのは、ディストリビューター側の固定サーバーロール**sysadmin**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
  
