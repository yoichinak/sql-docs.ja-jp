---
description: sp_changepublication_snapshot (Transact-sql)
title: sp_changepublication_snapshot (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changepublication_snapshot_TSQL
- sp_changepublication_snapshot
helpviewer_keywords:
- sp_changepublication_snapshot
ms.assetid: 518a4618-3592-4edc-8425-cbc33cdff891
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 437a923a6b4ad536f7702e547bb299bcf1ff47d1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541893"
---
# <a name="sp_changepublication_snapshot-transact-sql"></a>sp_changepublication_snapshot (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  指定されたパブリケーションのスナップショットエージェントのプロパティを変更します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
> [!IMPORTANT]  
>  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changepublication_snapshot [ @publication= ] 'publication'  
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
  
`[ @frequency_type = ] frequency_type` エージェントをスケジュールする頻度を指定します。 *frequency_type* は **int**,、値は次のいずれかを指定することができます。  
  
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
  
`[ @frequency_interval = ] frequency_interval` エージェントを実行する日を指定します。 *frequency_interval* は **int**,、値は次のいずれかを指定することができます。  
  
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
  
`[ @frequency_subday = ] frequency_subday`*Freq_subday_interval*の単位です。 *frequency_subday* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 度|  
|**2**|秒|  
|**4**|分|  
|**8**|時間|  
|NULL (既定値)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*の間隔を指定します。 *frequency_subday_interval* は **int**,、既定値は NULL です。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` スナップショットエージェントが実行される日付を指定します。 *frequency_relative_interval* は **int**,、既定値は NULL です。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数です。 *frequency_recurrence_factor* は **int**,、既定値は NULL です。  
  
`[ @active_start_date = ] active_start_date` スナップショットエージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date* は **int**,、既定値は NULL です。  
  
`[ @active_end_date = ] active_end_date` スナップショットエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date* は **int**,、既定値は NULL です。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` スナップショットエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day* は **int**,、既定値は NULL です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` スナップショットエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day* は **int**,、既定値は NULL です。  
  
`[ @snapshot_job_name = ] 'snapshot_agent_name'` 既存のジョブが使用されている場合は、既存のスナップショットエージェントジョブ名の名前を指定します。 *snapshot_agent_name* は **nvarchar (100)** で、既定値は NULL です。  
  
`[ @publisher_security_mode = ] publisher_security_mode` パブリッシャーに接続するときにエージェントが使用するセキュリティモードを示します。 *publisher_security_mode* は **smallint**,、既定値は NULL です。 **0** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は認証を、 **1** は Windows 認証を指定します。 以外のパブリッシャーには、値 **0** を指定する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
`[ @publisher_login = ] 'publisher_login'` パブリッシャーに接続するときに使用するログインを示します。 *publisher_login* は **sysname**,、既定値は NULL です。 *publisher_security_mode*が**0**の場合は*publisher_login*を指定する必要があります。 *Publisher_login*が NULL で*publisher_security_mode*が**1**の場合は、 *job_login*で指定された Windows アカウントをパブリッシャーに接続するときに使用されます。  
  
`[ @publisher_password = ] 'publisher_password'` パブリッシャーに接続するときに使用するパスワードを入力します。 *publisher_password* は **sysname**,、既定値は NULL です。  
  
> [!IMPORTANT]  
>  空白のパスワードは使用しないでください。 強力なパスワードを使用してください。 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @job_login = ] 'job_login'` エージェントを実行する Windows アカウントのログインを指定します。 *job_login* は **nvarchar (257)**,、既定値は NULL です。 この Windows アカウントは、ディストリビューターへのエージェント接続に常に使用されます。 新しいスナップショットエージェントジョブを作成するときに、このパラメーターを指定する必要があります。 これは、以外のパブリッシャーに対しては変更できません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
`[ @job_password = ] 'job_password'` エージェントを実行する Windows アカウントのパスワードを指定します。 *job_password* は **sysname**,、既定値は NULL です。 新しいスナップショットエージェントジョブを作成するときに、このパラメーターを指定する必要があります。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーでスナップショットエージェントを作成する場合は、*パブリッシャー*を使用しないでください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_changepublication_snapshot** は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changepublication_snapshot**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [パブリケーションとアーティクルのプロパティの変更](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication_snapshot &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
