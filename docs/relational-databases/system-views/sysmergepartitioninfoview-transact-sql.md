---
description: sysmergepartitioninfoview (Transact-SQL)
title: sysmergepartitioninfoview (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepartitioninfoview
- sysmergepartitioninfoview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfoview view
ms.assetid: 714e2935-1bc7-4901-aea2-64b1bbda03d6
author: stevestein
ms.author: sstein
ms.openlocfilehash: c194b2442762f2ec9373cc730cbc4835bce45983
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446521"
---
# <a name="sysmergepartitioninfoview-transact-sql"></a>sysmergepartitioninfoview (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sysmergepartitioninfoview**ビューでは、テーブルアーティクルのパーティション分割情報が公開されます。 このビューは、パブリッシャーのパブリケーションデータベースとサブスクライバーのサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|アーティクルの名前です。|  
|**type**|**tinyint**|アーティクルの種類を示します。次のいずれかを指定できます。<br /><br /> **0x0a** = テーブル。<br /><br /> **0x20** = プロシージャスキーマのみ。<br /><br /> **0x40** = ビュースキーマのみ、またはインデックス付きビュースキーマのみ。<br /><br /> **0x80** = 関数スキーマのみ。|  
|**objid**|**int**|パブリッシュされたオブジェクトの識別子です。|  
|**sync_objid**|**int**|同期データセットを表すビューのオブジェクト ID。|  
|**view_type**|**tinyint**|ビューの種類。<br /><br /> **0** = ビューではありません。すべてのベースオブジェクトを使用します。<br /><br /> **1** = 永続的なビュー。<br /><br /> **2** = 一時ビュー。|  
|**artid**|**uniqueidentifier**|指定されたアーティクルの一意の識別番号。|  
|**description**|**nvarchar (255)**|記事の簡単な説明。|  
|**pre_creation_command**|**tinyint**|サブスクリプションデータベースでアーティクルが作成されたときに実行する既定のアクションです。<br /><br /> **0** = なし-サブスクライバーにテーブルが既に存在する場合、アクションは実行されません。<br /><br /> **1** = Drop-テーブルを再作成する前に削除します。<br /><br /> **2** = 削除-サブセットフィルターの WHERE 句に基づいて削除を発行します。<br /><br /> **3** = 切り捨て-2 と同じですが、行ではなくページを削除します。 ただし、は WHERE 句を受け取りません。|  
|**pubid**|**uniqueidentifier**|現在のアーティクルが属するパブリケーションの ID。|  
|**ニックネーム**|**int**|アーティクル id のニックネームマッピングです。|  
|**column_tracking**|**int**|は、アーティクルに対して列の追跡が実装されているかどうかを示します。|  
|**status**|**tinyint**|アーティクルの状態。次のいずれかになります。<br /><br /> **1** = 同期されていない-テーブルをパブリッシュする初期処理スクリプトは、次にスナップショットエージェントが実行されるときに実行されます。<br /><br /> **2** = アクティブ-テーブルをパブリッシュする初期処理スクリプトが実行されました。|  
|**conflict_table**|**sysname**|現在のアーティクルに対して競合しているレコードを含むローカルテーブルの名前です。 このテーブルには情報提供のみを目的としています。このテーブルの内容は、カスタム競合解決ルーチンによって変更または削除されるか、管理者によって直接削除される可能性があります。|  
|**creation_script**|**nvarchar (255)**|この記事の作成スクリプト。|  
|**conflict_script**|**nvarchar (255)**|このアーティクルの競合スクリプト。|  
|**article_resolver**|**nvarchar (255)**|このアーティクルの競合回避モジュールです。|  
|**ins_conflict_proc**|**sysname**|競合テーブルへの競合情報の書き込みに使用するプロシージャです。|  
|**insert_proc**|**sysname**|同期中に行を挿入するために使用されるプロシージャです。|  
|**update_proc**|**sysname**|同期時に行の更新に使用するプロシージャです。|  
|**select_proc**|**sysname**|マージ エージェントがロックやアーティクルの列と行の検索に使用する、自動生成ストアド プロシージャの名前です。|  
|**metadata_select_proc**|**sysname**|マージレプリケーションシステムテーブル内のメタデータにアクセスするために使用する、自動的に生成されたストアドプロシージャの名前。|  
|**delete_proc**|**sysname**|同期中に行を削除するために使用されるプロシージャです。|  
|**schema_option**|**binary (8)**|指定されたアーティクルのスキーマ生成オプションのビットマップ。 サポートされている *schema_option* 値の詳細については、「 [transact-sql&#41;&#40;sp_addmergearticle ](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)」を参照してください。|  
|**destination_object**|**sysname**|サブスクライバーで作成されたテーブルの名前です。|  
|**destination_owner**|**sysname**|目的のオブジェクトの所有者名。|  
|**resolver_clsid**|**nvarchar (50)**|カスタム競合回避モジュールの ID。 ビジネスロジックハンドラーの場合、この値は NULL です。|  
|**subset_filterclause**|**nvarchar(1000)**|このアーティクルのフィルター句。|  
|**missing_col_count**|**int**|アーティクルにない、パブリッシュされた列の数です。|  
|**missing_cols**|**varbinary (128)**|アーティクルに含まれていない列を説明するビットマップ。|  
|**excluded_cols**|**varbinary (128)**|アーティクルから除外された列のビットマップ。|  
|**excluded_col_count**|**int**|アーティクルから除外された列の数です。|  
|**欄**|**varbinary (128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary (128)**|アーティクルから削除された列を説明するビットマップ。|  
|**resolver_info**|**nvarchar (255)**|カスタム競合回避モジュールに必要な追加情報の格納。|  
|**view_sel_proc**|**nvarchar (290)**|マージ エージェントが、動的にフィルター選択されたパブリケーションでアーティクルを最初に作成するとき、およびフィルター選択された任意のパブリケーションで変更された行を列挙するときに使用するストアド プロシージャの名前です。|  
|**gen_cur**|**bigint**|アーティクルのベーステーブルに対するローカルな変更の数を生成します。|  
|**vertical_partition**|**int**|列のフィルター選択がテーブル アーティクルで有効かどうかを示します。 **0** は、垂直フィルターがないことを示し、すべての列をパブリッシュします。|  
|**identity_support**|**int**|Id 範囲の自動処理を有効にするかどうかを指定します。 **1** は、id 範囲の処理が有効になっていることを示し、 **0** は id 範囲のサポートがないことを意味します。|  
|**before_image_objid**|**int**|追跡テーブルオブジェクト ID です。 パブリケーションに対してパーティション変更の最適化が有効になっている場合、追跡テーブルには特定のキー列の値が含まれます。|  
|**before_view_objid**|**int**|ビューテーブルのオブジェクト ID。 ビューは、削除または更新される前に、行が特定のサブスクライバーに属しているかどうかを追跡するテーブルにあります。 パブリケーションに対してパーティション変更の最適化が有効になっている場合にのみ適用されます。|  
|**verify_resolver_signature**|**int**|マージレプリケーションで競合回避モジュールを使用する前に、デジタル署名を検証するかどうかを指定します。<br /><br /> **0** = 署名は検証されません。<br /><br /> **1** = 署名は、信頼されたソースからのものかどうかを確認するために検証されます。|  
|**allow_interactive_resolver**|**bit**|アーティクルに対してインタラクティブ競合回避モジュールの使用を有効にするかどうかを指定します。 **1** は、インタラクティブ競合回避モジュールをアーティクルで使用できることを意味します。|  
|**fast_multicol_updateproc**|**bit**|1 つの UPDATE ステートメントで同じ行の複数の列に対して変更を適用するように、マージ エージェントが有効になっているかどうかを示します。<br /><br /> **0** = 変更された列ごとに個別の更新を発行します。<br /><br /> **1** = update ステートメントで発行され、1つのステートメントで複数の列に対して更新が行われるようにします。|  
|**check_permissions**|**int**|マージエージェントがパブリッシャーに変更を適用するときに検証されるテーブルレベル権限のビットマップ。 *check_permissions* には、次のいずれかの値を指定できます。<br /><br /> **0x00** = アクセス許可はチェックされません。<br /><br /> **0x10** = サブスクライバーでの挿入がアップロードされる前に、パブリッシャー側で権限をチェックします。<br /><br /> **0x20** = サブスクライバーで行われた更新をアップロードする前に、パブリッシャー側で権限をチェックします。<br /><br /> **0x40** = サブスクライバーで実行された削除をアップロードする前に、パブリッシャー側で権限をチェックします。|  
|**maxversion_at_cleanup**|**int**|マージ エージェントの次回実行時にクリーンアップされる generation の最大値です。|  
|**processing_order**|**int**|マージパブリケーション内のアーティクルの処理順序を示します。値が **0** の場合は、アーティクルが順序付けられていないことを示し、アーティクルは最低値から最高値の順に処理されます。 2 つのアーティクルの値が同じ場合、それらは同時に処理されます。 詳細については、「[Specify Merge Replication properties](../../relational-databases/replication/merge/specify-merge-replication-properties.md)」 (マージ レプリケーションのプロパティの指定) を参照してください。|  
|**upload_options**|**tinyint**|変更がサブスクライバーで許可されるか、サブスクライバーからアップロードされるかを示します。次の値のいずれかになります。<br /><br /> **0** = サブスクライバーで行われる更新に制限はありません。すべての変更がパブリッシャーにアップロードされます。<br /><br /> **1** = 変更はサブスクライバーで許可されますが、パブリッシャーにはアップロードされません。<br /><br /> **2** = サブスクライバーでの変更は許可されていません。|  
|**published_in_tran_pub**|**bit**|マージパブリケーション内のアーティクルがトランザクションパブリケーションでもパブリッシュされることを示します。<br /><br /> **0** = アーティクルはトランザクションアーティクルでパブリッシュされていません。<br /><br /> **1** = アーティクルはトランザクションアーティクルでもパブリッシュされます。|  
|**ライトウェイト**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**nchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|更新前のテーブルのビューの ID です。|  
|**delete_tracking**|**bit**|削除がレプリケートされるかどうかを示します。<br /><br /> **0** = 削除はレプリケートされません。<br /><br /> **1** = 削除がレプリケートされます。これは、マージレプリケーションの既定の動作です。<br /><br /> *Delete_tracking*の値が**0**の場合、サブスクライバー側で削除された行はパブリッシャー側で手動で削除する必要があり、パブリッシャー側で削除された行はサブスクライバー側で手動で削除する必要があります。<br /><br /> 注: 値が **0** の場合は、非収束になります。|  
|**compensate_for_errors**|**bit**|同期中にエラーが検出されたときに補正アクションが行われるかどうかを示します。<br /><br /> **0** = 補正アクションは無効です。<br /><br /> **1** = サブスクライバーまたはパブリッシャーで適用できない変更は、常に、マージレプリケーションの既定の動作である変更を元に戻す補正アクションにつながります。<br /><br /> 注: 値が **0** の場合は、非収束になります。|  
|**pub_range**|**bigint**|パブリッシャーの id 範囲のサイズ。|  
|**range**|**bigint**|調整でサブスクライバーに割り当てられる連続する id 値のサイズ。|  
|**threshold**|**int**|Id 範囲のしきい値の割合。|  
|**stream_blob_columns**|**bit**|バイナリ ラージ オブジェクトの列にストリームの最適化を使用するかどうかを示します。 **1** は、最適化が試行されることを意味します。|  
|**preserve_rowguidcol**|**bit**|レプリケーションが既存の rowguid 列を使用するかどうかを示します。 値 **1** は、既存の ROWGUIDCOL 列が使用されることを意味します。 **0** は、レプリケーションによって ROWGUIDCOL 列が追加されたことを示します。|  
|**partition_view_id**|**int**|サブスクライバーパーティションを定義するビューを識別します。|  
|**repl_view_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**partition_deleted_view_rule**|**sysname**|マージレプリケーショントリガー内で使用されるステートメントは、古い列値に基づいて削除または更新された各行のパーティション ID を取得します。|  
|**partition_inserted_view_rule**|**Sysname**|マージ レプリケーション トリガー内で、列の新しい値に基づいて挿入または更新された各行のパーティション ID を取得するために使用されるステートメントです。|  
|**membership_eval_proc_name**|**sysname**|[Transact-sql&#41;&#40;MSmerge_contents](../../relational-databases/system-tables/msmerge-contents-transact-sql.md)内の行の現在のパーティション id を評価するプロシージャの名前。|  
|**column_list**|**sysname**|アーティクルでパブリッシュされた列のコンマ区切りの一覧です。|  
|**column_list_blob**|**sysname**|バイナリラージオブジェクトの列を含む、アーティクルでパブリッシュされた列のコンマ区切りのリスト。|  
|**expand_proc**|**sysname**|新しく挿入された親行のすべての子行と、パーティションの変更または削除された親行のパーティション Id を再評価するプロシージャの名前。|  
|**logical_record_parent_nickname**|**int**|論理レコード内の特定のアーティクルの最上位レベルの親のニックネーム。|  
|**logical_record_view**|**int**|それぞれの子の rowguid に対応する、トップレベルにある親アーティクルの rowguid を出力するビューです。|  
|**logical_record_deleted_view_rule**|**sysname**|**Logical_record_view**に似ていますが、update トリガーと delete トリガーの "deleted" テーブルに子行が表示される点が異なります。|  
|**logical_record_level_conflict_detection**|**bit**|競合を、論理レコード レベルと、行または列レベルのどちらで検出するかを示します。<br /><br /> **0** = 行レベルまたは列レベルの競合検出が使用されます。<br /><br /> **1** = 論理レコードの競合検出が使用されます。この場合、パブリッシャーでの行の変更と、サブスクライバーでの同じ論理レコードの変更は競合として処理されます。<br /><br /> この値が 1 の場合には、論理レコード レベルでの競合解決だけを使用できます。|  
|**logical_record_level_conflict_resolution**|**bit**|競合を論理レコードレベルまたは行レベルまたは列レベルで解決する必要があるかどうかを示します。<br /><br /> **0** = 行または列レベルの解決が使用されます。<br /><br /> **1** = 競合が発生した場合、勝者からの論理レコード全体が、損失側の論理レコード全体を上書きします。<br /><br /> 値 1 は、論理レコード レベルでの検出でも、行または列レベルの検出でも使用することができます。|  
|**partition_options**|**tinyint**|アーティクル内のデータをパーティション分割する方法を定義します。これにより、すべての行が1つのパーティションまたは1つのサブスクリプションのみに属している場合に、パフォーマンスを最適化できます。 *Partition_options*には、次のいずれかの値を指定できます。<br /><br /> **0** = アーティクルのフィルター選択は静的であるか、またはパーティションごとに一意のデータのサブセットではありません ("重複する" パーティション)。<br /><br /> **1** = パーティションは重複しており、サブスクライバーで行われた DML の更新では、行が属するパーティションを変更することはできません。<br /><br /> **2** = アーティクルのフィルター選択によって重複しないパーティションが生成されますが、複数のサブスクライバーが同じパーティションを受け取ることができます。<br /><br /> **3** = アーティクルのフィルター選択により、各サブスクリプションで一意な重複しないパーティションが生成されます。|  
|**name**|**sysname**|パーティションの名前。|  
  
## <a name="see-also"></a>関連項目  
 [パラメーター化されたフィルターを使用してマージパブリケーションのパーティションを管理する](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepartition &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_helpmergepartition &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)  
  
  
