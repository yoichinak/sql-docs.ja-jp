---
description: sp_helpmergesubscription (Transact-sql)
title: sp_helpmergesubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergesubscription
- sp_helpmergesubscription_TSQL
helpviewer_keywords:
- sp_helpmergesubscription
ms.assetid: da564112-f769-4e67-9251-5699823e8c86
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 48d40b3209311968443a6c6d2b713b4aa1e3d43a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535199"
---
# <a name="sp_helpmergesubscription-transact-sql"></a>sp_helpmergesubscription (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  プッシュとプルの両方のマージパブリケーションに対するサブスクリプションに関する情報を返します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されるか、サブスクリプションデータベースの再パブリッシュサブスクライバーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergesubscription [ [ @publication=] 'publication']  
    [ , [ @subscriber=] 'subscriber']  
    [ , [ @subscriber_db=] 'subscriber_db']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
    [ , [ @found=] 'found' OUTPUT]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* の **sysname**,、既定値は **%** です。 パブリケーションは既に存在し、識別子のルールに準拠している必要があります。 NULL または **%** の場合、現在のデータベース内のすべてのマージパブリケーションおよびサブスクリプションに関する情報が返されます。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前を指定します。 *サブスクライバー* の **sysname**,、既定値は **%** です。 NULL または% の場合、指定されたパブリケーションに対するすべてのサブスクリプションに関する情報が返されます。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクリプションデータベースの名前を指定します。 *subscriber_db*のデータ型は **sysname**で、既定値はで **%** 、すべてのサブスクリプションデータベースに関する情報が返されます。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 パブリッシャーは有効なサーバーである必要があります。 *publisher*のデータ型は **sysname**で、既定値はで **%** 、すべてのパブリッシャーに関する情報が返されます。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャーデータベースの名前を指定します。 *publisher_db*のデータ型は **sysname**で、既定値はで **%** 、すべてのパブリッシャーデータベースに関する情報が返されます。  
  
`[ @subscription_type = ] 'subscription_type'` サブスクリプションの種類を示します。 *subscription_type*は **nvarchar (15)** で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**push** (既定値)|プッシュ サブスクリプション|  
|**だとすると**|プルサブスクリプション|  
|**両方とも**|プッシュおよびプル サブスクリプションの両方|  
  
`[ @found = ] 'found'OUTPUT` は、行を返すことを示すフラグです。 *見つかった*は **int** と出力パラメーターで、既定値は NULL です。 **1** は、パブリケーションが見つかったことを示します。 **0** は、パブリケーションが見つからないことを示します。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**sysname**|サブスクリプションの名前。|  
|**レプリケーション**|**sysname**|パブリケーションの名前。|  
|**publisher**|**sysname**|パブリッシャーの名前。|  
|**publisher_db**|**sysname**|パブリッシャーデータベースの名前。|  
|**サブスクライバ**|**sysname**|サブスクライバーの名前。|  
|**subscriber_db**|**sysname**|サブスクリプションデータベースの名前。|  
|**status**|**int**|サブスクリプションの状態:<br /><br /> **0** = すべてのジョブが開始を待機しています<br /><br /> **1** = 1 つ以上のジョブが開始されています<br /><br /> **2** = すべてのジョブが正常に実行されました<br /><br /> **3** = 少なくとも1つのジョブが実行されています<br /><br /> **4** = すべてのジョブがスケジュールされ、アイドル状態になっている<br /><br /> **5** = 少なくとも1つのジョブが前回のエラーの発生後に実行しようとしています<br /><br /> **6** = 少なくとも1つのジョブを正常に実行できませんでした|  
|**subscriber_type**|**int**|サブスクライバーの種類。|  
|**subscription_type**|**int**|サブスクリプションの種類:<br /><br /> **0** = プッシュ<br /><br /> **1** = プル<br /><br /> **2** = 両方|  
|**priority**|**float (8)**|サブスクリプションの優先度を示す数値。|  
|**sync_type**|**tinyint**|サブスクリプションの同期の種類。|  
|**description**|**nvarchar (255)**|マージ サブスクリプションの簡単な説明。|  
|**merge_jobid**|**binary(16)**|マージエージェントのジョブ ID。|  
|**full_publication**|**tinyint**|サブスクリプションが完全またはフィルター選択されたパブリケーションであるかどうか。|  
|**offload_enabled**|**bit**|レプリケーションエージェントのオフロード実行がサブスクライバーで実行されるように設定されているかどうかを指定します。 NULL の場合、実行はパブリッシャー側で実行されます。|  
|**offload_server**|**sysname**|エージェントが動作しているサーバーの名前。|  
|**use_interactive_resolver**|**int**|調整時に対話型の競合回避モジュールを使用するかどうかを示します。 **0**の場合、インタラクティブ競合回避モジュールは使用されません。|  
|**hostname**|**sysname**|サブスクリプションが [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) 関数の値によってフィルター処理されるときに指定される値。|  
|**subscriber_security_mode**|**smallint**|サブスクライバーのセキュリティモードを指定します。 **1** は Windows 認証を、 **0** は認証を意味し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**subscriber_login**|**sysname**|サブスクライバーのログイン名を指定します。|  
|**subscriber_password**|**sysname**|実際のサブスクライバーパスワードは返されません。 結果は "" という文字列でマスクされ **\*\*\*\*\*\*** ます。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helpmergesubscription** は、パブリッシャーまたは再パブリッシュサブスクライバーに格納されているサブスクリプション情報を返すために、マージレプリケーションで使用されます。  
  
 匿名サブスクリプションの場合、 *subscription_type*値は常に **1** (プル) です。 ただし、匿名サブスクリプションに関する情報を表示するには、サブスクライバーで [sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md) を実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpmergesubscription**を実行できるのは、 **sysadmin**固定サーバーロールのメンバー、 **db_owner**固定データベースロール、またはサブスクリプションが属しているパブリケーションのパブリケーションアクセスリストのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_addmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
