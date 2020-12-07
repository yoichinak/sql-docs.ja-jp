---
description: sp_helpmergearticle (Transact-sql)
title: sp_helpmergearticle (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticle
- sp_helpmergearticle_TSQL
helpviewer_keywords:
- sp_helpmergearticle
ms.assetid: 0fb9986a-3c33-46ef-87bb-297396ea5a6a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 04e67d82b6c567a5c94de8009635c31e41864b92
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535214"
---
# <a name="sp_helpmergearticle-transact-sql"></a>sp_helpmergearticle (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  アーティクルに関する情報を返します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されるか、サブスクリプションデータベースの再パブリッシュサブスクライバーで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergearticle [ [ @publication = ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` 情報を取得するパブリケーションの名前を指定します。 *publication*のデータ型は **sysname**で、既定値はです **%** 。これにより、現在のデータベースのすべてのパブリケーションに含まれるすべてのマージアーティクルに関する情報が返されます。  
  
`[ @article = ] 'article'` 情報を返すアーティクルの名前を指定します。 *アーティクル*のデータ型は **sysname**で、既定値はです **%** 。これにより、指定されたパブリケーションのすべてのマージアーティクルに関する情報が返されます。  
  
## <a name="result-set"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|アーティクルの識別子。|  
|**name**|**sysname**|アーティクルの名前。|  
|**source_owner**|**sysname**|ソースオブジェクトの所有者の名前。|  
|**source_object**|**sysname**|追加するアーティクルのソース オブジェクトの名前。|  
|**sync_object_owner**|**sysname**|パブリッシュされたアーティクルを定義するビューの所有者の名前。|  
|**sync_object**|**sysname**|パーティションの初期データを確立するために使用されるカスタムオブジェクトの名前。|  
|**description**|**nvarchar (255)**|アーティクルの説明です。|  
|**status**|**tinyint**|アーティクルの状態。次のいずれかの値になります。<br /><br /> **1** = 非アクティブ<br /><br /> **2** = アクティブ<br /><br /> **5** = データ定義言語 (DDL) 操作の保留中<br /><br /> **6** = 新しく生成されたスナップショットを使用する DDL 操作<br /><br /> 注: アーティクルが再初期化されると、 **5** と **6** の値が **2**に変更されます。|  
|**creation_script**|**nvarchar (255)**|サブスクリプションデータベースでアーティクルを作成するために使用される、オプションのアーティクルスキーマスクリプトのパスと名前です。|  
|**conflict_table**|**nvarchar (270)**|挿入または更新の競合を格納するテーブルの名前。|  
|**article_resolver**|**nvarchar (255)**|アーティクルのカスタム競合回避モジュール。|  
|**subset_filterclause**|**nvarchar(1000)**|行方向のフィルター選択を指定する WHERE 句。|  
|**pre_creation_command**|**tinyint**|作成前の方法。次のいずれかになります。<br /><br /> **0** = なし<br /><br /> **1** = drop<br /><br /> **2** = 削除<br /><br /> **3** = 切り捨て|  
|**schema_option**|**binary (8)**|アーティクルのスキーマ生成オプションのビットマップ。 このビットマップオプションの詳細については、「 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 」または「 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)」を参照してください。|  
|**type**|**smallint**|アーティクルの種類。次のいずれかの値になります。<br /><br /> **10** = テーブル<br /><br /> **32** = ストアドプロシージャ<br /><br /> **64** = ビューまたはインデックス付きビュー<br /><br /> **128** = ユーザー定義関数<br /><br /> **160** = シノニムスキーマのみ|  
|**column_tracking**|**int**|設定 (列レベルの追跡の) **1** は列レベルの追跡が on であることを示し、 **0** は列レベルの追跡がオフであることを示します。|  
|**resolver_info**|**nvarchar (255)**|アーティクルの競合回避モジュールの名前。|  
|**vertical_partition**|**bit**|アーティクルが列方向にパーティション分割されている場合は、 **1** は、アーティクルが垂直方向にパーティション分割されていることを示します。 **0** は、アーティクルがパーティション分割されていないことを示します。|  
|**destination_owner**|**sysname**|対象オブジェクトの所有者。 ストアド プロシージャ、ビュー、およびユーザー定義関数 (UDF) スキーマ アーティクルをマージするときのみ適用されます。|  
|**identity_support**|**int**|自動 id 範囲の処理が有効になっている場合は。 **1** は有効で、 **0** は無効になっています。|  
|**pub_identity_range**|**bigint**|新しい id 値を割り当てるときに使用する範囲のサイズ。 詳細については、「 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)」の「マージレプリケーション」セクションを参照してください。|  
|**identity_range**|**bigint**|新しい id 値を割り当てるときに使用する範囲のサイズ。 詳細については、「 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)」の「マージレプリケーション」セクションを参照してください。|  
|**threshold**|**int**|[!INCLUDE[ssEW](../../includes/ssew-md.md)]または以前のバージョンのを実行しているサブスクライバーで使用されるパーセンテージ値 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 **しきい値** は、マージエージェントが新しい id 範囲を割り当てるタイミングを制御します。 [しきい値] で指定した値のパーセンテージが使用されると、マージエージェントによって新しい id 範囲が作成されます。 詳細については、「 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)」の「マージレプリケーション」セクションを参照してください。|  
|**verify_resolver_signature**|**int**|マージレプリケーションで競合回避モジュールを使用する前にデジタル署名を検証する場合は、 **0** は、署名が検証されないことを示します。 **1** は、署名が信頼できるソースからのものかどうかを確認することを意味します。|  
|**destination_object**|**sysname**|対象オブジェクトの名前。 ストアド プロシージャ、ビュー、および UDF スキーマ アーティクルをマージするときのみ適用されます。|  
|**allow_interactive_resolver**|**int**|インタラクティブ競合回避モジュールが記事で使用されている場合 **1** は、このリゾルバーが使用されることを示し、 **0** は使用されないことを示します。|  
|**fast_multicol_updateproc**|**int**|1つの UPDATE ステートメントで同じ行の複数の列に変更を適用するためのマージエージェントを有効または無効にします。 **1** は1つのステートメントで複数の列が更新されることを示し、 **0** の場合は更新された各列に対して個別の UPDATE ステートメントが発生します。|  
|**check_permissions**|**int**|検証されるテーブルレベルの権限のビットマップを表す整数値。 使用可能な値の一覧については、「 [sp_addmergearticle &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)」を参照してください。|  
|**processing_order**|**int**|パブリケーションのアーティクルにデータ変更が適用される順序。|  
|**upload_options**|**tinyint**|クライアントサブスクリプションを使用して、サブスクライバーで行われる更新に対する制限を定義します。次のいずれかの値を指定できます。<br /><br /> **0** = クライアントサブスクリプションを使用してサブスクライバーで行われる更新に制限はありません。すべての変更がパブリッシャーにアップロードされます。<br /><br /> **1** = クライアントサブスクリプションを使用するサブスクライバーでの変更は許可されますが、パブリッシャーにはアップロードされません。<br /><br /> **2** = クライアントサブスクリプションを使用するサブスクライバーでは、変更は許可されません。<br /><br /> 詳細については、「[ダウンロード専用アーティクルを使用したマージ レプリケーションのパフォーマンス最適化](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)」を参照してください。|  
|**identityrangemanagementoption**|**int**|自動 id 範囲の処理が有効になっている場合は。 **1** は有効で、 **0** は無効になっています。|  
|**delete_tracking**|**bit**|削除をレプリケートする場合は、 **1** は、削除がレプリケートされることを示し、 **0** はその削除が行われないことを示します。|  
|**compensate_for_errors**|**bit**|同期中にエラーが発生した場合に補正アクションを実行するかどうかを示します。 **1** は補正アクションが実行されることを示し、 **0** は補正アクションが実行されないことを示します。|  
|**partition_options**|**tinyint**|アーティクル内のデータをパーティション分割する方法を定義します。これにより、すべての行が1つのパーティションまたは1つのサブスクリプションのみに属している場合に、パフォーマンスを最適化できます。 *partition_options* 、次のいずれかの値を指定できます。<br /><br /> **0** = アーティクルのフィルター選択は静的であるか、パーティションごとに一意のデータのサブセットを生成しません。つまり、"重なっている" パーティションです。<br /><br /> **1** = パーティションは重複しており、サブスクライバーで行われたデータ操作言語 (DML) の更新では、行が属するパーティションを変更することはできません。<br /><br /> **2** = アーティクルのフィルター選択によって重複しないパーティションが生成されますが、複数のサブスクライバーが同じパーティションを受け取ることができます。<br /><br /> **3** = アーティクルのフィルター選択により、各サブスクリプションで一意な重複しないパーティションが生成されます。|  
|**artid**|**uniqueidentifier**|アーティクルを一意に識別する識別子。|  
|**pubid**|**uniqueidentifier**|アーティクルがパブリッシュされるパブリケーションを一意に識別する識別子。|  
|**stream_blob_columns**|**bit**|バイナリラージオブジェクトの列をレプリケートするときに、データストリームの最適化が使用されているかどうかを示します。 **1** は最適化が使用されていることを示し、 **0** は最適化が使用されていないことを示します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_helpmergearticle** は、マージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpmergearticle**を実行できるのは、パブリケーションデータベースの固定データベースロール**db_owner** 、ディストリビューションデータベースの**replmonitor**ロール、またはパブリケーションのパブリケーションアクセスリストのメンバーだけです。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_helpmergearticle](../../relational-databases/replication/codesnippet/tsql/sp-helpmergearticle-tran_1.sql)]  
  
## <a name="see-also"></a>参照  
 [アーティクルのプロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
