---
description: sysmergepublications (Transact-sql)
title: sysmergepublications (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepublications
- sysmergepublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepublications system table
ms.assetid: 7f82c6c3-22d1-47c0-a92b-4d64b98cc455
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4f079b7ea36d55f978db4c802efb3c8c4283eab3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540231"
---
# <a name="sysmergepublications-transact-sql"></a>sysmergepublications (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベースで定義されているマージパブリケーションごとに1行のデータを格納します。 このテーブルは、パブリケーションデータベースとサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|既定のサーバーの名前。|  
|**publisher_db**|**sysname**|既定のパブリッシャーデータベースの名前。|  
|**name**|**sysname**|パブリケーションの名前を指定します。|  
|**description**|**nvarchar (255)**|パブリケーションの簡単な説明。|  
|**保有**|**int**|パブリケーションセット全体の保有期間。単位は **retention_period_unit** 列の値によって示されます。|  
|**publication_type**|**tinyint**|パブリケーションがフィルター選択されていることを示します。<br /><br /> **0** = フィルター処理されていません。<br /><br /> **1** = フィルター処理済み。|  
|**pubid**|**uniqueidentifier**|このパブリケーションの一意な識別番号です。 パブリケーションが追加されたときに生成されます。|  
|**designmasterid**|**uniqueidentifier**|将来使用するために予約されています。|  
|**parentid**|**uniqueidentifier**|現在のピアまたはサブセットパブリケーションが作成された親パブリケーションを示します (階層パブリッシュトポロジに使用されます)。|  
|**sync_mode**|**tinyint**|このパブリケーションの同期モードです。<br /><br /> **0** = ネイティブ。<br /><br /> **1** = 文字。|  
|**allow_push**|**int**|パブリケーションがプッシュ サブスクリプションを許可するかどうかを示します。<br /><br /> **0** = プッシュサブスクリプションは許可されません。<br /><br /> **1** = プッシュサブスクリプションは許可されます。|  
|**allow_pull**|**int**|パブリケーションでプルサブスクリプションが許可されているかどうかを示します。<br /><br /> **0** = プルサブスクリプションは許可されていません。<br /><br /> **1** = プルサブスクリプションは許可されています。|  
|**allow_anonymous**|**int**|パブリケーションが匿名サブスクリプションを許可するかどうかを示します。<br /><br /> **0** = 匿名サブスクリプションは許可されません。<br /><br /> **1** = 匿名サブスクリプションは許可されます。|  
|**centralized_conflicts**|**int**|競合レコードがパブリッシャーに格納されているかどうかを示します。<br /><br /> **0** = 競合レコードはパブリッシャーに格納されません。<br /><br /> **1** = 競合レコードはパブリッシャーに格納されます。|  
|**status**|**tinyint**|将来使用するために予約されています。|  
|**snapshot_ready**|**tinyint**|パブリケーションのスナップショットの状態を示します。<br /><br /> **0** = スナップショットは使用する準備ができていません。<br /><br /> **1** = スナップショットは使用する準備ができています。<br /><br /> **2** = このパブリケーションの新しいスナップショットを作成する必要があります。|  
|**enabled_for_internet**|**bit**|FTP やその他のサービスを使用して、パブリケーションの同期ファイルがインターネットに公開されているかどうかを示します。<br /><br /> **0** = 同期ファイルは、インターネットからアクセスできます。<br /><br /> **1** = 同期ファイルにインターネットからアクセスすることはできません。|  
|**dynamic_filters**|**bit**|パラメーター化された行フィルターでパブリケーションがフィルター選択されているかどうかを示します。<br /><br /> **0** = パブリケーションは行フィルター選択されていません。<br /><br /> **1** = パブリケーションは行フィルター選択されています。|  
|**snapshot_in_defaultfolder**|**bit**|スナップショット ファイルが既定のフォルダーに格納されるかどうかを指定します。<br /><br /> **0** = スナップショットファイルは既定のフォルダーにあります。<br /><br /> **1** = スナップショットファイルは、 **alt_snapshot_folder**によって指定された場所に格納されます。|  
|**alt_snapshot_folder**|**nvarchar (255)**|スナップショットの代替フォルダーの場所です。|  
|**pre_snapshot_script**|**nvarchar (255)**|へのポインター。サブスクライバーでスナップショットを適用するときに、レプリケーションオブジェクトのスクリプトの前にマージエージェント実行される**sql** ファイル。|  
|**post_snapshot_script**|**nvarchar (255)**|へのポインター。他のすべてのレプリケーションオブジェクトのスクリプトとデータが初期同期中に適用された後にマージエージェント実行する**sql** ファイルです。|  
|**compress_snapshot**|**bit**|**Alt_snapshot_folder**の場所に書き込まれるスナップショットを CAB 形式で圧縮するかどうかを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] ます。 **0** は、ファイルが圧縮されないことを指定します。|  
|**ftp_address**|**sysname**|ディストリビューターのファイル転送プロトコル (FTP) サービスのネットワークアドレス。 FTP が有効になっている場合に、マージエージェントが取得するパブリケーションスナップショットファイルの場所を指定します。|  
|**ftp_port**|**int**|ディストリビューターの FTP サービスのポート番号。|  
|**ftp_subdirectory**|**nvarchar (255)**|マージエージェントのスナップショットファイルを取得するために使用できるサブディレクトリ。|  
|**ftp_login**|**sysname**|FTP サービスへの接続に使用するユーザー名。|  
|**ftp_password**|**nvarchar (524)**|FTP サービスへの接続に使用するユーザーパスワード。|  
|**conflict_retention**|**int**|競合を保持する保有期間を日数で指定します。 保有期間が経過すると、競合するテーブルから競合する行が削除されます。|  
|**keep_before_values**|**int**|このパブリケーションに対して同期の最適化が行われているかどうかを指定します。<br /><br /> **0** = 同期は最適化されていません。また、すべてのサブスクライバーに送信されるパーティションは、パーティション内のデータが変更されたときに検証されます。<br /><br /> **1** = 同期は最適化されており、変更されたパーティション内の行を持つサブスクライバーだけが影響を受けます。|  
|**allow_subscription_copy**|**bit**|サブスクリプションデータベースをコピーする機能が有効になっているかどうかを指定します。 **0** は、コピーが許可されていないことを意味します。|  
|**allow_synctoalternate**|**bit**|代替同期パートナーがこのパブリッシャーと同期できるようにするかどうかを指定します。 **0** は、同期パートナーが許可されていないことを示します。|  
|**validate_subscriber_info**|**nvarchar (500)**|サブスクライバー情報を取得し、パラメーター化された行フィルター条件をサブスクライバーで検証するために使用される関数の一覧を示します。|  
|**ad_guidname**|**sysname**|パブリケーションが Active Directory でパブリッシュされるかどうかを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] ます。 有効な GUID は、パブリケーションが Active Directory にパブリッシュされることを指定します。 GUID は、対応する Active Directory パブリケーションオブジェクトの **objectGUID**です。 NULL の場合、パブリケーションは Active Directory でパブリッシュされません。|  
|**backward_comp_level**|**int**|データベースの互換性レベル。 次の値のいずれかです。<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。<br /><br /> **100**  =  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 。|  
|**max_concurrent_merge**|**int**|同時に実行できるマージプロセスの最大数。 このプロパティの値が **0** の場合は、特定の時点で同時に実行されているマージプロセスの数に制限がないことを意味します。 このプロパティは、マージパブリケーションに対して一度に実行できる同時マージプロセスの数に制限を設定します。 同時にスケジュールされているスナップショットプロセスの数が、の値の実行を許可している場合は、余分なジョブがキューに格納され、現在実行中のマージプロセスが終了するまで待機します。|  
|**max_concurrent_dynamic_snapshots**|**int**|マージ パブリケーションに対して実行できるフィルター選択されたデータの同時実行スナップショット セッションの最大数です。 **0**の場合、任意の時点でパブリケーションに対して同時に実行できるフィルター選択されたデータスナップショットセッションの最大数に制限はありません。 このプロパティは、1 つのマージ アプリケーションに対して一度に実行できる同時実行スナップショット処理数の制限値を設定します。 同時にスケジュールされているスナップショットプロセスの数が、の値の実行を許可している場合は、余分なジョブがキューに格納され、現在実行中のマージプロセスが終了するまで待機します。|  
|**use_partition_groups**|**smallint**|パブリケーションで事前計算済みパーティションを使用するかどうかを指定します。|  
|**dynamic_filters_function_list**|**nvarchar (500)**|パブリケーションのパラメーター化された行フィルターで使用される関数の、セミコロンで区切られた一覧です。|  
|**partition_id_eval_proc**|**sysname**|割り当てられているパーティション ID を判断するために、サブスクライバーのマージエージェントによって実行されるプロシージャの名前を指定します。|  
|**publication_number**|**smallint**|**Pubid**への2バイトマッピングを提供する id 列を指定します。 **pubid** はパブリケーションのグローバル一意識別子ですが、パブリケーション番号は、指定されたデータベースでのみ一意です。|  
|**replicate_ddl**|**int**|パブリケーションでスキーマレプリケーションがサポートされているかどうかを示します。<br /><br /> **0** = DDL ステートメントはレプリケートされません。<br /><br /> **1** = パブリッシャーで実行される DDL ステートメントはレプリケートされます。<br /><br /> 詳細については、「[パブリケーション データベースでのスキーマの変更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)」を参照してください。|  
|**allow_subscriber_initiated_snapshot**|**bit**|は、パラメーター化されたフィルターを使用して、パブリケーションのスナップショットを生成するプロセスをサブスクライバーが開始できることを示します。 **1** は、サブスクライバーがスナップショットプロセスを開始できることを示します。|  
|**dynamic_snapshot_queue_timeout**|**int**|パラメーター化フィルターを使用するときに、サブスクライバーがスナップショット生成処理の開始までキューで待機する分数を指定します。|  
|**dynamic_snapshot_ready_timeout**|**int**|パラメーター化されたフィルターを使用するときに、サブスクライバーがスナップショット生成処理の完了を待機する時間 (分) を指定します。|  
|**ディストリビューター**|**sysname**|パブリケーションのディストリビューターの名前。|  
|**snapshot_jobid**|**binary(16)**|サブスクライバーによるスナップショット生成処理の開始が可能な場合のスナップショットを生成するエージェント ジョブを示します。|  
|**allow_web_synchronization**|**bit**|パブリケーションで Web 同期が有効になっているかどうかを指定します。 **1** は、パブリケーションに対して web 同期が有効になっていることを示します。|  
|**web_synchronization_url**|**nvarchar (500)**|Web 同期に使用するインターネット URL の既定値を指定します。|  
|**allow_partition_realignment**|**bit**|パブリッシャーでの行の変更がパーティションの変更を伴う場合、削除をサブスクライバーに送信するかどうかを示します。<br /><br /> **0** = 古いパーティションのデータはサブスクライバーに残されますが、パブリッシャーでこのデータに加えられた変更はこのサブスクライバーにレプリケートされませんが、サブスクライバーで行われた変更はパブリッシャーにレプリケートされます。<br /><br /> **1** = サブスクライバーのパーティションの一部ではないデータを削除することによって、パーティション変更の結果を反映するために、サブスクライバーを削除します。<br /><br /> 詳細については、「 [sp_addmergepublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)」を参照してください。<br /><br /> 注: この値が **0** のときにサブスクライバーに残っているデータは、読み取り専用であるかのように処理する必要があります。ただし、これはレプリケーションシステムによって厳密に適用されるわけではありません。|  
|**retention_period_unit**|**tinyint**|*保有期間*を定義するときに使用する単位を定義します。次のいずれかの値を指定できます。<br /><br /> **0** = 日。<br /><br /> **1** = 週。<br /><br /> **2** = 月。<br /><br /> **3** = 年。|  
|**decentralized_conflicts**|**int**|競合の原因となったサブスクライバーで競合レコードを保存するかどうかを示します。<br /><br /> **0** = 競合レコードはサブスクライバーに保存されません。<br /><br /> **1** = 競合レコードはサブスクライバーに保存されます。|  
|**generation_leveling_threshold**|**int**|ジェネレーションに含まれる変更の数を指定します。 生成とは、パブリッシャーまたはサブスクライバーに配信される変更のコレクションです。|  
|**automatic_reinitialization_policy**|**bit**|自動再初期化を実行する前に、サブスクライバーから変更をアップロードするかどうかを示します。<br /><br /> **1** = 自動再初期化が行われる前に、サブスクライバーから変更がアップロードされます。<br /><br /> **0** = 自動再初期化の前に変更がアップロードされることはありません。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)  
  
  
