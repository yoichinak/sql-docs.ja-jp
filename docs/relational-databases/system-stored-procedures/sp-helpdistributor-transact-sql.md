---
description: sp_helpdistributor (Transact-sql)
title: sp_helpdistributor (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributor_TSQL
- sp_helpdistributor
helpviewer_keywords:
- sp_helpdistributor
ms.assetid: 37b0983e-3b69-4f0f-977e-20efce0a0b97
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f2c7f0778ced979765e046634d0bb39adc01578d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549648"
---
# <a name="sp_helpdistributor-transact-sql"></a>sp_helpdistributor (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  ディストリビューター、ディストリビューションデータベース、作業ディレクトリ、およびエージェントユーザーアカウントに関する情報を一覧表示し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースまたは任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpdistributor [ [ @distributor= ] 'distributor' OUTPUT ]  
    [ , [ @distribdb= ] 'distribdb' OUTPUT ]  
    [ , [ @directory= ] 'directory' OUTPUT ]  
    [ , [ @account= ] 'account' OUTPUT ]  
    [ , [ @min_distretention= ] min_distretention OUTPUT ]  
    [ , [ @max_distretention= ] max_distretention OUTPUT ]  
    [ , [ @history_retention= ] history_retention OUTPUT ]  
    [ , [ @history_cleanupagent= ] 'history_cleanupagent' OUTPUT ]  
    [ , [ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @local = ] 'local' ]  
    [ , [ @rpcsrvname= ] 'rpcsrvname' OUTPUT ]  
    [ , [ @publisher_type = ] 'publisher_type' OUTPUT ]  
```  
  
## <a name="arguments"></a>引数  
`[ @distributor = ] 'distributor' OUTPUT` ディストリビューターの名前を指定します。 ディストリビューターは **sysname**で、既定値はです **%** 。これは、結果セットを返す唯一の値です。  
  
`[ @distribdb = ] 'distribdb' OUTPUT` ディストリビューションデータベースの名前を指定します。 *distribdb* は **sysname**で、既定値はです **%** 。これは、結果セットを返す唯一の値です。  
  
`[ @directory = ] 'directory' OUTPUT` は作業ディレクトリです。 *ディレクトリ* は **nvarchar (255)**,、既定値は **%** 、結果セットを返す唯一の値です。  
  
`[ @account = ] 'account' OUTPUT` は [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ユーザーアカウントです。 *アカウント*は **nvarchar (255)**,、既定値は **%** 、結果セットを返す唯一の値です。  
  
`[ @min_distretention = ] _min_distretentionOUTPUT` ディストリビューションの最小保有期間を時間単位で示します。 *min_distretention* は **int**,、既定値は **-1**です。  
  
`[ @max_distretention = ] _max_distretentionOUTPUT` ディストリビューションの最大保有期間を時間単位で示します。 *max_distretention* は **int**,、既定値は **-1**です。  
  
`[ @history_retention = ] _history_retentionOUTPUT` 履歴の保有期間を時間単位で示します。 *history_retention* は **int**,、既定値は **-1**です。  
  
`[ @history_cleanupagent = ] 'history_cleanupagent' OUTPUT` 履歴クリーンアップエージェントの名前を指定します。 *history_cleanupagent* は **nvarchar (100)** で、既定値はです **%** 。これは、結果セットを返す唯一の値です。  
  
`[ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT` ディストリビューションクリーンアップエージェントの名前を指定します。 *distrib_cleanupagent* は **nvarchar (100)** で、既定値はです **%** 。これは、結果セットを返す唯一の値です。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher* は **sysname**で、既定値は NULL です。  
  
`[ @local = ] 'local'` がローカルサーバーの値を取得するかどうかを指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 *local* は **nvarchar (5)**,、既定値は NULL です。  
  
`[ @rpcsrvname = ] 'rpcsrvname' OUTPUT` リモートプロシージャコールを発行するサーバーの名前を指定します。 *rpcsrvname* の部分は **sysname**で、既定 **%** 値はです。これは、結果セットを返す唯一の値です。  
  
`[ @publisher_type = ] 'publisher_type' OUTPUT` パブリッシャーのパブリッシャーの種類を示します。 *publisher_type* は **sysname**で、既定値はです **%** 。これは、結果セットを返す唯一の値です。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**ディストリビューター**|**sysname**|ディストリビューターの名前。|  
|**ディストリビューションデータベース**|**sysname**|ディストリビューションデータベースの名前。|  
|**名簿**|**nvarchar (255)**|作業ディレクトリの名前。|  
|**アカウント**|**nvarchar (255)**|Windows ユーザー アカウントの名前です。|  
|**最小 distrib.exe 保有期間**|**int**|ディストリビューションの最小保有期間。|  
|**最大 distrib.exe 保有期間**|**int**|ディストリビューションの最大保有期間。|  
|**history retention**|**int**|履歴の保有期間。|  
|**history cleanup agent**|**nvarchar (100)**|履歴クリーンアップエージェントの名前。|  
|**ディストリビューション クリーンアップ エージェント (distribution cleanup agent)**|**nvarchar (100)**|ディストリビューションクリーンアップエージェントの名前。|  
|**rpc server name**|**sysname**|リモートディストリビューターまたはローカルディストリビューターの名前。|  
|**rpc ログイン名**|**sysname**|リモート ディストリビューターに対するリモート プロシージャ呼び出しで使用するログインです。|  
|**パブリッシャーの種類**|**sysname**|パブリッシャーの種類です。次のいずれかを指定できます。<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE11I**<br /><br /> **ORACLE GATEWAY **|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helpdistributor** は、すべての種類のレプリケーションで使用されます。  
  
 **Sp_helpdistributor**の実行時に1つ以上の出力パラメーターが指定されている場合、NULL に設定されたすべての出力パラメーターには、終了時に値が割り当てられ、結果セットは返されません。 出力パラメーターが指定されていない場合は、結果セットが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 次の結果セット列または出力パラメーターは、パブリッシャーの **sysadmin** 固定サーバーロールのメンバーと、パブリケーションデータベースの **db_owner** 固定データベースロールのメンバーに返されます。  
  
|結果セット列|出力パラメーター|  
|-----------------------|----------------------|  
|account|**\@顧客**|  
|最小 distrib.exe 保有期間|**\@min_distretention**|  
|最大 distrib.exe 保有期間|**\@max_distretention**|  
|history retention|**\@history_retention**|  
|history cleanup agent|**\@history_cleanupagent**|  
|ディストリビューション クリーンアップ エージェント (distribution cleanup agent)|**\@distrib_cleanupagent**|  
|rpc ログイン名|なし|  
  
 次の結果セット列は、ディストリビューターのパブリケーション用のパブリケーション アクセス リストのユーザーに返されます。  
  
-   directory  
  
 次の結果セット列は、すべてのユーザーに返されます。  
  
|結果セット列|出力パラメーター|  
|-----------------------|----------------------|  
|ディストリビューター (distributor)|**\@ディストリビューター**|  
|ディストリビューション データベース (distribution database)|**\@distribdb**|  
|rpc server name|**\@rpcsrvname**|  
|publisher type|**\@publisher_type**|  
  
## <a name="see-also"></a>参照  
 [View and Modify Distributor and Publisher Properties (ディストリビューターとパブリッシャーのプロパティの表示および変更)](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
