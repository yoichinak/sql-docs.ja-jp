---
description: sp_changesubstatus (Transact-sql)
title: sp_changesubstatus (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubstatus
- sp_changesubstatus_TSQL
helpviewer_keywords:
- sp_changesubstatus
ms.assetid: 9370e47a-d128-4f15-9224-1c3642770c39
author: markingmyname
ms.author: maghan
ms.openlocfilehash: faee6b09f682c5d13a3c005d95b1d513d9206026
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539129"
---
# <a name="sp_changesubstatus-transact-sql"></a>sp_changesubstatus (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  既存のサブスクライバーの状態を変更します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changesubstatus [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
        , [ @status = ] 'status'  
    [ , [ @previous_status = ] 'previous_status' ]  
    [ , [ @destination_db = ] 'destination_db' ]  
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
    [ , [ @optional_command_line = ] 'optional_command_line' ]  
    [ , [ @distribution_jobid = ] distribution_jobid ]  
    [ , [ @from_auto_sync = ] from_auto_sync ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @offloadagent= ] remote_agent_activation ]  
    [ , [ @offloadserver= ] 'remote_agent_server_name' ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] dts_package_location ]  
    [ , [ @skipobjectactivation = ] skipobjectactivation  
  [ , [ @distribution_job_name= ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* の **sysname**,、既定値は **%** です。 *パブリケーション*が指定されていない場合は、すべてのパブリケーションが影響を受けます。  
  
`[ @article = ] 'article'` アーティクルの名前を指定します。 アーティクルの名前はパブリケーションに対して一意である必要があります。 *アーティクル* は **sysname**で、既定値は **%** です。 *アーティクル*が指定されていない場合は、すべてのアーティクルが影響を受けます。  
  
`[ @subscriber = ] 'subscriber'` 状態を変更するサブスクライバーの名前を指定します。 *サブスクライバー* の **sysname**,、既定値は **%** です。 *サブスクライバー*が指定されていない場合、指定されたアーティクルのすべてのサブスクライバーについて状態が変更されます。  
  
`[ @status = ] 'status'`**Syssubscriptions**テーブルのサブスクリプションの状態を示します。 *status* の部分は **sysname**で、既定値はありません。これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**active**|サブスクライバーが同期され、データを受信しています。|  
|**inactive**|サブスクライブはしていませんが、サブスクライバーのエントリが存在します。|  
|**subscribed**|サブスクライバーはデータを要求していますが、まだ同期はとられていません。|  
  
`[ @previous_status = ] 'previous_status'` は、サブスクリプションの以前の状態です。 *previous_status* は **sysname**,、既定値は NULL です。 このパラメーターを使用すると、現在その状態になっているすべてのサブスクリプションを変更することができます。これにより、特定のサブスクリプションセットに対してグループ関数が許可されます (たとえば、すべてのアクティブなサブスクリプションを **サブスクライブ**済みに設定します)。  
  
`[ @destination_db = ] 'destination_db'` 転送先データベースの名前を指定します。 *destination_db* は **sysname**で、既定値は **%** です。  
  
`[ @frequency_type = ] frequency_type` ディストリビューションタスクをスケジュールする頻度を指定します。 *frequency_type* は **int**,、既定値は NULL です。  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*によって設定された頻度に適用する値を指定します。 *frequency_interval* は **int**,、既定値は NULL です。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` ディストリビューションタスクの日付を指定します。 このパラメーターは、 *frequency_type* が 32 (月単位) に設定されている場合に使用されます。 *frequency_relative_interval* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|First|  
|**2**|秒|  
|**4**|Third|  
|**8**|4 番目|  
|**16**|Last (最後へ)|  
|NULL (既定値)||  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数です。 *frequency_recurrence_factor* は **int**,、既定値は NULL です。  
  
`[ @frequency_subday = ] frequency_subday` 定義した期間にスケジュールを再設定する頻度を分単位で指定します。 *frequency_subday* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 度|  
|**2**|秒|  
|**4**|分|  
|**8**|時間|  
|NULL (既定値)||  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*の間隔を指定します。 *frequency_subday_interval* は **int**,、既定値は NULL です。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` ディストリビューションタスクを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day* は **int**,、既定値は NULL です。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` ディストリビューションタスクのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day* は **int**,、既定値は NULL です。  
  
`[ @active_start_date = ] active_start_date` ディストリビューションタスクを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date* は **int**,、既定値は NULL です。  
  
`[ @active_end_date = ] active_end_date` ディストリビューションタスクのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date* は **int**,、既定値は NULL です。  
  
`[ @optional_command_line = ] 'optional_command_line'` は省略可能なコマンドプロンプトです。 *optional_command_line* は **nvarchar (4000)**,、既定値は NULL です。  
  
`[ @distribution_jobid = ] distribution_jobid` サブスクリプションの状態を非アクティブからアクティブに変更するときの、サブスクリプションのディストリビューターでのディストリビューションエージェントのジョブ ID を示します。 その他の場合は、定義されません。 このストアドプロシージャの1回の呼び出しに複数のディストリビューションエージェントが関係している場合、結果は定義されません。 *distribution_jobid* は **binary (16)**,、既定値は NULL です。  
  
`[ @from_auto_sync = ] from_auto_sync` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @offloadagent = ] remote_agent_activation`
 > [!NOTE]  
>  リモートエージェントのアクティブ化は非推奨とされており、サポートされなくなりました。 このパラメーターは、スクリプトの旧バージョンとの互換性を維持するためにのみサポートされています。 *Remote_agent_activation*を**0**以外の値に設定すると、エラーが生成されます。  
  
`[ @offloadserver = ] 'remote_agent_server_name'`
 > [!NOTE]  
>  リモートエージェントのアクティブ化は非推奨とされており、サポートされなくなりました。 このパラメーターは、スクリプトの旧バージョンとの互換性を維持するためにのみサポートされています。 *Remote_agent_server_name*を NULL 以外の値に設定すると、エラーが生成されます。  
  
`[ @dts_package_name = ] 'dts_package_name'` データ変換サービス (DTS) パッケージの名前を指定します。 *dts_package_name* は **sysname**で、既定値は NULL です。 たとえば、 **DTSPub_Package** という名前のパッケージの場合、を指定し `@dts_package_name = N'DTSPub_Package'` ます。  
  
`[ @dts_package_password = ] 'dts_package_password'` パッケージのパスワードを指定します。 *dts_package_password* は **sysname** で、既定値は NULL です。これは、password プロパティを変更せずに残すことを指定します。  
  
> [!NOTE]  
>  DTS パッケージには、パスワードが必要です。  
  
`[ @dts_package_location = ] dts_package_location` パッケージの場所を指定します。 *dts_package_location* は **int**,、既定値は **0**です。 **0**の場合、パッケージの場所はディストリビューターにあります。 **1**の場合、パッケージの場所はサブスクライバーです。 パッケージの場所には、 **ディストリビューター** または **サブスクライバー**を指定できます。  
  
`[ @skipobjectactivation = ] skipobjectactivation` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @distribution_job_name = ] 'distribution_job_name'` ディストリビューションジョブの名前を指定します。 *distribution_job_name* は **sysname**,、既定値は NULL です。  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーでアーティクルのプロパティを変更する場合は、*パブリッシャー*を使用しないでください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_changesubstatus** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 **sp_changesubstatus** によって、 **syssubscriptions** テーブル内のサブスクライバーの状態が変更され、状態が変更されます。 必要に応じて、 **sysarticles** テーブル内のアーティクルの状態を更新して、アクティブまたは非アクティブであることを示します。 必要に応じて、レプリケートされたテーブルの **sysobjects** テーブルでレプリケーションフラグをオンまたはオフに設定します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changesubstatus**を実行できるのは、 **sysadmin**固定サーバーロールのメンバー、 **db_owner**固定データベースロールのメンバー、またはサブスクリプションの作成者だけです。  
  
## <a name="see-also"></a>参照  
 [sp_addsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
