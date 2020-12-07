---
description: sp_help_proxy (Transact-SQL)
title: sp_help_proxy (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f0125bee2811495eefc015e6be65d30b398edeaf
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549688"
---
# <a name="sp_help_proxy-transact-sql"></a>sp_help_proxy (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  1つまたは複数のプロキシの情報を一覧表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @subsystem_name = ] 'subsystem_name' ,  
    [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>引数  
`[ @proxy_id = ] id` 情報を一覧表示するプロキシのプロキシ識別番号を指定します。 *Proxy_id*は**int**,、既定値は NULL です。 *Id*または*proxy_name*を指定できます。  
  
`[ @proxy_name = ] 'proxy_name'` 情報を一覧表示するプロキシの名前。 *Proxy_name*は**sysname**で、既定値は NULL です。 *Id*または*proxy_name*を指定できます。  
  
`[ @subsystem_name = ] 'subsystem_name'` プロキシを一覧表示するサブシステムの名前。 *Subsystem_name*は**sysname**で、既定値は NULL です。 *Subsystem_name*が指定されている場合は、*名前*も指定する必要があります。  
  
 次の表に、各サブシステムの値を示します。  
  
|[値]|説明|  
|-----------|-----------------|  
|ActiveScripting| ActiveX スクリプト|  
|CmdExec|オペレーティング システム (CmdExec)|  
|スナップショット|レプリケーション スナップショット エージェント|  
|LogReader|レプリケーション ログ リーダー エージェント|  
|配布|レプリケーションディストリビューションエージェント|  
|マージする|Replication Merge Agent|  
|QueueReader|Replication Queue Reader Agent|  
|ANALYSISQUERY|Analysis Services コマンド|  
|ANALYSISCOMMAND|Analysis Services クエリ|  
|Dts|SSIS パッケージ実行|  
|PowerShell|PowerShell スクリプト|  
  
`[ @name = ] 'name'` プロキシを一覧表示するログインの名前を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 名前は **nvarchar (256)**,、既定値は NULL です。 *Name*を指定する場合は、 *subsystem_name*も指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|プロキシの識別番号。|  
|**name**|**sysname**|プロキシの名前。|  
|**credential_identity**|**sysname**|プロキシに関連付けられている資格情報の Microsoft Windows ドメイン名とユーザー名。|  
|**有効**|**tinyint**|プロキシが有効かどうか  { **0** = 無効、 **1** = 有効}|  
|**description**|**nvarchar(1024)**|このプロキシの説明。|  
|**user_sid**|**varbinary(85)**|プロキシに関する Windows ユーザーの Windows セキュリティ ID|  
|**credential_id**|**int**|このプロキシに関連付けられている資格情報の識別子。|  
|**credential_identity_exists**|**int**|credential_identity が存在するかどうか  {0 = 存在しない、1 = 存在する}|  
  
## <a name="remarks"></a>解説  
 パラメーターを指定しない場合、 **sp_help_proxy** インスタンス内のすべてのプロキシに関する情報が一覧表示されます。  
  
 特定のサブシステムに対してログインが使用できるプロキシを特定するには、 *名前* と *subsystem_name*を指定します。 これらの引数を指定すると、 **sp_help_proxy** 指定されたログインがアクセスする可能性があり、指定したサブシステムに使用できるプロキシが一覧表示されます。  
  
## <a name="permissions"></a>アクセス許可  
 既定では、 **sysadmin** 固定サーバーロールのメンバーは、このストアドプロシージャを実行できます。 それ以外のユーザーには、 **msdb** データベースの **SQLAgentOperatorRole** 固定サーバー ロールを与える必要があります。  
  
 **Sqlagentoperatorrole**の詳細については、「 [SQL Server エージェント固定データベースロール](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」を参照してください。  
  
> [!NOTE]  
>  **Sysadmin**のメンバーがこのストアドプロシージャを実行した場合、 **credential_identity**列と**user_sid**列が結果セットに返されるだけです。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-information-for-all-proxies"></a>A. すべてのプロキシに関する情報を一覧表示する  
 次の例では、インスタンス内のすべてのプロキシに関する情報を一覧表示します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-proxy"></a>B. 特定のプロキシに関する情報を一覧表示する  
 次の例では、という名前のプロキシに関する情報を一覧表示 `Catalog application proxy` します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャの SQL Server エージェント ](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  
