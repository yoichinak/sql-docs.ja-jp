---
description: sp_help_alert (Transact-SQL)
title: sp_help_alert (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_alert
- sp_help_alert_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_alert
ms.assetid: 850cef4e-6348-4439-8e79-fd1bca712091
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b02f303a4465df18cb049d06ecef585dad29a504
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549725"
---
# <a name="sp_help_alert-transact-sql"></a>sp_help_alert (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  特定のサーバーに対して定義された警告に関する情報をレポートします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_alert [ [ @alert_name = ] 'alert_name' ]   
     [ , [ @order_by = ] 'order_by' ]   
     [ , [ @alert_id = ] alert_id ]   
     [ , [ @category_name = ] 'category' ]   
     [ , [ @legacy_format = ] legacy_format ]  
```  
  
## <a name="arguments"></a>引数  
`[ @alert_name = ] 'alert_name'` アラートの名前。 *alert_name* は **nvarchar (128)** です。 *Alert_name*が指定されていない場合は、すべてのアラートに関する情報が返されます。  
  
`[ @order_by = ] 'order_by'` 結果を生成するために使用する並べ替え順序。 *order_by*は **sysname**で、既定値は N '*name*' です。  
  
`[ @alert_id = ] alert_id` 情報を報告する警告の識別番号を指定します。 *alert_id*は **int**,、既定値は NULL です。  
  
`[ @category_name = ] 'category'` アラートのカテゴリ。 *category* は **sysname**,、既定値は NULL です。  
  
`[ @legacy_format = ] legacy_format` 従来の結果セットを生成するかどうかを指定します。 *legacy_format* は **ビット**,、既定値は **0**です。 *Legacy_format*が**1**の場合、 **sp_help_alert** Microsoft SQL Server 2000 で**sp_help_alert**によって返された結果セットを返します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 ** \@ Legacy_format**が**0**の場合、 **sp_help_alert**によって次の結果セットが生成されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|システムによって割り当てられた一意な整数識別子。|  
|**name**|**sysname**|アラート名 (例: Demo: Full **msdb** log)。|  
|**event_source**|**nvarchar (100)**|イベントのソース。 バージョン7.0 の場合、常に**MSSQLServer**になります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|警告を定義するメッセージエラー番号。 (通常、 **sysmessages** テーブルのエラー番号に対応します)。 重大度を使用して警告を定義する場合、 **message_id** は **0** または NULL になります。|  
|**severity**|**int**|アラートを定義する重大度レベル ( **9** ~ **25**、 **110**、 **120**、 **130**、または **140**)。|  
|**有効**|**tinyint**|警告が現在有効になっているかどうか (**1**) またはない (**0**) かどうかの状態。 有効でない警告は送信されません。|  
|**delay_between_responses**|**int**|警告への応答の間の待機時間 (秒単位)。|  
|**last_occurrence_date**|**int**|警告が最後に発生した日付。|  
|**last_occurrence_time**|**int**|アラートが最後に発生した時刻。|  
|**last_response_date**|**int**|**SQLServerAgent**サービスが最後に警告に応答した日付。|  
|**last_response_time**|**int**|**SQLServerAgent**サービスが最後に警告に応答した時刻。|  
|**notification_message**|**nvarchar(512)**|電子メールまたはポケットベルによる通知の一部としてオペレーターに送信される追加メッセージ (省略可)。|  
|**include_event_description**|**tinyint**|Microsoft Windows アプリケーション ログからの SQL Server エラーの説明を通知メッセージに含めるかどうか。|  
|**database_name**|**sysname**|警告を起動するためにエラーが発生する必要があるデータベース。 データベース名が NULL の場合、エラーが発生した場所に関係なく警告が発生します。|  
|**event_description_keyword**|**nvarchar (100)**|Windows アプリケーション ログ内の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーの説明。これには、提供されたものと同様の文字シーケンスが含まれている必要があります。|  
|**occurrence_count**|**int**|アラートが発生した回数。|  
|**count_reset_date**|**int**|**Occurrence_count**が最後にリセットされた日付。|  
|**count_reset_time**|**int**|**Occurrence_count**が最後にリセットされた時刻。|  
|**job_id**|**uniqueidentifier**|警告に応答して実行されるジョブの識別番号を指定します。|  
|**job_name**|**sysname**|警告に応答して実行されるジョブの名前。|  
|**has_notification**|**int**|この警告について1つ以上のオペレーターに通知される場合は0以外。 値は、次の値の1つ以上 (連結されています)。<br /><br /> **1**= 電子メール通知<br /><br /> **2**= ポケットベルによる通知<br /><br /> **4**= **net send** 通知があります。|  
|**flags**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**performance_condition**|**nvarchar(512)**|**Type**が**2**の場合、この列にはパフォーマンス条件の定義が表示されます。それ以外の場合、列は NULL になります。|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 の場合は常に '[Uncategorized]' となります。|  
|**wmi_namespace**|**sysname**|**Type**が**3**の場合、この列には WMI イベントの名前空間が表示されます。|  
|**wmi_query**|**nvarchar(512)**|**Type**が**3**の場合、この列には WMI イベントのクエリが表示されます。|  
|**type**|**int**|イベントの種類。<br /><br /> **1 個**の  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントアラート<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パフォーマンスの警告<br /><br /> **3** = WMI イベント警告|  
  
 ** \@ Legacy_format**が**1**の場合、 **sp_help_alert**によって次の結果セットが生成されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|システムによって割り当てられた一意な整数識別子。|  
|**name**|**sysname**|アラート名 (例: Demo: Full **msdb** log)。|  
|**event_source**|**nvarchar (100)**|イベントのソース。 バージョン7.0 の場合、常に**MSSQLServer**になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**event_category_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**event_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**message_id**|**int**|警告を定義するメッセージエラー番号。 (通常、 **sysmessages** テーブルのエラー番号に対応します)。 重大度を使用して警告を定義する場合、 **message_id** は **0** または NULL になります。|  
|**severity**|**int**|アラートを定義する重大度レベル ( **9** ~ **25**、 **110**、 **120**、 **130**、または 1**40**)。|  
|**有効**|**tinyint**|警告が現在有効になっているかどうか (**1**) またはない (**0**) かどうかの状態。 有効でない警告は送信されません。|  
|**delay_between_responses**|**int**|警告への応答の間の待機時間 (秒単位)。|  
|**last_occurrence_date**|**int**|警告が最後に発生した日付。|  
|**last_occurrence_time**|**int**|アラートが最後に発生した時刻。|  
|**last_response_date**|**int**|**SQLServerAgent**サービスが最後に警告に応答した日付。|  
|**last_response_time**|**int**|**SQLServerAgent**サービスが最後に警告に応答した時刻。|  
|**notification_message**|**nvarchar(512)**|電子メールまたはポケットベルによる通知の一部としてオペレーターに送信される追加メッセージ (省略可)。|  
|**include_event_description**|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Windows アプリケーションログからのエラーの説明を通知メッセージの一部として含めるかどうかを指定します。|  
|**database_name**|**sysname**|警告を起動するためにエラーが発生する必要があるデータベース。 データベース名が NULL の場合、エラーが発生した場所に関係なく警告が発生します。|  
|**event_description_keyword**|**nvarchar (100)**|Windows アプリケーション ログ内の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーの説明。これには、提供されたものと同様の文字シーケンスが含まれている必要があります。|  
|**occurrence_count**|**int**|アラートが発生した回数。|  
|**count_reset_date**|**int**|**Occurrence_count**が最後にリセットされた日付。|  
|**count_reset_time**|**int**|**Occurrence_count**が最後にリセットされた時刻。|  
|**job_id**|**uniqueidentifier**|ジョブの識別番号。|  
|**job_name**|**sysname**|アラートへの応答として実行されるオンデマンドジョブ。|  
|**has_notification**|**int**|この警告について1つ以上のオペレーターに通知される場合は0以外。 値は次のとおりです。複数の場合は OR で表されます。<br /><br /> **1**= 電子メール通知<br /><br /> **2**= ポケットベルによる通知<br /><br /> **4**= **net send** 通知があります。|  
|**flags**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].|  
|**performance_condition**|**nvarchar(512)**|**Type**が**2**の場合、この列にはパフォーマンス条件の定義が表示されます。 **Type**が**3**の場合、この列には WMI イベントのクエリが表示されます。 それ以外の場合、列は NULL になります。|  
|**category_name**|**sysname**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] 7.0 では常に '**[未カテゴリ化]**' になり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**type**|**int**|アラートの種類:<br /><br /> **1 個**の  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントアラート<br /><br /> **2**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パフォーマンスの警告<br /><br /> **3** = WMI イベント警告|  
  
## <a name="remarks"></a>解説  
 **sp_help_alert** は、 **msdb** データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 それ以外のユーザーには、 **msdb** データベースの **SQLAgentOperatorRole** 固定サーバー ロールを与える必要があります。  
  
 **Sqlagentoperatorrole**の詳細については、「 [SQL Server エージェント固定データベースロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、`Demo: Sev. 25 Errors` 警告に関する情報をレポートします。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_alert @alert_name = 'Demo: Sev. 25 Errors';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sp_update_alert &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
