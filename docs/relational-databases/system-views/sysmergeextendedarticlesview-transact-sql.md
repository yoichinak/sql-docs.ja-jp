---
description: sysmergeextendedarticlesview (Transact-SQL)
title: sysmergeextendedarticlesview (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergeextendedarticlesview
- sysmergeextendedarticlesview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeextendedarticlesview view
ms.assetid: bd5c8414-5292-41fd-80aa-b55a50ced7e2
author: stevestein
ms.author: sstein
ms.openlocfilehash: f5f400a8e08d242427ca5101461ccb9dacd58310
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485455"
---
# <a name="sysmergeextendedarticlesview-transact-sql"></a>sysmergeextendedarticlesview (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sysmergeextendedarticlesview**ビューは、アーティクル情報を公開します。 このビューは、パブリッシャーのパブリケーションデータベースとサブスクライバーのサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|アーティクルの名前です。|  
|**type**|**tinyint**|アーティクルの種類を示します。次のいずれかを指定できます。<br /><br /> **10** = テーブル。<br /><br /> **32** = Proc スキーマのみ。<br /><br /> **64** = ビュースキーマのみ、またはインデックス付きビュースキーマのみ。<br /><br /> **128** = 関数スキーマのみ。<br /><br /> **160** = シノニムスキーマのみ。|  
|**objid**|**int**|パブリッシャー オブジェクトの識別子。|  
|**sync_objid**|**int**|同期されたデータセットを表すビューの識別子。|  
|**view_type**|**tinyint**|ビューの種類。<br /><br /> **0** = ビューではありません。すべてのベースオブジェクトを使用します。<br /><br /> **1** = 永続的なビュー。<br /><br /> **2** = 一時ビュー。|  
|**artid**|**uniqueidentifier**|指定されたアーティクルの一意の識別番号。|  
|**description**|**nvarchar (255)**|記事の簡単な説明。|  
|**pre_creation_command**|**tinyint**|サブスクリプションデータベースでアーティクルが作成されたときに実行する既定のアクションです。<br /><br /> **0** = なし-サブスクライバーにテーブルが既に存在する場合、アクションは実行されません。<br /><br /> **1** = Drop-テーブルを再作成する前に削除します。<br /><br /> **2** = 削除-サブセットフィルターの WHERE 句に基づいて削除を発行します。<br /><br /> **3** = 切り捨て-2 と同じですが、行ではなくページを削除します。 ただし、は WHERE 句を受け取りません。|  
|**pubid**|**uniqueidentifier**|現在のアーティクルが属するパブリケーションの ID。|  
|**ニックネーム**|**int**|アーティクル id のニックネームマッピングです。|  
|**column_tracking**|**int**|アーティクルに対して列の追跡が実装されているかどうかを示します。|  
|**status**|**tinyint**|アーティクルの状態。次のいずれかになります。<br /><br /> **1** = 同期されていない-テーブルをパブリッシュする初期処理スクリプトは、次にスナップショットエージェントが実行されるときに実行されます。<br /><br /> **2** = アクティブ-テーブルをパブリッシュする初期処理スクリプトが実行されました。<br /><br /> **5** = New_inactive 追加されます。<br /><br /> **6** = New_active 追加されます。|  
|**conflict_table**|**sysname**|現在のアーティクルに対して競合しているレコードを含むローカルテーブルの名前です。 このテーブルには情報提供のみを目的としています。このテーブルの内容は、カスタム競合解決ルーチンによって変更または削除されるか、管理者によって直接削除される可能性があります。|  
|**creation_script**|**nvarchar (255)**|この記事の作成スクリプト。|  
|**conflict_script**|**nvarchar (255)**|このアーティクルの競合スクリプト。|  
|**article_resolver**|**nvarchar (255)**|アーティクルのカスタム行レベル競合回避モジュール。|  
|**ins_conflict_proc**|**sysname**|**Conflict_table**との競合を書き込むために使用されるプロシージャです。|  
|**insert_proc**|**sysname**|同期化の際に行を挿入するため、既定の競合回避モジュールが使用するプロシージャ。|  
|**update_proc**|**sysname**|同期中に行を更新するために、既定の競合回避モジュールによって使用されるプロシージャです。|  
|**select_proc**|**sysname**|マージエージェントがロックを実行し、アーティクルの列と行を検索するために使用する、自動的に生成されたストアドプロシージャの名前。|  
|**schema_option**|**binary (8)**|サポートされている *schema_option*の値については、「 [transact-sql&#41;&#40;sp_addmergearticle ](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)」を参照してください。|  
|**destination_object**|**sysname**|サブスクライバーで作成されたテーブルの名前です。|  
|**resolver_clsid**|**nvarchar (50)**|カスタム競合回避モジュールの ID。|  
|**subset_filterclause**|**nvarchar(1000)**|このアーティクルのフィルター句。|  
|**missing_col_count**|**int**|欠落している列の数。|  
|**missing_cols**|**varbinary (128)**|欠落している列のビットマップ。|  
|**欄**|**varbinary (128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resolver_info**|**nvarchar (255)**|カスタム競合回避モジュールに必要な追加情報の格納。|  
|**view_sel_proc**|**nvarchar (290)**|動的にフィルター選択されたパブリケーションでアーティクルを最初に作成するとき、およびフィルター選択されたパブリケーションの変更された行を列挙するためにマージエージェントが使用するストアドプロシージャの名前。|  
|**gen_cur**|**int**|アーティクルのベーステーブルに対するローカルの変更の生成番号。|  
|**excluded_cols**|**varbinary (128)**|アーティクルがサブスクライバーに送信されるときに、アーティクルから除外される列のビットマップ。|  
|**excluded_col_count**|**int**|除外する列の数。|  
|**vertical_partition**|**int**|列のフィルター選択がテーブル アーティクルで有効かどうかを示します。 **0** は、垂直フィルターがないことを示し、すべての列をパブリッシュします。|  
|**identity_support**|**int**|Id 範囲の自動処理を有効にするかどうかを指定します。 **1** は、id 範囲の処理が有効になっていることを示し、 **0** は id 範囲のサポートがないことを意味します。|  
|**destination_owner**|**sysname**|目的のオブジェクトの所有者名。|  
|**before_image_objid**|**int**|追跡テーブルオブジェクト ID です。 パブリケーションがパーティション変更の最適化を有効にするように構成されている場合、追跡テーブルには特定のキー列の値が含まれます。|  
|**before_view_objid**|**int**|ビューテーブルのオブジェクト ID。 ビューは、削除または更新される前に、行が特定のサブスクライバーに属しているかどうかを追跡するテーブルにあります。 * \@ Keep_partition_changes*true を使用してパブリケーションが作成された場合にのみ適用され  =  **true**ます。|  
|**verify_resolver_signature**|**int**|マージレプリケーションで競合回避モジュールを使用する前に、デジタル署名を検証するかどうかを指定します。<br /><br /> **0** = 署名は検証されません。<br /><br /> **1** = 署名は、信頼されたソースからのものかどうかを確認するために検証されます。|  
|**allow_interactive_resolver**|**bit**|アーティクルに対してインタラクティブ競合回避モジュールの使用を有効にするかどうかを指定します。 **1** は、インタラクティブ競合回避モジュールがアーティクルで使用されることを示します。|  
|**fast_multicol_updateproc**|**bit**|1 つの UPDATE ステートメントで同じ行の複数の列に対して変更を適用するように、マージ エージェントが有効になっているかどうかを示します。<br /><br /> **0** = 変更された列ごとに個別の更新を発行します。<br /><br /> **1** = update ステートメントで発行され、1つのステートメントで複数の列に対して更新が行われるようにします。|  
|**check_permissions**|**int**|マージエージェントがパブリッシャーに変更を適用するときに検証されるテーブルレベル権限のビットマップ。 *check_permissions* には、次のいずれかの値を指定できます。<br /><br /> **0x00** = アクセス許可はチェックされません。<br /><br /> **0x10** = サブスクライバーでの挿入をアップロードする前に、パブリッシャー側で権限をチェックします。<br /><br /> **0x20** = サブスクライバーで行われた更新をアップロードする前に、パブリッシャー側で権限をチェックします。<br /><br /> **0x40** = サブスクライバーで実行された削除をアップロードする前に、パブリッシャー側で権限をチェックします。|  
|**maxversion_at_cleanup**|**int**|メタデータがクリーンアップされる最大のジェネレーション。|  
|**processing_order**|**int**|マージパブリケーション内のアーティクルの処理順序を示します。値が **0** の場合は、アーティクルが順序付けられていないことを示し、アーティクルは最低値から最高値の順に処理されます。 2 つのアーティクルの値が同じ場合、それらは同時に処理されます。 詳細については、「[Specify Merge Replication properties](../../relational-databases/replication/merge/specify-merge-replication-properties.md)」 (マージ レプリケーションのプロパティの指定) を参照してください。|  
|**published_in_tran_pub**|**bit**|マージパブリケーション内のアーティクルがトランザクションパブリケーションでもパブリッシュされることを示します。<br /><br /> **0** = アーティクルはトランザクションアーティクルでパブリッシュされていません。<br /><br /> **1** = アーティクルはトランザクションアーティクルでもパブリッシュされます。|  
|**upload_options**|**tinyiny**|変更がサブスクライバーで許可されるか、サブスクライバーからアップロードされるかを示します。次の値のいずれかになります。<br /><br /> **0** = サブスクライバーで行われる更新に制限はありません。すべての変更がパブリッシャーにアップロードされます。<br /><br /> **1** = 変更はサブスクライバーで許可されますが、パブリッシャーにはアップロードされません。<br /><br /> **2** = サブスクライバーでの変更は許可されていません。|  
|**ライトウェイト**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**delete_proc**|**sysname**|同期中に行を削除するために、既定の競合回避モジュールによって使用されるプロシージャです。|  
|**before_upd_view_objid**|**int**|更新前のテーブルのビューの ID。|  
|**delete_tracking**|**bit**|削除がレプリケートされるかどうかを示します。<br /><br /> **0** = 削除はレプリケートされません。<br /><br /> **1** = 削除がレプリケートされます。これは、マージレプリケーションの既定の動作です。<br /><br /> *Delete_tracking*の値が**0**の場合、サブスクライバー側で削除された行はパブリッシャー側で手動で削除する必要があり、パブリッシャー側で削除された行はサブスクライバー側で手動で削除する必要があります。<br /><br /> 注: 値が **0** の場合は、非収束になります。|  
|**compensate_for_errors**|**bit**|同期中にエラーが検出されたときに補正アクションが行われるかどうかを示します。<br /><br /> **0** = 補正アクションは無効です。<br /><br /> **1** = サブスクライバーまたはパブリッシャーで適用できない変更は、常に、マージレプリケーションの既定の動作である変更を元に戻す補正アクションにつながります。<br /><br /> 注: 値が **0** の場合は、非収束になります。|  
|**pub_range**|**bigint**|パブリッシャーの id 範囲のサイズ。|  
|**range**|**bigint**|調整でサブスクライバーに割り当てられる連続する id 値のサイズ。|  
|**threshold**|**int**|Id 範囲のしきい値の割合。|  
|**metadata_select_proc**|**sysname**|マージレプリケーションシステムテーブル内のメタデータにアクセスするために使用する、自動的に生成されたストアドプロシージャの名前。|  
|**stream_blob_columns**|**bit**|バイナリ ラージ オブジェクトの列をレプリケートするときに、データ ストリーム最適化が使用されるかどうかを示します。 **1** は、最適化が試行されることを意味します。|  
|**preserve_rowguidcol**|**bit**|レプリケーションが既存の rowguid 列を使用するかどうかを示します。 値 **1** は、既存の ROWGUIDCOL 列が使用されることを意味します。 **0** は、レプリケーションによって ROWGUIDCOL 列が追加されたことを示します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [sysmergearticles &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)  
  
  
