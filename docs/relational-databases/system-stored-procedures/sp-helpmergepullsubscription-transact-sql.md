---
description: sp_helpmergepullsubscription (Transact-SQL)
title: sp_helpmergepullsubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepullsubscription
- sp_helpmergepullsubscription_TSQL
helpviewer_keywords:
- sp_helpmergepullsubscription
ms.assetid: 6f3125f3-0dfa-40bd-b725-8aa1591234f6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b74d9846d672a59adbde9eada760af1d60fc725e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543277"
---
# <a name="sp_helpmergepullsubscription-transact-sql"></a>sp_helpmergepullsubscription (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サブスクライバーに存在するプルサブスクリプションに関する情報を返します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergepullsubscription [ [ @publication=] 'publication']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
```  
  
## <a name="argument"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* の **sysname**,、既定値は **%** です。 *パブリケーション*がの場合 **%** 、現在のデータベース内のすべてのマージパブリケーションおよびサブスクリプションに関する情報が返されます。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher*は **sysname**で、既定値は **%** です。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャーデータベースの名前を指定します。 *publisher_db*は **sysname**で、既定値は **%** です。  
  
`[ @subscription_type = ] 'subscription_type'` プルサブスクリプションを表示するかどうかを指定します。 *subscription_type*は **nvarchar (10)**,、既定値は **' pull '** です。 有効な値は、 **' push '**、 **' pull '**、または **' both '** です。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**nvarchar(1000)**|サブスクリプションの名前。|  
|**レプリケーション**|**sysname**|パブリケーションの名前。|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher_db**|**sysname**|パブリッシャーデータベースの名前。|  
|**サブスクライバ**|**sysname**|サブスクライバーの名前。|  
|**subscription_db**|**sysname**|サブスクリプションデータベースの名前。|  
|**status**|**int**|サブスクリプションの状態:<br /><br /> **0** = 非アクティブなサブスクリプション<br /><br /> **1** = アクティブなサブスクリプション<br /><br /> **2** = 削除されたサブスクリプション<br /><br /> **3** = デタッチされたサブスクリプション<br /><br /> **4** = アタッチされたサブスクリプション<br /><br /> **5** = アップロードによる再初期化のためのサブスクリプションがマークされました<br /><br /> **6** = サブスクリプションのアタッチに失敗しました<br /><br /> **7** = バックアップから復元されたサブスクリプション|  
|**subscriber_type**|**int**|サブスクライバーの種類:<br /><br /> **1** = グローバル<br /><br /> **2** = ローカル<br /><br /> **3** = 匿名|  
|**subscription_type**|**int**|サブスクリプションの種類:<br /><br /> **0** = プッシュ<br /><br /> **1** = プル<br /><br /> **2** = 匿名|  
|**priority**|**float (8)**|サブスクリプションの優先度。 値は **100.00**未満である必要があります。|  
|**sync_type**|**tinyint**|サブスクリプションの同期の種類:<br /><br /> **1** = 自動<br /><br /> **2** = スナップショットは使用されません。|  
|**description**|**nvarchar (255)**|プルサブスクリプションの簡単な説明です。|  
|**merge_jobid**|**binary(16)**|マージエージェントのジョブ ID。|  
|**enabled_for_syncmgr**|**int**|同期マネージャーを使用してサブスクリプションを同期できるかどうかを指定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] します。|  
|**last_updated**|**nvarchar (26)**|マージエージェントがサブスクリプションを最後に正常に同期した時刻。|  
|**publisher_login**|**sysname**|パブリッシャーのログイン名。|  
|**publisher_password**|**sysname**|パブリッシャーのパスワードです。|  
|**publisher_security_mode**|**int**|パブリッシャーのセキュリティモードを指定します。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証<br /><br /> **1** = Windows 認証|  
|**ディストリビューター**|**sysname**|ディストリビューターの名前。|  
|**distributor_login**|**sysname**|ディストリビューターのログイン名です。|  
|**distributor_password**|**sysname**|ディストリビューターのパスワードです。|  
|**distributor_security_mode**|**int**|ディストリビューターのセキュリティモードを指定します。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証<br /><br /> **1** = Windows 認証|  
|**ftp_address**|**sysname**|旧バージョンとの互換性のためにのみ使用できます。 ディストリビューターのファイル転送プロトコル (FTP) サービスのネットワークアドレスを示します。|  
|**ftp_port**|**int**|旧バージョンとの互換性のためにのみ使用できます。 ディストリビューター用の FTP サービスのポート番号です。|  
|**ftp_login**|**sysname**|旧バージョンとの互換性のためにのみ使用できます。 FTP サービスへの接続に使用するユーザー名です。|  
|**ftp_password**|**sysname**|旧バージョンとの互換性のためにのみ使用できます。 FTP サービスに接続するときに使用するユーザー パスワードです。|  
|**alt_snapshot_folder**|**nvarchar (255)**|場所が既定の場所に加えてまたは以外の場合に、スナップショットフォルダーが格納される場所。|  
|**working_directory**|**nvarchar (255)**|オプションが指定されている場合に、FTP を使用してスナップショットファイルが転送されるディレクトリへの完全修飾パスです。|  
|**use_ftp**|**bit**|サブスクリプションは、インターネット経由でパブリケーションをサブスクライブしています。また、FTP アドレスのプロパティが構成されています。 **0**の場合、サブスクリプションは FTP を使用していません。 **1**の場合、サブスクリプションは FTP を使用しています。|  
|**offload_agent**|**bit**|エージェントをリモートでアクティブにして実行できるかどうかを指定します。 **0**の場合、エージェントをリモートでアクティブにすることはできません。|  
|**offload_server**|**sysname**|リモートから起動するときに使用するサーバーの名前です。|  
|**use_interactive_resolver**|**int**|調整時に対話型の競合回避モジュールを使用するかどうかを示します。 **0**の場合、インタラクティブ競合回避モジュールは使用されません。|  
|**subid**|**uniqueidentifier**|サブスクライバーの ID。|  
|**dynamic_snapshot_location**|**nvarchar (255)**|スナップショットファイルが保存されるフォルダーへのパスです。|  
|**last_sync_status**|**int**|同期の状態:<br /><br /> **1** = 開始<br /><br /> **2** = 成功<br /><br /> **3** = 実行中<br /><br /> **4** = アイドル<br /><br /> **5** = 前の障害の後に再試行しています<br /><br /> **6** = 失敗<br /><br /> **7** = 検証に失敗しました<br /><br /> **8** = 成功した検証<br /><br /> **9** = シャットダウンが要求されました|  
|**last_sync_summary**|**sysname**|前回の同期の結果の説明。|  
|**use_web_sync**|**bit**|サブスクリプションを HTTPS で同期できるかどうかを指定します。値 **1** は、この機能が有効になっていることを意味します。|  
|**internet_url**|**nvarchar(260)**|Web 同期用のレプリケーションリスナーの場所を表す URL。|  
|**internet_login**|**nvarchar(128)**|基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するログインです。|  
|**internet_password**|**nvarchar (524)**|基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するログインのパスワード。|  
|**internet_security_mode**|**int**|Web 同期をホストしている Web サーバーに接続するときに使用される認証モード。 値 **1** は Windows 認証を意味し、値 **0** は認証を意味し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**internet_timeout**|**int**|Web 同期要求が期限切れになるまでの時間の長さ (秒単位)。|  
|**hostname**|**nvarchar(128)**|パラメーター化された行フィルターの WHERE 句でこの関数を使用する場合に、 [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) にオーバーロードされた値を指定します。|  
|**job_login**|**nvarchar(512)**|マージエージェントを実行する Windows アカウントを指定します。このアカウントは、*ドメイン* \\ *ユーザー名*の形式で返されます。|  
|**job_password**|**sysname**|セキュリティ上の理由から、値 " **\*\*\*\*\*\*\*\*\*\*** " は常に返されます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helpmergepullsubscription** は、マージレプリケーションで使用します。 結果セットの **last_updated** で返される日付は、 *YYYYMMDD hh: mm: ss*として書式設定されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpmergepullsubscription**を実行できるのは、 **sysadmin**固定サーバーロールおよび**db_owner**固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_addmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_changemergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
