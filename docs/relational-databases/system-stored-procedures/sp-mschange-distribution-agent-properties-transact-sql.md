---
title: sp_MSchange_distribution_agent_properties (T-sql)
description: SQL Server レプリケーショントポロジのディストリビューションエージェントのプロパティを変更するために使用される sp_MSchange_distribution_agent_properties ストアドプロシージャについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_MSchange_distribution_agent_properties
- sp_MSchange_distribution_agent_properties_TSQL
helpviewer_keywords:
- sp_MSchange_distribution_agent_properties
ms.assetid: 7dac5e68-bf84-433a-a531-66921f35126f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 276e56e28c7455949fcf12b32f684365c20c618f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547639"
---
# <a name="sp_mschange_distribution_agent_properties-transact-sql"></a>sp_MSchange_distribution_agent_properties (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  以降のバージョンのディストリビューターで実行されるディストリビューションエージェントジョブのプロパティを変更し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ます。 このストアドプロシージャは、パブリッシャーがのインスタンスで実行されている場合に、プロパティを変更するために使用し [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ます。 このストアドプロシージャは、ディストリビューター側のディストリビューションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_MSchange_distribution_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @subscriber = ] 'subscriber'   
        , [ @subscriber_db = ] 'subscriber_db'   
        , [ @property = ] 'property'   
        , [ @value = ] 'value' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher* は **sysname**で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` パブリケーションデータベースの名前を指定します。 *publisher_db* は **sysname**であり、既定値はありません。  
  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前を指定します。 *サブスクライバー* は **sysname**,、既定値はありません。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクリプションデータベースの名前を指定します。 *subscriber_db* は **sysname**であり、既定値はありません。  
  
`[ @property = ] 'property'` 変更するパブリケーションプロパティを設定します。 *プロパティ* は **sysname**,、既定値はありません。  
  
`[ @value = ] 'value'` 新しいプロパティ値を指定します。 *値* は **nvarchar (524)**,、既定値は NULL です。  
  
 次の表では、変更可能なディストリビューションエージェントジョブのプロパティと、それらのプロパティの値に関する制限について説明します。  
  
|プロパティ|[値]|説明|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||エージェントを実行する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントのログイン。|  
|**distrib_job_password**||エージェントジョブを実行する Windows アカウントのパスワード。|  
|**subscriber_catalog**||OLE DB プロバイダーに接続するときに使用するカタログ。 *このプロパティは、以外の場合にのみ有効です* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。*サブスクライバー。*|  
|**subscriber_datasource**||OLE DB プロバイダーで認識されるデータ ソースの名前。 *このプロパティは、以外の場合にのみ有効です* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。*サブスクライバー。*|  
|**subscriber_location**||OLE DB プロバイダーによって認識されるデータベースの場所です。 *このプロパティは、以外の場合にのみ有効です* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。*サブスクライバー。*|  
|**subscriber_login**||サブスクライバーに接続してサブスクリプションを同期するときに使用するログインです。|  
|**subscriber_password**||サブスクライバーのパスワード。<br /><br /> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]|  
|**subscriber_provider**||データソース以外の OLE DB プロバイダーが登録されている一意のプログラム識別子 (PROGID) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *このプロパティは、以外の場合にのみ有効です* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。*サブスクライバー。*|  
|**subscriber_providerstring**||データソースを識別する OLE DB プロバイダー固有の接続文字列。 *このプロパティは、SQL Server 以外のサブスクライバーに対してのみ有効です。*|  
|**subscriber_security_mode**|**1**|[Windows 認証]。<br /><br /> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証。|  
|**subscriber_type**|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバ|  
||**1**|ODBC データソースサーバー|  
||**3**|OLE DB プロバイダー|  
|**subscriptionstreams**||変更のバッチをサブスクライバーに並列的に適用するために、ディストリビューション エージェントごとに許可される接続の数を表します。 *以外の場合はサポートされません* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。*サブスクライバー、Oracle パブリッシャー、またはピアツーピアサブスクリプション。*|  
  
> [!NOTE]  
>  エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_MSchange_distribution_agent_properties** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 パブリッシャーが以降のバージョンのインスタンスで実行されている場合は [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 、 [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) を使用して、ディストリビューターで実行されるプッシュサブスクリプションを同期するマージエージェントジョブのプロパティを変更する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_MSchange_distribution_agent_properties**を実行できるのは、ディストリビューター側の固定サーバーロール**sysadmin**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_addpushsubscription_agent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)   
 [sp_addsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)  
  
  
