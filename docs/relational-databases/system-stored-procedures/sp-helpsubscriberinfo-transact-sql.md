---
description: sp_helpsubscriberinfo (Transact-sql)
title: sp_helpsubscriberinfo (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscriberinfo
- sp_helpsubscriberinfo_TSQL
helpviewer_keywords:
- sp_helpsubscriberinfo
ms.assetid: fbabe1ec-57cf-425c-bae7-af7f5d3198fd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 490355fa242d799d524690242e4f7e2a0d8ea830
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535100"
---
# <a name="sp_helpsubscriberinfo-transact-sql"></a>sp_helpsubscriberinfo (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  サブスクライバーに関する情報を表示します。 このストアドプロシージャは、パブリッシャー側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpsubscriberinfo [ [ @subscriber =] 'subscriber']  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前を指定します。 *サブスクライバー* のデータ型は **sysname**で、既定値はで **%** 、すべての情報が返されます。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher* は **sysname**で、既定値は現在のサーバーの名前です。  
  
> [!NOTE]  
>  Oracle パブリッシャーの場合を除き、*パブリッシャー*を指定することはできません。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**サブスクライバ**|**sysname**|サブスクライバーの名前。|  
|**type**|**tinyint**|サブスクライバーの種類:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース**1** = ODBC データソース|  
|**ログイン**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のログイン ID。|  
|**password**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証のパスワード。|  
|**commit_batch_size**|**int**|サポートされていません。|  
|**status_batch_size**|**int**|サポートされていません。|  
|**flush_frequency**|**int**|サポートされていません。|  
|**frequency_type**|**int**|ディストリビューション エージェントを実行する頻度。<br /><br /> **1** = 1 回<br /><br /> **2** = 要求時<br /><br /> **4** = 日単位<br /><br /> **8** = 週単位<br /><br /> **16** = 月単位<br /><br /> **32** = 毎月の相対<br /><br /> **64** = 自動開始<br /><br /> **128** = 定期的|  
|**frequency_interval**|**int**|*Frequency_type*によって設定された頻度に適用される値。|  
|**frequency_relative_interval**|**int**|*Frequency_type*が**32** (月単位) に設定されている場合に使用ディストリビューションエージェントの日付:<br /><br /> **1** = 最初<br /><br /> **2** = 秒<br /><br /> **4** = 3 番目<br /><br /> **8** = 4 番目<br /><br /> **16** = 最後|  
|**frequency_recurrence_factor**|**int**|*Frequency_type*によって使用される繰り返し係数。|  
|**frequency_subday**|**int**|定義した期間にスケジュールを組み直す頻度。<br /><br /> **1** = 1 回<br /><br /> **2** = 秒<br /><br /> **4** = 分<br /><br /> **8** = 時間|  
|**frequency_subday_interval**|**int**|*Frequency_subday*の間隔。|  
|**active_start_time_of_day**|**int**|ディストリビューションエージェントを最初にスケジュール設定した時刻を HHMMSS 形式で指定します。|  
|**active_end_time_of_day**|**int**|ディストリビューションエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。|  
|**active_start_date**|**int**|ディストリビューションエージェントを最初にスケジュール設定する日付。形式は YYYYMMDD です。|  
|**active_end_date**|**int**|ディストリビューションエージェントのスケジュール設定を停止する日付を YYYYMMDD 形式で指定します。|  
|**retryattempt**|**int**|サポートされていません。|  
|**retrydelay**|**int**|サポートされていません。|  
|**description**|**nvarchar (255)**|サブスクライバーのテキストによる説明。|  
|**security_mode**|**int**|実装されたセキュリティモード:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証|  
|**frequency_type2**|**int**|マージ エージェントを実行する頻度。<br /><br /> **1** = 1 回<br /><br /> **2** = 要求時<br /><br /> **4** = 日単位<br /><br /> **8** = 週単位<br /><br /> **16** = 月単位<br /><br /> **32** = 毎月の相対<br /><br /> **64** = 自動開始<br /><br /> **128** = 定期的|  
|**frequency_interval2**|**int**|*Frequency_type*によって設定された頻度に適用される値。|  
|**frequency_relative_interval2**|**int**|*Frequency_type*が 32 (月単位) に設定されている場合に使用マージエージェントの日付:<br /><br /> **1** = 最初<br /><br /> **2** = 秒<br /><br /> **4** = 3 番目<br /><br /> **8** = 4 番目<br /><br /> **16** = 最後|  
|**frequency_recurrence_factor2**|**int**|*Frequency_type * ** によって使用される繰り返し係数。|  
|**frequency_subday2**|**int**|定義した期間にスケジュールを組み直す頻度。<br /><br /> **1** = 1 回<br /><br /> **2** = 秒<br /><br /> **4** = 分<br /><br /> **8** = 時間|  
|**frequency_subday_interval2**|**int**|*Frequency_subday*の間隔。|  
|**active_start_time_of_day2**|**int**|マージエージェントを最初にスケジュール設定した時刻を HHMMSS 形式で指定します。|  
|**active_end_time_of_day2**|**int**|マージエージェントのスケジュール設定を停止する時刻を HHMMSS 形式で指定します。|  
|**active_start_date2**|**int**|マージ エージェントを最初にスケジュールに組み込んだ日付。形式は YYYYMMDD です。|  
|**active_end_date2**|**int**|マージ エージェントのスケジュールへの組み込みを停止した日付。形式は YYYYMMDD です。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helpsubscriberinfo** は、スナップショットレプリケーション、トランザクションレプリケーション、およびマージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpsubscriberinfo**を実行できるのは、 **sysadmin**固定サーバーロールのメンバー、 **db_owner**固定データベースロールのメンバー、またはパブリケーションのパブリケーションアクセスリストのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addpullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_changesubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
