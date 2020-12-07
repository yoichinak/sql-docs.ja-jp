---
description: sp_articlecolumn (Transact-SQL)
title: sp_articlecolumn (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlecolumn
- sp_articlecolumn_TSQL
helpviewer_keywords:
- sp_articlecolumn
ms.assetid: 8abaa8c1-d99e-4788-970f-c4752246c577
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d67cb8b9d25b97756bd1e0f86c5425542a2601d2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548342"
---
# <a name="sp_articlecolumn-transact-sql"></a>sp_articlecolumn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  パブリッシュされたテーブルのデータを垂直方向にフィルター選択するために、アーティクルに含まれる列を指定するために使用します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_articlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column' ]  
    [ , [ @operation = ] 'operation' ]  
    [ , [ @refresh_synctran_procs = ] refresh_synctran_procs ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @change_active = ] change_actve ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @internal = ] 'internal' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` このアーティクルを含むパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @article = ] 'article'` アーティクルの名前を指定します。 *アーティクル* は **sysname**で、既定値はありません。  
  
`[ @column = ] 'column'` 追加または削除する列の名前を指定します。 *列* は **sysname**,、既定値は NULL です。 NULL の場合、すべての列がパブリッシュされます。  
  
`[ @operation = ] 'operation'` アーティクルの列を追加または削除するかどうかを指定します。 *操作* は **nvarchar (5)**,、既定値は add です。 **add** は、レプリケーションの列にマークを付けます。 **drop** は列をマーク解除します。  
  
`[ @refresh_synctran_procs = ] refresh_synctran_procs` レプリケートされた列の数と一致するように、即時更新サブスクリプションをサポートするストアドプロシージャを再生成するかどうかを指定します。 *refresh_synctran_procs* は **ビット**,、既定値は **1**です。 **1**の場合、ストアドプロシージャが再生成されます。  
  
`[ @ignore_distributor = ] ignore_distributor` ディストリビューターに接続せずにこのストアドプロシージャを実行するかどうかを示します。 *ignore_distributor* は **ビット**,、既定値は **0**です。 **0**の場合、データベースでパブリッシングが有効になっている必要があります。アーティクルキャッシュは、アーティクルによってレプリケートされた新しい列を反映するように更新する必要があります。 **1**の場合、パブリッシュされていないデータベースに存在するアーティクルのアーティクル列を削除できます。回復する場合にのみ使用してください。  
  
`[ @change_active = ] change_active` サブスクリプションを持つパブリケーションの列を変更できます。 *change_active* は **int** で、既定値は **0**です。 **0**の場合、列は変更されません。 **1**の場合、サブスクリプションを持つアクティブなアーティクルに対して列の追加や削除を行うことができます。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot* は **ビット**,、既定値は **0**です。  
  
 **0** を指定すると、アーティクルへの変更によってスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1** に設定すると、アーティクルへの変更によってスナップショットが無効になることがあります。また、新しいスナップショットを必要とする既存のサブスクリプションが存在する場合は、既存のスナップショットが古い形式としてマークされ、新しいスナップショットが生成されることを示します。  
  
 [** @force_reinit_subscription =** ] *force_reinit_subscription*  
 このストアドプロシージャによって実行されるアクションで、既存のサブスクリプションの再初期化が必要になる可能性があることを確認します。 *force_reinit_subscription* は **ビット**,、既定値は **0**です。  
  
 **0** に設定すると、アーティクルへの変更によってサブスクリプションが再初期化されることはありません。 変更によってサブスクリプションが再初期化される必要があることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。 **1** に設定すると、アーティクルへの変更によって既存のサブスクリプションが再初期化され、サブスクリプションの再初期化を行う権限が与えられます。  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  *パブリッシャーは* 、パブリッシャーでは使用できません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
`[ @internal = ] 'internal'` 内部でのみ使用します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_articlecolumn** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 **Sp_articlecolumn**を使用してフィルター処理できるのは、サブスクライブされていないアーティクルだけです。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlecolumn-transac_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_articlecolumn**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [列フィルターを定義および変更する](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [パブリッシュされたデータのフィルター処理](../../relational-databases/replication/publish/filter-published-data.md)   
 [sp_addarticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
