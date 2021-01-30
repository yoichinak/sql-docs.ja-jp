---
description: sp_mergearticlecolumn (Transact-SQL)
title: sp_mergearticlecolumn (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_mergearticlecolumn
- sp_mergearticlecolumn_TSQL
helpviewer_keywords:
- sp_mergearticlecolumn
ms.assetid: b4f2b888-e094-4759-a472-d893638995eb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b5d8d2f63afd421081058dd1b53ec8084f4b5e13
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99185312"
---
# <a name="sp_mergearticlecolumn-transact-sql"></a>sp_mergearticlecolumn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージパブリケーションを垂直方向にパーティション分割します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_mergearticlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column'  
    [ , [ @operation = ] 'operation'   
    [ , [ @schema_replication = ] 'schema_replication' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *Publication* は **sysname**,、既定値はありません。  
  
`[ @article = ] 'article'` パブリケーション内のアーティクルの名前を指定します。 *アーティクル* は **sysname** で、既定値はありません。  
  
`[ @column = ] 'column'` 列分割を作成する列を指定します。 *列* は **sysname**,、既定値は NULL です。 値が NULL で `@operation = N'add'` の場合、既定ではソース テーブルのすべての列がアーティクルに追加されます。 *操作* が **drop** に設定されている場合、*列* を NULL にすることはできません。 アーティクルから列を除外するには、 **sp_mergearticlecolumn** を実行し、  `@operation = N'drop'` 指定された *アーティクル* から削除される各列に対して列およびを指定します。  
  
`[ @operation = ] 'operation'` レプリケーションの状態を示します。 *操作* は **nvarchar (4)**,、既定値は ADD です。 **add** は、レプリケーションの列にマークを付けます。 **drop** 列をクリアします。  
  
`[ @schema_replication = ] 'schema_replication'` マージエージェントの実行時にスキーマ変更が反映されることを指定します。 *schema_replication* は **nvarchar (5)**,、既定値は FALSE です。  
  
> [!NOTE]  
>  *Schema_replication* では、 **FALSE** のみがサポートされています。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` スナップショットを無効にする機能を有効または無効にします。 *force_invalidate_snapshot* は **ビット**,、既定値は **0** です。  
  
 **0** を指定すると、マージアーティクルへの変更によってスナップショットが無効になることはありません。  
  
 **1** に設定すると、マージアーティクルへの変更によってスナップショットが無効になる可能性があります。この場合、値 **1** を指定すると、新しいスナップショットを作成する権限が与えられます。  
  
`[ @force_reinit_subscription = ]force_reinit_subscription_` サブスクリプションを再初期化する機能を有効または無効にします。 *force_reinit_subscription* はビットで、既定値は **0** です。  
  
 **0** を指定すると、マージアーティクルへの変更によってサブスクリプションが再初期化されることはありません。  
  
 **1** に設定すると、マージアーティクルへの変更によってサブスクリプションが再初期化されることがあります。この場合、値 **1** を指定すると、サブスクリプションの再初期化が許可されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_mergearticlecolumn** は、マージレプリケーションで使用します。  
  
 自動 ID 範囲管理が使用されている場合、アーティクルから ID 列を削除することはできません。 詳細については、「[Replicate Identity Columns](../../relational-databases/replication/publish/replicate-identity-columns.md)」 (ID 列のレプリケート) を参照してください。  
  
 初期スナップショットの作成後にアプリケーションが新しい列方向のパーティションを設定する場合は、新しいスナップショットを生成し、各サブスクリプションに再適用する必要があります。 スナップショットは、次回スケジュールされているスナップショット エージェントおよびディストリビューション エージェント、またはマージ エージェントが実行されるときに適用されます。  
  
 行レベルの追跡を使用して競合を検出する場合 (既定値)、ベース テーブルには最大 1,024 列含めることができますが、最大 246 列がパブリッシュされるようにアーティクルから列をフィルター選択する必要があります。 列の追跡を使用する場合、ベース テーブルには最大 246 列を含めることができます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-mergearticlecolumn-tr_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_mergearticlecolumn** を実行できるのは、固定サーバーロール **sysadmin** または固定データベースロール **db_owner** のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [マージ アーティクル間の結合フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [マージ アーティクルのパラメーター化された行フィルターの定義および変更](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [パブリッシュされたデータのフィルター処理](../../relational-databases/replication/publish/filter-published-data.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
