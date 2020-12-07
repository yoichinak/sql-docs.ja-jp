---
description: sp_add_alert (Transact-sql)
title: sp_add_alert (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_alert
- sp_add_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_alert
ms.assetid: d9b41853-e22d-4813-a79f-57efb4511f09
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dd4c19f3cbe2525bf9b968e1d314767217f62129
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419316"
---
# <a name="sp_add_alert-transact-sql"></a>sp_add_alert (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  アラートを作成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_alert [ @name = ] 'name'   
     [ , [ @message_id = ] message_id ]   
     [ , [ @severity = ] severity ]   
     [ , [ @enabled = ] enabled ]  
     [ , [ @delay_between_responses = ] delay_between_responses ]   
     [ , [ @notification_message = ] 'notification_message' ]   
     [ , [ @include_event_description_in = ] include_event_description_in ]   
     [ , [ @database_name = ] 'database' ]   
     [ , [ @event_description_keyword = ] 'event_description_keyword_pattern' ]   
     [ , { [ @job_id = ] job_id | [ @job_name = ] 'job_name' } ]   
     [ , [ @raise_snmp_trap = ] raise_snmp_trap ]   
     [ , [ @performance_condition = ] 'performance_condition' ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @wmi_namespace = ] 'wmi_namespace' ]  
     [ , [ @wmi_query = ] 'wmi_query' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'` 警告の名前。 この名前は、警告に対する応答として送信される電子メールまたはポケットベルのメッセージに表示されます。 一意である必要があり、パーセント () 文字を含めることができ **%** ます。 *名前* は **sysname**,、既定値はありません。  
  
`[ @message_id = ] message_id` 警告を定義するメッセージエラー番号。 (通常、 **sysmessages** テーブルのエラー番号に対応しています)。 *message_id* は **int**,、既定値は **0**です。 *重大度*を使用して警告を定義する場合は、 *message_id*を**0**または NULL にする必要があります。  
  
> [!NOTE]  
>  Microsoft Windows アプリケーションログに書き込まれた **sysmessages** エラーのみが、アラートを送信する可能性があります。  
  
`[ @severity = ] severity` 警告を定義する重大度レベル ( **1** ~ **25**)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Sysmessages**テーブルに格納されているすべてのメッセージが、指定された [!INCLUDE[msCoName](../../includes/msconame-md.md)] 重大度で Windows アプリケーションログに送信されると、アラートが送信されます。 *重大度* は **int**,、既定値は0です。 警告を定義するために *message_id* を使用する場合は、 *重大度* を **0**にする必要があります。  
  
`[ @enabled = ] enabled` 警告の現在の状態を示します。 *有効* になっているは **tinyint**,、既定値は 1 (有効) です。 **0**の場合、警告は無効になり、起動されません。  
  
`[ @delay_between_responses = ] delay_between_responses` 警告への応答間の待機時間 (秒単位)。 *delay_between_responses*は **int**,、既定値は **0**です。これは、応答の間 (アラートが発生するたびに応答が生成される) の待機がないことを意味します。 応答は、次のいずれかまたは両方の形式で指定できます。  
  
-   電子メールまたはポケットベルを使用して送信された1つ以上の通知。  
  
-   実行するジョブ。  
  
 この値を設定することにより、たとえば、短時間にアラートが繰り返し発生した場合に、不要な電子メールメッセージが送信されないようにすることができます。  
  
`[ @notification_message = ] 'notification_message'` は、電子メール、 **net send**、またはポケットベルによる通知の一部としてオペレーターに送信されるオプションの追加メッセージです。 *notification_message* は **nvarchar (512)**,、既定値は NULL です。 *Notification_message*を指定すると、修復プロシージャなどの特別なメモを追加する場合に便利です。  
  
`[ @include_event_description_in = ] include_event_description_in` エラーの説明を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通知メッセージの一部として含めるかどうかを指定します。 *include_event_description_in*は **tinyint**で、既定値は **5** (電子メールと **net send**) です。また、これらの値の1つ以上を **or** 論理演算子と組み合わせて使用することもできます。  
  
> [!IMPORTANT]
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の今後のバージョンでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントからポケットベル オプションと **net send** オプションが削除される予定です。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。  
  
|値|説明|  
|-----------|-----------------|  
|**0**|None|  
|**1**|電子メール|  
|**2**|ポケットベル|  
|**4**|**net send**|  
  
`[ @database_name = ] 'database'` 警告を起動するためにエラーが発生する必要があるデータベース。 *データベース*が指定されていない場合は、エラーが発生した場所に関係なく警告が発生します。 *データベース* は **sysname**です。 角かっこ ([]) で囲まれた名前は使用できません。 既定値は NULL です。  
  
`[ @event_description_keyword = ] 'event_description_keyword_pattern'` エラーの説明が必要とする文字のシーケンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[tsql](../../includes/tsql-md.md)] LIKE 式パターン一致文字を使用できます。 *event_description_keyword_pattern* は **nvarchar (100)**,、既定値は NULL です。 このパラメーターは、オブジェクト名 ( **% customer_table%** など) をフィルター処理する場合に便利です。  
  
`[ @job_id = ] job_id` このアラートに応答して実行するジョブのジョブ識別番号を指定します。 *job_id* は **uniqueidentifier**,、既定値は NULL です。  
  
`[ @job_name = ] 'job_name'` この警告に応答して実行されるジョブの名前。 *job_name*は **sysname**,、既定値は NULL です。  
  
> [!NOTE]  
>  *Job_id*または*job_name*のいずれかを指定する必要がありますが、両方を指定することはできません。  
  
`[ @raise_snmp_trap = ] raise_snmp_trap` バージョン7.0 では実装されていません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *raise_snmp_trap* は **tinyint**,、既定値は0です。  
  
`[ @performance_condition = ] 'performance_condition'` は、'*itemcomparatorvalue*' という形式で表された値です。 *performance_condition* は **nvarchar (512)** で、既定値は NULL です。これらの要素で構成されます。  
  
|要素の書式設定|説明|  
|--------------------|-----------------|  
|*Item*|パフォーマンス オブジェクト、パフォーマンス カウンター、またはカウンターの名前付きインスタンス。|  
|*演算子*|>、<、または = のいずれかの演算子|  
|*Value*|カウンターの数値|  
  
`[ @category_name = ] 'category'` 警告カテゴリの名前。 *category* は **sysname**,、既定値は NULL です。  
  
`[ @wmi_namespace = ] 'wmi_namespace'` イベントを照会する WMI 名前空間。 *wmi_namespace* は **sysname**,、既定値は NULL です。 サポートされるのはローカル サーバーの名前空間だけです。  
  
`[ @wmi_query = ] 'wmi_query'` 警告の WMI イベントを指定するクエリ。 *wmi_query* は **nvarchar (512)**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **sp_add_alert** は、 **msdb** データベースから実行する必要があります。  
  
 次の状況では、およびアプリケーションによって生成されたエラーやメッセージ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が Windows アプリケーションログに送信されるため、アラートが発生する可能性があります。  
  
-   重大度19以上の **sys. メッセージ** エラー  
  
-   With LOG 構文を使用して呼び出された RAISERROR ステートメント  
  
-   **Sp_altermessage**を使用して変更または作成されたすべての**sys. メッセージ**エラー  
  
-   **Xp_logevent**を使用してログに記録されたイベント  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、警告システム全体を簡単に管理できるグラフィカルなツールです。警告の基本構成を設定するには、SQL Server Management Studio を使用することをお勧めします。  
  
 警告が正常に動作しないときは、次のことを確認してください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントサービスが実行されています。  
  
-   Windows アプリケーション ログにイベントが表示されること。  
  
-   アラートが有効になっています。  
  
-   **xp_logevent** で生成されたイベントは master データベースで発生します。 そのため、 **xp_logevent**は、警告の** \@ database_name**が **' master '** または NULL の場合を除き、アラートをトリガーしません。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sp_add_alert** を実行できるのは、 **sysadmin**固定サーバー ロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 次の例では、警告発生時にジョブ `Back up the AdventureWorks2012 Database` を実行する Test Alert という警告を追加します。  
  
> [!NOTE]  
>  この例では、メッセージ55001とジョブが既に存在していることを前提としてい `Back up the AdventureWorks2012 Database` ます。 この例は、説明のためだけに示しています。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_alert  
    @name = N'Test Alert',  
    @message_id = 55001,   
   @severity = 0,   
   @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
   @job_name = N'Back up the AdventureWorks2012 Database' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_altermessage &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_delete_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-alert-transact-sql.md)   
 [sp_help_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
