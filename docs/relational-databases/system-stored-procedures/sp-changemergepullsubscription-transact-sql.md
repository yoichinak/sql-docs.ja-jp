---
description: sp_changemergepullsubscription (Transact-sql)
title: sp_changemergepullsubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergepullsubscription
- sp_changemergepullsubscription_TSQL
helpviewer_keywords:
- sp_changemergepullsubscription
ms.assetid: 5e0d04f2-6175-44a2-ad96-a8e2986ce4c9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 39cb33678b853feadbbb20a88669f0b48a3d444a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546218"
---
# <a name="sp_changemergepullsubscription-transact-sql"></a>sp_changemergepullsubscription (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージ プル サブスクリプションのプロパティを変更します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changemergepullsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @publisher= ] 'publisher' ]  
    [ , [ @publisher_db= ] 'publisher_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値は% です。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher*は **sysname**で、既定値は% です。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャーデータベースの名前を指定します。 *publisher_db*は **sysname**,、既定値は% です。  
  
`[ @property = ] 'property'` 変更するプロパティの名前を指定します。 *プロパティ* は **sysname**,、テーブル内のいずれかの値を指定できます。  
  
`[ @value = ] 'value'` 指定したプロパティの新しい値を指定します。 *値*は **nvarchar (255)**,、テーブル内の値のいずれかを指定することができます。  
  
|プロパティ|[値]|説明|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||場所が既定の場所に加えてまたは以外の場合に、スナップショットフォルダーが格納される場所。|  
|**description**||このマージ プル サブスクリプションの説明です。|  
|**ディストリビューター**||ディストリビューターの名前。|  
|**distributor_login**||ディストリビューターで認証に使用されるログイン ID [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**distributor_password**||認証のためにディストリビューターで使用されるパスワード (暗号化) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**distributor_security_mode**|**1**|ディストリビューターへの接続時に Windows 認証を使用します。|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ディストリビューターへの接続時に認証を使用します。|  
|**dynamic_snapshot_location**||スナップショット ファイルが保存されるフォルダーへのパスです。|  
|**ftp_address**||旧バージョンとの互換性のためにのみ使用できます。 ディストリビューターのファイル転送プロトコル (FTP) サービスのネットワークアドレスを示します。|  
|**ftp_login**||旧バージョンとの互換性のためにのみ使用できます。 FTP サービスへの接続に使用するユーザー名です。|  
|**ftp_password**||旧バージョンとの互換性のためにのみ使用できます。 FTP サービスに接続するときに使用するユーザー パスワードです。|  
|**ftp_port**||旧バージョンとの互換性のためにのみ使用できます。 ディストリビューター用の FTP サービスのポート番号です。|  
|**hostname**||結合フィルターまたは論理レコードリレーションシップの WHERE 句でこの関数を使用する場合の HOST_NAME () の値を指定します。|  
|**internet_login**||基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するログインです。|  
|**internet_password**||基本認証を使用して Web 同期をホストしている Web サーバーに接続するときにマージエージェントが使用するログインのパスワード。|  
|**internet_security_mode**|**1**|Web 同期をホストしている Web サーバーに接続するときに Windows 認証を使用します。|  
||**0**|Web 同期をホストしている Web サーバーに接続するときは、基本認証を使用します。|  
|**internet_timeout**||Web 同期要求が期限切れになるまでの時間の長さ (秒単位)。|  
|**internet_url**||Web 同期用のレプリケーションリスナーの場所を表す URL。|  
|**merge_job_login**||エージェントを実行する Windows アカウントのログイン。|  
|**merge_job_password**||エージェントを実行する Windows アカウントのパスワード。|  
|**priority**||旧バージョンとの互換性のためにのみ使用できます。サブスクリプションの優先度を変更する代わりに、パブリッシャーで [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md) を実行します。|  
|**publisher_login**||パブリッシャーで認証に使用されるログイン ID [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**publisher_password**||認証のためにパブリッシャーで使用されるパスワード (暗号化) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**publisher_security_mode**|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーに接続するときに認証を使用します。|  
||**1**|パブリッシャーに接続するときに Windows 認証を使用。|  
||**2**|同期トリガーは、静的な **sysservers** エントリを使用してリモートプロシージャコール (RPC) を実行します。また、パブリッシャーは、 **sysservers** テーブルのリモートサーバーまたはリンクサーバーとして定義されている必要があります。|  
|**sync_type**|**自動**|パブリッシュされたテーブルのスキーマと初期データは、最初にサブスクライバーに転送されます。|  
||"**なし**"|サブスクライバーには、パブリッシュされたテーブルのスキーマと初期データが既にあります。システムテーブルとデータは常に転送されます。|  
|**use_ftp**|**true**|一般的なプロトコルの代わりに FTP を使用してスナップショットを取得します。|  
||**false**|スナップショットを取得するには、一般的なプロトコルを使用します。|  
|**use_web_sync**|**true**|サブスクリプションは HTTP 経由で同期できます。|  
||**false**|サブスクリプションは HTTP 上で同期できません。|  
|**use_interactive_resolver**|**true**|調整時にインタラクティブ競合回避モジュールを使用します。|  
||**false**|インタラクティブ競合回避モジュールは使用されません。|  
|**working_directory**||オプションが指定されている場合に、FTP を使用してスナップショットファイルが転送されるディレクトリへの完全修飾パスです。|  
|NULL (既定値)||*プロパティ*に対してサポートされている値の一覧を返します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_changemergepullsubscription** は、マージレプリケーションで使用します。  
  
 現在のサーバーがサブスクライバー、現在のデータベースがサブスクライバー データベースであると解釈されます。  
  
 エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changemergepullsubscription**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_dropmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepullsubscription-transact-sql.md)   
 [sp_helpmergepullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
