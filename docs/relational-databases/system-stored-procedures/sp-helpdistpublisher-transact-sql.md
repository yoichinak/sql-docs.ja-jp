---
description: sp_helpdistpublisher (Transact-SQL)
title: sp_helpdistpublisher (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistpublisher_TSQL
- sp_helpdistpublisher
helpviewer_keywords:
- sp_helpdistpublisher
ms.assetid: f207c22d-8fb2-4756-8a9d-6c51d6cd3470
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 129192de74a83232334437035599cffe24a910d8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543343"
---
# <a name="sp_helpdistpublisher-transact-sql"></a>sp_helpdistpublisher (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  ディストリビューターを使用しているパブリッシャーのプロパティを返します。 このストアドプロシージャは、ディストリビューター側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` プロパティが返されるパブリッシャーを指定します。 *publisher* は **sysname**で、既定値は **%** です。  
  
`[ @check_user = ] check_user` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|発行元の名前。|  
|**distribution_db**|**sysname**|指定されたパブリッシャーのディストリビューションデータベースです。|  
|**security_mode**|**int**|キュー更新サブスクリプションのパブリッシャー、または以外のパブリッシャーに接続するために、レプリケーションエージェントによって使用されるセキュリティモード [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証<br /><br /> **1** = Windows 認証|  
|**ログイン**|**sysname**|キュー更新サブスクリプションのパブリッシャーへの接続、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以外のパブリッシャーとの接続のため、レプリケーション エージェントで使用されるログイン名です。|  
|**password**|**nvarchar (524)**|単純な暗号化形式で返されるパスワードです。 **Sysadmin**以外のユーザーのパスワードは NULL です。|  
|**active**|**bit**|リモートパブリッシャーがローカルサーバーをディストリビューターとして使用しているかどうか。<br /><br /> **0** = いいえ<br /><br /> **1** = はい|  
|**working_directory**|**nvarchar (255)**|作業ディレクトリの名前。|  
|**テッド**|**bit**|パブリッシャーがディストリビューターに接続するときにパスワードが必要かどうかを示します。 以降のバージョンでは [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 、これは常に **0**を返す必要があります。これは、パスワードが必要であることを意味します。|  
|**thirdparty_flag**|**bit**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはサード パーティのアプリケーションによってパブリケーションが有効にされるかどうかを示します。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、oracle、または oracle ゲートウェイパブリッシャー。<br /><br /> **1** = サードパーティのアプリケーションを使用して、パブリッシャーはと統合されてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**publisher_type**|**sysname**|パブリッシャーの種類です。次のいずれかを指定できます。<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE11I**<br /><br /> **ORACLE GATEWAY **|  
|**publisher_data_source**|**nvarchar (4000)**|パブリッシャーでの OLE DB データ ソースの名前です。|  
|**storage_connection_string**|**nvarchar (4000)**|ディストリビューターまたはパブリッシャーが Azure SQL Database にある場合の作業ディレクトリのストレージアクセスキー。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helpdistpublisher** は、すべての種類のレプリケーションで使用されます。  
  
 **sp_helpdistpublisher** では、**sysadmin** 以外のログインの結果セットには、パブリッシャーのログインまたはパスワードは表示されません。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールのメンバーは、ローカルサーバーをディストリビューターとして使用している任意のパブリッシャーに対して**sp_helpdistpublisher**を実行できます。 ディストリビューションデータベースの **db_owner** 固定データベースロールまたは **replmonitor** ロールのメンバーは、そのディストリビューションデータベースを使用しているすべてのパブリッシャーに対して **sp_helpdistpublisher** を実行できます。 指定された *パブリッシャー* にあるパブリケーションのパブリケーションアクセスリストのユーザーは **sp_helpdistpublisher**を実行できます。 場合 *パブリッシャー* が指定されていない、ユーザーがアクセス権を持っているすべてのパブリッシャーの情報が返されます。  
  
## <a name="see-also"></a>参照  
 [View and Modify Distributor and Publisher Properties (ディストリビューターとパブリッシャーのプロパティの表示および変更)](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
