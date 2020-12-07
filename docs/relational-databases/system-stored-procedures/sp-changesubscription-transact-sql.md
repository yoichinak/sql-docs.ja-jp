---
description: sp_changesubscription (Transact-sql)
title: sp_changesubscription (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- changesubscription
- sp_changesubscription
- changesubscription_TSQL
- sp_changesubscription_TSQL
helpviewer_keywords:
- sp_changesubscription
ms.assetid: f9d91fe3-47cf-4915-b6bf-14c9c3d8a029
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d1dd4a0fc40cf24896de912c1254b154a5538866
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543695"
---
# <a name="sp_changesubscription-transact-sql"></a>sp_changesubscription (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  キュー更新トランザクションレプリケーションに関係するスナップショットまたはトランザクションプッシュサブスクリプションまたはプルサブスクリプションのプロパティを変更します。 他のすべての種類のプルサブスクリプションのプロパティを変更するには、 [sp_change_subscription_properties &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)を使用します。 パブリッシャー側のパブリケーションデータベースに対して**sp_changesubscription**が実行されます。  
  
> [!IMPORTANT]  
>  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changesubscription [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 変更するパブリケーションの名前を指定します。 *publication*は **sysname**で、既定値はありません。  
  
`[ @article = ] 'article'` 変更するアーティクルの名前を指定します。 *アーティクル* は **sysname**で、既定値はありません。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前を指定します。 *サブスクライバー* は **sysname**,、既定値はありません。  
  
`[ @destination_db = ] 'destination_db'` サブスクリプションデータベースの名前を指定します。 *destination_db* は **sysname**であり、既定値はありません。  
  
`[ @property = ] 'property'` 指定されたサブスクリプションの変更対象となるプロパティを指定します。 *プロパティ* は **nvarchar (30)**,、テーブル内の値のいずれかを指定することができます。  
  
`[ @value = ] 'value'` 指定した *プロパティ*の新しい値を指定します。 *値* は **nvarchar (4000)**,、テーブル内の値のいずれかを指定することができます。  
  
|プロパティ|[値]|説明|  
|--------------|-----------|-----------------|  
|**distrib_job_login**||エージェントを実行する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントのログイン。|  
|**distrib_job_password**||エージェントを実行する Windows アカウントのパスワード。|  
|**subscriber_catalog**||OLE DB プロバイダーに接続するときに使用するカタログ。 このプロパティは、以外のサブスクライバーに対してのみ有効です [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|**subscriber_datasource**||OLE DB プロバイダーで認識されるデータ ソースの名前。 *このプロパティは、以外の場合にのみ有効です* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。*サブスクライバー。*|  
|**subscriber_location**||OLE DB プロバイダーによって認識されるデータベースの場所です。 *このプロパティは、以外の場合にのみ有効です* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。*サブスクライバー。*|  
|**subscriber_login**||サブスクライバーでのログイン名。|  
|**subscriber_password**||指定されたログインの強力なパスワード。|  
|**subscriber_security_mode**|**1**|サブスクライバーに接続するときに Windows 認証を使用。|  
||**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サブスクライバーへの接続時に認証を使用します。|  
|**subscriber_provider**||データソース以外の OLE DB プロバイダーが登録されている一意のプログラム識別子 (PROGID) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *このプロパティは、以外の場合にのみ有効です* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。*サブスクライバー。*|  
|**subscriber_providerstring**||データソースを識別する OLE DB プロバイダー固有の接続文字列。 *このプロパティは、以外の場合にのみ有効です* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。*サブスクライバー。*|  
|**subscriptionstreams**||変更のバッチをサブスクライバーに並列的に適用するために、ディストリビューションエージェントごとに許可される接続の数を指定します。 パブリッシャーでは、 **1** ~ **64** の範囲の値がサポートされてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 以外の**0** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバー、Oracle パブリッシャー、またはピアツーピアサブスクリプションの場合、このプロパティは0にする必要があります。|  
|**subscriber_type**|**1**|ODBC データソースサーバー|  
||**3**|OLE DB プロバイダー|  
|**memory_optimized**|**bit**|サブスクリプションがメモリ最適化テーブルをサポートしていることを示します。 *memory_optimized* は **ビット**です。1は true (サブスクリプションはメモリ最適化テーブルをサポートします) です。|  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーに対して*パブリッシャー*を指定することはできません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_changesubscription** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 **sp_changesubscription** は、キュー更新トランザクションレプリケーションに関係するプッシュサブスクリプションまたはプルサブスクリプションのプロパティを変更する場合にのみ使用できます。 他のすべての種類のプルサブスクリプションのプロパティを変更するには、 [sp_change_subscription_properties &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)を使用します。  
  
 エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changesubscription**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_addsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)  
  
  
