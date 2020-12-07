---
description: sp_addpublication_snapshot (Transact-SQL)
title: sp_addpublication_snapshot (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e59ad9f2fb37ac4bd8aecc18d126c397ec4f67d5
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541990"
---
# <a name="sp_addpublication_snapshot-transact-sql"></a>sp_addpublication_snapshot (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  指定されたパブリケーションのスナップショット エージェントを作成します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
> [!IMPORTANT]  
>  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addpublication_snapshot [ @publication= ] 'publication'  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @snapshot_job_name = ] 'snapshot_agent_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @frequency_type = ] frequency_type` スナップショットエージェントを実行する頻度を指定します。 *frequency_type* は **int**,、値は次のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 回のみ|  
|**4** (既定値)|毎日|  
|**8**|業務.|  
|**16**|月単位。|  
|**32**|月単位に frequency_interval で示される間隔|  
|**64**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントの起動時。|  
|**128**|コンピューターがアイドル状態のときに実行する|  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*によって設定された頻度に適用する値を指定します。 *frequency_interval* は **int**,、値は次のいずれかを指定することができます。  
  
|Frequency_type の値|frequency_interval への影響|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval* は使用されていません。|  
|**4** (既定値)|*Frequency_interval*毎日、既定値は日単位です。|  
|**8**|*frequency_interval* は、次の1つまたは複数の [&#124; (ビットごと](../../t-sql/language-elements/bitwise-or-transact-sql.md) の or) 論理演算子と組み合わせて使用します。<br /><br /> **1** = 日曜日 &#124;<br /><br /> **2** = 月曜日 &#124;<br /><br /> **4** = 火曜日 &#124;<br /><br /> **8** = 水曜日 &#124;<br /><br /> **16** = 木曜日 &#124;<br /><br /> **32** = 金曜日 &#124;<br /><br /> **64** = 土曜日|  
|**16**|月の *frequency_interval* 日。|  
|**32**|*frequency_interval* は次のいずれかです。<br /><br /> **1** = 日曜日 &#124;<br /><br /> **2** = 月曜日 &#124;<br /><br /> **3** = 火曜日 &#124;<br /><br /> **4** = 水曜日 &#124;<br /><br /> **5** = 木曜日 &#124;<br /><br /> **6** = 金曜日 &#124;<br /><br /> **7** = 土曜日 &#124;<br /><br /> **8** = 日 &#124;<br /><br /> **9** = 平日 &#124;<br /><br /> **10** = 週末|  
|**64**|*frequency_interval* は使用されていません。|  
|**128**|*frequency_interval* は使用されていません。|  
  
`[ @frequency_subday = ] frequency_subday`*Freq_subday_interval*の単位です。 *frequency_subday* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 度|  
|**2**|秒|  
|**4** (既定値)|分|  
|**8**|時間|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*の間隔を指定します。 *frequency_subday_interval* は **int**,、既定値は 5 (5 分ごと) を意味します。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` スナップショットエージェントが実行される日付を指定します。 *frequency_relative_interval* は **int**,、既定値は1です。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数です。 *frequency_recurrence_factor* は **int**,、既定値は0です。  
  
`[ @active_start_date = ] active_start_date` スナップショットエージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date* は **int**,、既定値は0です。  
  
`[ @active_end_date = ] active_end_date` スナップショットエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date* は **int**,、既定値は 99991231,、9999年12月31日を意味します。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` スナップショットエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day* は **int**,、既定値は0です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` スナップショットエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day* は **int**,、既定値は 235959,、11:59:59 pm 24時間制として測定されます。  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'` 既存のジョブが使用されている場合は、既存のスナップショットエージェントジョブ名の名前を指定します。 *snapshot_agent_name* は **nvarchar (100)** で、既定値は NULL です。 このパラメーターは内部で使用するため、新しいパブリケーションを作成するときには指定しないでください。 *Snapshot_agent_name*が指定されている場合、 *job_login*と*job_password*は NULL である必要があります。  
  
`[ @publisher_security_mode = ] publisher_security_mode` パブリッシャーに接続するときにエージェントが使用するセキュリティモードを示します。 *publisher_security_mode* は **smallint**,、既定値は1です。 **0** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は認証を、 **1** は Windows 認証を指定します。 以外のパブリッシャーには、値 **0** を指定する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` パブリッシャーに接続するときに使用するログインを示します。 *publisher_login* は **sysname**,、既定値は NULL です。 *publisher_security_mode*が**0**の場合は*publisher_login*を指定する必要があります。 *Publisher_login*が NULL で*publisher_security_mode*が**1**の場合、 *job_login*で指定されたアカウントは、パブリッシャーに接続するときに使用されます。  
  
`[ @publisher_password = ] 'publisher_password'` パブリッシャーに接続するときに使用するパスワードを入力します。 *publisher_password* は **sysname**,、既定値は NULL です。  
  
> [!IMPORTANT]  
>  認証情報をスクリプトファイルに保存しないでください。 セキュリティを強化するために、実行時にログイン名とパスワードを指定することをお勧めします。  
  
`[ @job_login = ] 'job_login'` エージェントを実行するアカウントのログインを指定します。 Azure SQL Managed Instance で、SQL Server アカウントを使用します。 *job_login* は **nvarchar (257)**,、既定値は NULL です。 このアカウントは、ディストリビューターへのエージェント接続に常に使用されます。 新しいスナップショットエージェントジョブを作成するときに、このパラメーターを指定する必要があります。  
  
> [!NOTE]
>  以外のパブリッシャーの場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、これは [Sp_adddistpublisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)で指定されたログインと同じである必要があります。  
  
`[ @job_password = ] 'job_password'` エージェントを実行する Windows アカウントのパスワードを指定します。 *job_password* は **sysname**であり、既定値はありません。 新しいスナップショットエージェントジョブを作成するときに、このパラメーターを指定する必要があります。  
  
> [!IMPORTANT]  
>  認証情報をスクリプトファイルに保存しないでください。 セキュリティを強化するために、実行時にログイン名とパスワードを指定することをお勧めします。  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーでスナップショットエージェントを作成する場合は、*パブリッシャー*を使用しないでください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_addpublication_snapshot** は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addpublication_snapshot**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [sp_addpublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication_snapshot &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_startpublication_snapshot &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
