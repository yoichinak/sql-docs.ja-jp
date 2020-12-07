---
description: sp_addsynctriggers (Transact-sql)
title: sp_addsynctriggers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsynctriggers_TSQL
- sp_addsynctriggers
helpviewer_keywords:
- sp_addsynctriggers
ms.assetid: e37d0c3b-19bf-4719-9535-96ba361372b3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 38c0e33c780e13f11266d8cafde93fbdca2ebc11
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539225"
---
# <a name="sp_addsynctriggers-transact-sql"></a>sp_addsynctriggers (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  すべての種類の更新可能なサブスクリプション (即時更新、キュー更新、およびフェールオーバーとしてキュー更新を使用する即時更新) で使用されるトリガーを、サブスクライバー側で作成します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
> [!IMPORTANT]  
>  **Sp_addsynctrigger**の代わりに[sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)プロシージャを使用する必要があります。 [sp_script_synctran_commands](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md) は、 **sp_addsynctrigger** 呼び出しを含むスクリプトを生成します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addsynctriggers [ @sub_table = ] 'sub_table'  
        , [ @sub_table_owner = ] 'sub_table_owner'  
        , [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @ins_proc = ] 'ins_proc'   
        , [ @upd_proc = ] 'upd_proc'   
        , [ @del_proc = ] 'del_proc'   
        , [ @cftproc = ] 'cftproc'  
        , [ @proc_owner = ] 'proc_owner'  
    [ , [ @identity_col = ] 'identity_col' ]  
    [ , [ @ts_col = ] 'timestamp_col' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]   
        , [ @primary_key_bitmap = ] 'primary_key_bitmap'  
    [ , [ @identity_support = ] identity_support ]  
    [ , [ @independent_agent = ] independent_agent ]  
        , [ @distributor = ] 'distributor'   
    [ , [ @pubversion = ] pubversion  
```  
  
## <a name="arguments"></a>引数  
`[ @sub_table = ] 'sub_table'` サブスクライバーテーブルの名前を指定します。 *sub_table* は **sysname**であり、既定値はありません。  
  
`[ @sub_table_owner = ] 'sub_table_owner'` サブスクライバーテーブルの所有者の名前を指定します。 *sub_table_owner* は **sysname**であり、既定値はありません。  
  
`[ @publisher = ] 'publisher'` パブリッシャーサーバーの名前を指定します。 *publisher* は **sysname**で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャーデータベースの名前を指定します。 *publisher_db* は **sysname**であり、既定値はありません。 NULL の場合は、現在のデータベースが使用されます。  
  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *Publication* は **sysname**,、既定値はありません。  
  
`[ @ins_proc = ] 'ins_proc'` パブリッシャー側での同期トランザクション挿入をサポートするストアドプロシージャの名前を指定します。 *ins_proc* は **sysname**であり、既定値はありません。  
  
`[ @upd_proc = ] 'upd_proc'` パブリッシャーでの同期トランザクション更新をサポートするストアドプロシージャの名前を指定します。 *ins_proc* は **sysname**であり、既定値はありません。  
  
`[ @del_proc = ] 'del_proc'` パブリッシャー側での同期トランザクション削除をサポートするストアドプロシージャの名前を指定します。 *ins_proc* は **sysname**であり、既定値はありません。  
  
`[ @cftproc = ] 'cftproc'` キュー更新を許可するパブリケーションによって使用される自動生成プロシージャの名前を指定します。 *cftproc* は **sysname**,、既定値はありません。 即時更新を許可するパブリケーションの場合、この値は NULL になります。 このパラメーターは、キュー更新 (キュー更新、およびフェールオーバーとしてキュー更新を使用する即時更新) が許可されているパブリケーションに適用されます。  
  
`[ @proc_owner = ] 'proc_owner'` パブリケーションを更新するために自動生成されたすべてのストアドプロシージャ (queued または immediate) が作成された、パブリッシャーのユーザーアカウントを指定します。 *proc_owner* は **sysname** で、既定値はありません。  
  
`[ @identity_col = ] 'identity_col'` パブリッシャーの id 列の名前を指定します。 *identity_col* は **sysname**,、既定値は NULL です。  
  
`[ @ts_col = ] 'timestamp_col'` パブリッシャーの **timestamp** 列の名前を指定します。 *timestamp_col* は **sysname**,、既定値は NULL です。  
  
`[ @filter_clause = ] 'filter_clause'` は、水平フィルターを定義する restriction (WHERE) 句です。 制限句を入力する場合は、WHERE キーワードを省略します。 *filter_clause*は **nvarchar (4000)**,、既定値は NULL です。  
  
`[ @primary_key_bitmap = ] 'primary_key_bitmap'` テーブル内の主キー列のビットマップです。 *primary_key_bitmap* は **varbinary (4000)**,、既定値はありません。  
  
`[ @identity_support = ] identity_support` キュー更新を使用する場合に、id 範囲の自動処理を有効または無効にします。 *identity_support* は **ビット**,、既定値は **0**です。 **0** は、id 範囲がサポートされていないことを示します。 **1** の場合、id 範囲の自動処理が有効になります。  
  
`[ @independent_agent = ] independent_agent` このパブリケーションに対して1つのディストリビューションエージェント (独立したエージェント) があるか、またはパブリケーションデータベースとサブスクリプションデータベースのペアごとに1つのディストリビューションエージェント (共有エージェント) があるかどうかを示します。 この値には、パブリッシャーで定義されているパブリケーションの independent_agent プロパティの値が反映されます。 *independent_agent* はビットで、既定値は **0**です。 **0**の場合、エージェントは共有エージェントです。 **1**の場合、エージェントは独立したエージェントです。  
  
`[ @distributor = ] 'distributor'` ディストリビューターの名前を指定します。 *ディストリビューター* は **sysname**,、既定値はありません。  
  
`[ @pubversion = ] pubversion` パブリッシャーのバージョンを示します。 *pubversion* は **int**,、既定値は1です。 **1** は、パブリッシャーのバージョンが [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 2 以前であることを示します。 **2** は、パブリッシャーが [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service PACK 3 (SP3) 以降であることを意味します。 パブリッシャーのバージョンが SP3 以降の場合は、 *pubversion*を明示的に**2**に設定する必要があり [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_addsynctriggers** は、サブスクリプションの初期化の一部としてディストリビューションエージェントによって使用されます。 このストアドプロシージャは、一般にユーザーによって実行されるのではなく、ユーザーが同期なしのサブスクリプションを手動で設定する必要がある場合に便利です。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addsynctriggers**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_script_synctran_commands &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-script-synctran-commands-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
