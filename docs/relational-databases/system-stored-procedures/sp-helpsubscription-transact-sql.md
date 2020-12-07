---
description: sp_helpsubscription (Transact-sql)
title: sp_helpsubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscription_TSQL
- sp_helpsubscription
helpviewer_keywords:
- sp_helpsubscription
ms.assetid: ff96bcbf-e2b9-4da8-8515-d80d4ce86c16
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5ff06497437017fd6771a7402c18d16a5ee6f94b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543264"
---
# <a name="sp_helpsubscription-transact-sql"></a>sp_helpsubscription (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  特定のパブリケーション、アーティクル、サブスクライバー、またはサブスクリプションのセットに関連付けられているサブスクリプション情報を一覧表示します。 このストアドプロシージャは、パブリッシャー側のパブリケーションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpsubscription [ [ @publication = ] 'publication' ]   
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]   
    [ , [ @found=] found OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 関連付けられているパブリケーションの名前を指定します。 *publication* のデータ型は **sysname**で、既定値はです **%** 。この場合、このサーバーのすべてのサブスクリプション情報が返されます。  
  
`[ @article = ] 'article'` アーティクルの名前を指定します。 *アーティクル* は **sysname**で、既定値はです **%** 。これにより、選択したパブリケーションとサブスクライバーのすべてのサブスクリプション情報が返されます。 **All**の場合、パブリケーションの完全なサブスクリプションに対して1つのエントリのみが返されます。  
  
`[ @subscriber = ] 'subscriber'` サブスクリプション情報を取得するサブスクライバーの名前を指定します。 *サブスクライバー* のデータ型は **sysname**で、既定値はです **%** 。これにより、選択したパブリケーションとアーティクルのすべてのサブスクリプション情報が返されます。  
  
`[ @destination_db = ] 'destination_db'` 転送先データベースの名前を指定します。 *destination_db* は **sysname**で、既定値は **%** です。  
  
`[ @found = ] 'found'OUTPUT` は、行を返すことを示すフラグです。 *見つかった*は **int** と出力パラメーターで、既定値は23456です。  
  
 **1** は、パブリケーションが見つかったことを示します。  
  
 **0** は、パブリケーションが見つからないことを示します。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher* は **sysname**で、既定値は現在のサーバーの名前です。  
  
> [!NOTE]  
>  Oracle パブリッシャーの場合を除き、*パブリッシャー*を指定することはできません。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**サブスクライバ**|**sysname**|サブスクライバーの名前。|  
|**レプリケーション**|**sysname**|パブリケーションの名前。|  
|**記事**|**sysname**|アーティクルの名前。|  
|**転送先データベース**|**sysname**|レプリケートされたデータの格納先のデータベースの名前。|  
|**サブスクリプションの状態**|**tinyint**|サブスクリプションの状態:<br /><br /> **0** = 非アクティブ<br /><br /> **1** = サブスクライブ済み<br /><br /> **2** = アクティブ|  
|**同期の種類**|**tinyint**|サブスクリプションの同期の種類:<br /><br /> **1** = 自動<br /><br /> **2** = なし|  
|**サブスクリプションの種類**|**int**|サブスクリプションの種類:<br /><br /> **0** = プッシュ<br /><br /> **1** = プル<br /><br /> **2** = 匿名|  
|**full subscription**|**bit**|サブスクリプションがパブリケーション内のすべてのアーティクルを対象としているかどうかを示します。<br /><br /> **0** = いいえ<br /><br /> **1** = はい|  
|**サブスクリプション名**|**nvarchar (255)**|サブスクリプションの名前。|  
|**更新モード**|**int**|**0** = 読み取り専用<br /><br /> **1** = 即時更新サブスクリプション|  
|**distribution job id**|**binary(16)**|ディストリビューション エージェントのジョブ ID。|  
|**loopback_detection**|**bit**|ディストリビューション エージェントが、サブスクライバーで発生したトランザクションをサブスクライバーに戻すかどうかを示します。<br /><br /> **0** = 返送します。<br /><br /> **1** = を返しません。<br /><br /> 双方向トランザクション レプリケーションで使用されます。 詳細については、「 [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md)」を参照してください。|  
|**offload_enabled**|**bit**|レプリケーションエージェントのオフロード実行がサブスクライバーで実行されるように設定されているかどうかを指定します。<br /><br /> **0**の場合、エージェントはパブリッシャーで実行されます。<br /><br /> **1**の場合、エージェントはサブスクライバーで実行されます。|  
|**offload_server**|**sysname**|リモートエージェントのアクティブ化が有効になっているサーバーの名前。 NULL の場合は、 [MSdistribution_agents](../../relational-databases/system-tables/msdistribution-agents-transact-sql.md) テーブルに一覧表示されている現在の offload_server が使用されます。|  
|**dts_package_name**|**sysname**|データ変換サービス (DTS) パッケージの名前を指定します。|  
|**dts_package_location**|**int**|DTS パッケージの場所 (サブスクリプションに割り当てられている場合)。 パッケージがある場合、値 **0** は **ディストリビューター**でのパッケージの場所を指定します。 値 **1** は **サブスクライバー**を指定します。|  
|**subscriber_security_mode**|**smallint**|サブスクライバーのセキュリティモードを指定します。 **1** は Windows 認証を、 **0** は認証を意味し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**subscriber_login**|**sysname**|サブスクライバーのログイン名を指定します。|  
|**subscriber_password**||実際のサブスクライバーパスワードは返されません。 結果は、"**&#42;&#42;&#42;&#42;&#42;&#42;**" 文字列によってマスクされます。|  
|**job_login**|**sysname**|ディストリビューションエージェントの実行に使用する Windows アカウントの名前。|  
|**job_password**||実際のジョブ パスワードは返されません。 結果は、"**&#42;&#42;&#42;&#42;&#42;&#42;**" 文字列によってマスクされます。|  
|**distrib_agent_name**|**nvarchar (100)**|サブスクリプションを同期するエージェントジョブの名前。|  
|**subscriber_type**|**tinyint**|サブスクライバーの種類。次のいずれかを指定できます。<br /><br /> **0** = SQL Server サブスクライバー<br /><br /> **1** = ODBC データソースサーバー<br /><br /> **2** = Microsoft JET データベース (非推奨)<br /><br /> **3** = OLE DB プロバイダー|  
|**subscriber_provider**|**sysname**|SQL Server 以外のデータソースの OLE DB プロバイダーが登録されている一意のプログラム識別子 (PROGID)。|  
|**subscriber_datasource**|**nvarchar (4000)**|OLE DB プロバイダーで認識されるデータ ソースの名前。|  
|**subscriber_providerstring**|**nvarchar (4000)**|データソースを識別する OLE DB プロバイダー固有の接続文字列。|  
|**subscriber_location**|**nvarchar (4000)**|OLE DB プロバイダーによって認識されるデータベースの場所|  
|**subscriber_catalog**|**sysname**|OLE DB プロバイダーに接続するときに使用するカタログ。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helpsubscription** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 実行権限は、既定で **public** ロールに設定されています。 ユーザーに返されるのは、ユーザーが自分で作成したサブスクリプションの情報だけです。 すべてのサブスクリプションに関する情報は、パブリッシャーの **sysadmin** 固定サーバーロールのメンバー、またはパブリケーションデータベースの固定データベースロール **db_owner** のメンバーに返されます。  
  
## <a name="see-also"></a>参照  
 [sp_addsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
