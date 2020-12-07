---
description: sp_changemergesubscription (Transact-sql)
title: sp_changemergesubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergesubscription_TSQL
- sp_changemergesubscription
helpviewer_keywords:
- sp_changemergesubscription
ms.assetid: fd820f35-c189-4e2d-884d-b60c1c469f58
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d1df7bd62aa2cecb23096121630eb0d89ce21dc8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536664"
---
# <a name="sp_changemergesubscription-transact-sql"></a>sp_changemergesubscription (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージのプッシュ サブスクリプションについて、選択したプロパティを変更します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
> [!IMPORTANT]  
>  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changemergesubscription [ [ @publication= ] 'publication' ]  
    [ , [ @subscriber= ] 'subscriber'  
    [ , [ @subscriber_db= ] 'subscriber_db' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 変更するパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値は NULL です。 変更できるのは既存のパブリケーションだけであり、識別子の規則に従う必要があります。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前を指定します。 *サブスクライバー* の **sysname**,、既定値は NULL です。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクリプションデータベースの名前を指定します。 *subscriber_db*は **sysname**,、既定値は NULL です。  
  
`[ @property = ] 'property'` 指定したパブリケーションの変更対象となるプロパティを指定します。 *プロパティ* は **sysname**,、テーブル内のいずれかの値を指定できます。  
  
`[ @value = ] 'value'` 指定した *プロパティ*の新しい値を指定します。 *値* は **nvarchar (255)**,、テーブル内の値のいずれかを指定することができます。  
  
|プロパティ|[値]|説明|  
|--------------|-----------|-----------------|  
|**description**||マージ サブスクリプションの説明。|  
|**priority**||サブスクリプションの優先度です。 既定の競合回避モジュールでは、競合が検出された場合に優先される優先順位を使用します。|  
|**merge_job_login**||エージェントを実行する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントのログイン。|  
|**merge_job_password**||エージェントを実行する Windows アカウントのパスワード。|  
|**publisher_security_mode**|**1**|パブリッシャーに接続するときに Windows 認証を使用。|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]パブリッシャーに接続するときに認証を使用します。|  
|**publisher_login**||パブリッシャーでのログイン名。|  
|**publisher_password**||指定されたパブリッシャーログインの強力なパスワード。|  
|**subscriber_security_mode**|**1**|サブスクライバーに接続するときに Windows 認証を使用。|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サブスクライバーへの接続時に認証を使用します。|  
|**subscriber_login**||サブスクライバーでのログイン名。|  
|**subscriber_password**||指定されたサブスクライバーログインの強力なパスワード。|  
|**sync_type**|**自動**|パブリッシュされたテーブルのスキーマと初期データは、最初にサブスクライバーに転送されます。|  
||"**なし**"|サブスクライバーには、パブリッシュされたテーブルのスキーマと初期データが既にあります。システムテーブルとデータは常に転送されます。|  
|**use_interactive_resolver**|**true**|対話的に競合を回避できるすべてのアーティクルについて、対話的に競合を解決できるようにします。|  
||**false**|既定の競合回避モジュールまたはカスタム競合回避モジュールを使用して自動的に競合を解決します。|  
|NULL (既定値)|NULL (既定値)||  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_changemergesubscription** は、マージレプリケーションで使用します。  
  
 エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changemergesubscription**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_addmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [sp_helpmergesubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
