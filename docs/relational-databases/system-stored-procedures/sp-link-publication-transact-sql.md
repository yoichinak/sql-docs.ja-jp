---
description: sp_link_publication (Transact-SQL)
title: sp_link_publication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_link_publication_TSQL
- sp_link_publication
helpviewer_keywords:
- sp_link_publication
ms.assetid: 1945ed24-f9f1-4af6-94ca-16d8e864706e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b80c28d86ae4d7022ad8784adfa7ab9023e3ebd0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543237"
---
# <a name="sp_link_publication-transact-sql"></a>sp_link_publication (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  パブリッシャーへの接続時に即時更新サブスクリプションの同期トリガーによって使用される構成およびセキュリティ情報を設定します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
> [!IMPORTANT]
>  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
> 
> [!IMPORTANT]
>  特定の条件下で、サブスクライバーが [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 以降を実行していて、パブリッシャーが以前のバージョンを実行している場合、このストアドプロシージャは失敗する可能性があります。 このシナリオでストアドプロシージャが失敗した場合は、パブリッシャーを [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 以降にアップグレードしてください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_link_publication [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @security_mode = ] security_mode  
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ]'password' ]  
    [ , [ @distributor = ] 'distributor' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` リンク先のパブリッシャーの名前を指定します。 *publisher* は **sysname**で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` リンク先のパブリッシャーデータベースの名前を指定します。 *publisher_db* は **sysname**であり、既定値はありません。  
  
`[ @publication = ] 'publication'` リンクするパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @security_mode = ] security_mode` サブスクライバーが即時更新のためにリモートパブリッシャーに接続するために使用するセキュリティモードを示します。 *security_mode* は **int**,、これらの値のいずれかを指定できます。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
|[値]|説明|  
|-----------|-----------------|  
|**0**|では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 *ログイン* と *パスワード*として、このストアドプロシージャで指定されたログインで認証を使用します。<br /><br /> 注: 以前のバージョンのでは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、このオプションを使用して動的リモートプロシージャ呼び出し (RPC) を指定していました。|  
|**1**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サブスクライバーで変更を行うユーザーのセキュリティコンテキスト (認証または Windows 認証) を使用します。<br /><br /> 注: このアカウントは、十分な特権を持つパブリッシャーにも存在する必要があります。 Windows 認証を使用する場合は、セキュリティアカウントの委任がサポートされている必要があります。|  
|**2**|**Sp_link_publication**を使用して作成された、既存のユーザー定義のリンクサーバーログインを使用します。|  
  
`[ @login = ] 'login'` ログインを示します。 *login* のデータ型は **sysname** で、既定値は NULL です。 *Security_mode*が**0**の場合は、このパラメーターを指定する必要があります。  
  
`[ @password = ] 'password'` パスワードを入力します。 *パスワード* は **sysname**,、既定値は NULL です。 *Security_mode*が**0**の場合は、このパラメーターを指定する必要があります。  
  
`[ @distributor = ] 'distributor'` ディストリビューターの名前を指定します。 *ディストリビューター* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_link_publication** は、トランザクションレプリケーションで即時更新サブスクリプションによって使用されます。  
  
 **sp_link_publication** は、プッシュサブスクリプションとプルサブスクリプションの両方に使用できます。 サブスクリプションが作成される前または後に呼び出すことができます。 [MSsubscription_properties &#40;transact-sql&#41;](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)システムテーブルにエントリが挿入または更新されます。  
  
 プッシュサブスクリプションの場合、このエントリは [sp_subscription_cleanup &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)によってクリーンアップできます。 プルサブスクリプションの場合、エントリをクリーンアップするには [&#40;transact-sql&#41;を sp_droppullsubscription ](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md) するか、 [transact-sql &#40;&#41;sp_subscription_cleanup ](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)します。 また、セキュリティ上の問題については、 [MSsubscription_properties &#40;transact-sql&#41;](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)システムテーブルのエントリをクリアするために、NULL パスワードを使用して**sp_link_publication**を呼び出すこともできます。  
  
 即時更新サブスクライバーがパブリッシャーに接続するときに使用される既定のモードでは、Windows 認証を使用した接続は許可されません。 Windows 認証のモードで接続するには、パブリッシャーに対してリンクサーバーを設定する必要があります。また、即時更新サブスクライバーは、サブスクライバーの更新時にこの接続を使用する必要があります。 そのためには、 **sp_link_publication**を*security_mode*2 で実行する必要があり  =  **2**ます。 Windows 認証を使用する場合は、セキュリティアカウントの委任がサポートされている必要があります。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent_failover](../../relational-databases/replication/codesnippet/tsql/sp-link-publication-tran_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_link_publication**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_droppullsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
