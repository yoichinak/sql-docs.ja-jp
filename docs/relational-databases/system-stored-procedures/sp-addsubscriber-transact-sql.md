---
description: sp_addsubscriber (Transact-sql)
title: sp_addsubscriber (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9e48362fd0c671f3b7f9427c6a1ad291c175fa71
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546232"
---
# <a name="sp_addsubscriber-transact-sql"></a>sp_addsubscriber (Transact-sql)
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]

  パブリッシャーに新しいサブスクライバーを追加し、サブスクライバーがパブリケーションを受け取れるようにします。 このストアドプロシージャは、パブリッシャー側のパブリケーションデータベースで、スナップショットパブリケーションおよびトランザクションパブリケーションに対して実行されます。また、リモートディストリビューターを使用するマージパブリケーションの場合、このストアドプロシージャはディストリビューター側で実行されます。  
  
> [!IMPORTANT]  
>  このストアドプロシージャは非推奨とされます。 パブリッシャーでサブスクライバーを明示的に登録する必要がなくなりました。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addsubscriber [ @subscriber = ] 'subscriber'  
    [ , [ @type = ] type ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @commit_batch_size = ] commit_batch_size ]  
    [ , [ @status_batch_size = ] status_batch_size ]  
    [ , [ @flush_frequency = ] flush_frequency ]  
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
    [ , [ @description = ] 'description' ]  
    [ , [ @security_mode = ] security_mode ]  
    [ , [ @encrypted_password = ] encrypted_password ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @subscriber = ] 'subscriber'` 有効なサブスクライバーとしてこのサーバーのパブリケーションに追加するサーバーの名前を指定します。 *サブスクライバー* は **sysname**,、既定値はありません。  
  
`[ @type = ] type` サブスクライバーの種類を示します。 *種類* は **tinyint**で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**0** (既定値)|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サブスクライバー|  
|**1**|ODBC データソースサーバー|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet データベース|  
|**3**|OLE DB プロバイダー|  
  
`[ @login = ] 'login'` 認証のログイン ID を示し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *login* のデータ型は **sysname** で、既定値は NULL です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @password = ] 'password'` 認証用のパスワードを入力し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *パスワード* は **nvarchar (524)**,、既定値は NULL です。  
  
> [!IMPORTANT]  
>  空白のパスワードは使用しないでください。 強力なパスワードを使用してください。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @commit_batch_size = ] commit_batch_size` このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。  
  
> [!NOTE]  
>  この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @status_batch_size = ] status_batch_size` このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。  
  
> [!NOTE]  
>  この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @flush_frequency = ] flush_frequency` このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。  
  
> [!NOTE]  
>  この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_type = ] frequency_type` レプリケーションエージェントをスケジュールする頻度を指定します。 *frequency_type* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 回|  
|**2**|オン デマンド|  
|**4**|毎日|  
|**8**|週次|  
|**16**|月単位|  
|**32**|月単位の相対|  
|**64** (既定値)|自動開始|  
|**128**|繰り返し|  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*によって設定された頻度に適用される値を指定します。 *frequency_interval* は **int**,、既定値は1です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` レプリケーションエージェントの日付を指定します。 このパラメーターは、 *frequency_type* が **32** (月単位) に設定されている場合に使用されます。 *frequency_relative_interval* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1** (既定値)|First|  
|**2**|秒|  
|**4**|Third|  
|**8**|4 番目|  
|**16**|Last (最後へ)|  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`*Frequency_type*によって使用される定期実行係数です。 *frequency_recurrence_factor* は **int**,、既定値は **0**です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_subday = ] frequency_subday` 定義した期間中に再スケジュールする頻度を指定します。 *frequency_subday* は **int**,、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|1 度|  
|**2**|秒|  
|**4** (既定値)|分|  
|**8**|時間|  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequency_subday*の間隔を指定します。 *frequency_subday_interval* は **int**,、既定値は **5**です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` レプリケーションエージェントを最初にスケジュール設定する時刻を HHMMSS 形式で指定します。 *active_start_time_of_day* は **int**,、既定値は **0**です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` レプリケーションエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。 *active_end_time_of_day*は **int**,、既定値は 235959,、11:59:59 pm 24時間制として測定されます。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @active_start_date = ] active_start_date` レプリケーションエージェントを最初にスケジュール設定する日付を YYYYMMDD 形式で指定します。 *active_start_date* は **int**,、既定値は0です。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @active_end_date = ] active_end_date` レプリケーションエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。 *active_end_date* は **int**,、既定値は 99991231,、9999年12月31日を意味します。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @description = ] 'description'` サブスクライバーのテキストの説明を入力します。 *説明* は **nvarchar (255)**,、既定値は NULL です。  
  
`[ @security_mode = ] security_mode` 実装されているセキュリティモードです。 *security_mode* は **int**,、既定値は1です。 **0** は認証を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 **1** Windows 認証を指定します。  
  
> [!NOTE]  
>  このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のために保持されています。 このプロパティは、 [sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)の実行時に、サブスクリプションごとに指定されるようになりました。 この値を指定すると、このサブスクライバーでサブスクリプションを作成するときに既定値として使用され、警告メッセージが返されます。  
  
`[ @encrypted_password = ] encrypted_password` このパラメーターは非推奨とされており、旧バージョンとの互換性のみを設定するために提供されていますが、 *encrypted_password* の値は任意ですが、 **0** を指定するとエラーが発生します。  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーからパブリッシュする場合は、*パブリッシャー*を使用しないでください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_addsubscriber** は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
 サブスクライバーがマージパブリケーションへの匿名サブスクリプションのみを持つ場合、 **sp_addsubscriber**は必要ありません。  
  
 **sp_addsubscriber**は、**ディストリビューション**データベースの[MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md)テーブルに書き込みます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addsubscriber**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
