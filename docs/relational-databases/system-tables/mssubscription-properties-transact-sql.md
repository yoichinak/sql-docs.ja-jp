---
description: MSsubscription_properties (Transact-SQL)
title: MSsubscription_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscription_properties
- MSsubscription_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_properties system table
ms.assetid: f96fc1ae-b798-4b05-82a7-564ae6ef23b8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8895f78aa31e5fa38b52de7163ddb2a1554e5617
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545512"
---
# <a name="mssubscription_properties-transact-sql"></a>MSsubscription_properties (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSsubscription_properties**テーブルには、サブスクライバーでレプリケーションエージェントを実行するために必要なパラメーター情報の行が含まれています。 このテーブルは、プルサブスクリプションの場合はサブスクライバー側のサブスクリプションデータベースに格納され、プッシュサブスクリプションの場合はディストリビューター側のディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|パブリッシャーの名前です。|  
|**publisher_db**|**sysname**|パブリッシャーデータベースの名前。|  
|**レプリケーション**|**sysname**|パブリケーションの名前を指定します。|  
|**publication_type**|**int**|パブリケーションの種類です。<br /><br /> **0** = トランザクション。<br /><br /> **2** = Merge。|  
|**publisher_login**|**sysname**|パブリッシャーで認証に使用されるログイン ID [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**publisher_password**|**nvarchar (524)**|パブリッシャーで認証に使用されるパスワード (暗号化されたもの) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**publisher_security_mode**|**int**|パブリッシャーで実装されているセキュリティ モード。<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 認証。<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 認証。<br /><br /> **2** = 同期トリガーは、静的な **sysservers** エントリを使用してリモートプロシージャコール (RPC) を実行します。また、 *パブリッシャー* は、 **sysservers** テーブルのリモートサーバーまたはリンクサーバーとして定義されている必要があります。|  
|**ディストリビューター**|**sysname**|ディストリビューターの名前です。|  
|**distributor_login**|**sysname**|SQL Server 認証のためにディストリビューターで使用されるログイン ID。|  
|**distributor_password**|**nvarchar (524)**|ディストリビューターで認証に使用されるパスワード (暗号化されたもの) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**distributor_security_mode**|**int**|ディストリビューターで実装されているセキュリティ モード。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。<br /><br /> **1** = Windows 認証。|  
|**ftp_address**|**sysname**|ディストリビューターのファイル転送プロトコル (FTP) サービスのネットワークアドレス。|  
|**ftp_port**|**int**|ディストリビューターの FTP サービスのポート番号。|  
|**ftp_login**|**sysname**|FTP サービスへの接続に使用するユーザー名。|  
|**ftp_password**|**nvarchar (524)**|FTP サービスへの接続に使用される u. ユーザーパスワード。|  
|**alt_snapshot_folder**|**nvarchar (255)**|スナップショットの代替フォルダーの場所を指定します。|  
|**working_directory**|**nvarchar (255)**|データファイルとスキーマファイルの格納に使用する作業ディレクトリの名前。|  
|**use_ftp**|**bit**|スナップショットを取得するために通常のプロトコルではなく FTP を使用することを指定します。 **1**の場合、FTP が使用されます。|  
|**dts_package_name**|**sysname**|データ変換サービス (DTS) パッケージの名前を指定します。|  
|**dts_package_password**|**nvarchar (524)**|パッケージのパスワードを指定します。|  
|**dts_package_location**|**int**|DTS パッケージが格納されている場所です。|  
|**enabled_for_syncmgr**|**bit**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] 同期マネージャーを介してサブスクリプションを同期化できるかどうかを示します。<br /><br /> **0** = サブスクリプションは同期マネージャーに登録されていません。<br /><br /> **1** = サブスクリプションは同期マネージャーに登録されており、を起動せずに同期でき [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。|  
|**offload_agent**|**bit**|エージェントをリモートからアクティブ化できるかどうかを指定します。 **0**の場合、エージェントをリモートでアクティブにすることはできません。|  
|**offload_server**|**sysname**|リモートからのアクティブ化に使用するサーバーのネットワーク名を指定します。|  
|**dynamic_snapshot_location**|**nvarchar (255)**|スナップショットファイルを保存するフォルダーへのパスを指定します。|  
|**use_web_sync**|**bit**|サブスクリプションを HTTP で同期できるかどうかを指定します。 値 **1** は、この機能が有効になっていることを意味します。|  
|**internet_url**|**nvarchar(260)**|Web 同期に対するレプリケーション リスナーの位置を表す URL。|  
|**internet_login**|**sysname**|認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するログインです [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**internet_password**|**nvarchar (524)**|認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するログインのパスワード [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**internet_security_mode**|**int**|Web 同期をホストしている Web サーバーに接続するときに使用される認証モード。値 **1** は Windows 認証を意味し、値 **0** は認証を意味し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**internet_timeout**|**int**|Web 同期要求が期限切れとなるまでの時間の長さ (秒単位)。|  
|**hostname**|**sysname**|結合フィルターまたは論理レコードリレーションシップの**where**句でこの関数を使用する場合の**HOST_NAME**の値を指定します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
