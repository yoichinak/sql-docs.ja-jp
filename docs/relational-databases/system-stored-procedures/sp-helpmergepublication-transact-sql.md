---
description: sp_helpmergepublication (Transact-SQL)
title: sp_helpmergepublication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepublication
- sp_helpmergepublication_TSQL
helpviewer_keywords:
- sp_helpmergepublication
ms.assetid: dfe1e1e1-9a65-406a-aced-6385a078e135
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1042543ba82dcbd4bc7376acf6943a838506b6fa
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549602"
---
# <a name="sp_helpmergepublication-transact-sql"></a>sp_helpmergepublication (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージパブリケーションに関する情報を返します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergepublication [ [ @publication = ] 'publication' ]  
    [ , [ @found = ] 'found' OUTPUT ]  
    [ , [ @publication_id = ] 'publication_id' OUTPUT ]  
    [ , [ @reserved = ] 'reserved' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
```  
  
## <a name="arguments"></a>引数  
 [ @publication **=** ] **'**_パブリケーション_**'**  
 パブリケーションの名前を指定します。 *publication*のデータ型は **sysname**で、既定値はです **%** 。これは、現在のデータベースにあるすべてのマージパブリケーションに関する情報を返します。  
  
 [ @found **=** ] **'***found***'** 出力  
 行を返すことを示すフラグ。 *見つかった*は **int** と出力パラメーターで、既定値は NULL です。 **1** は、パブリケーションが見つかったことを示します。 **0** は、パブリケーションが見つからないことを示します。  
  
 [ @publication_id **=** ] **'***publication_id***'** 出力  
 パブリケーション識別番号です。 *publication_id* は **uniqueidentifier** と出力パラメーターで、既定値は NULL です。  
  
 [ @reserved **=** ] **'***予約済み***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]*予約済み*は**nvarchar (20)**,、既定値は NULL です。  
  
 [ @publisher **=** ] **'***パブリッシャー***'**  
 パブリッシャーの名前です。 *publisher* は **sysname**で、既定値は NULL です。  
  
 [ @publisher_db **=** ] **'***publisher_db***'**  
 パブリケーションデータベースの名前です。 *publisher_db* は **sysname**,、既定値は NULL です。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|id|**int**|結果セットリスト内のパブリケーションの順序。|  
|name|**sysname**|パブリケーションの名前。|  
|description|**nvarchar (255)**|パブリケーションの説明です。|  
|status|**tinyint**|パブリケーションデータを使用できるかどうかを示します。|  
|retention|**int**|パブリケーション内のアーティクルの変更に関するメタデータを保存する時間。 この期間の単位は、日、週、月、または年にすることができます。 単位の詳細については、retention_period_unit 列を参照してください。|  
|sync_mode|**tinyint**|パブリケーションの同期モード。<br /><br /> **0** = ネイティブ一括コピープログラム (**bcp** ユーティリティ)<br /><br /> **1** = 文字一括コピー|  
|allow_push|**int**|指定されたパブリケーションに対してプッシュサブスクリプションを作成できるかどうかを決定します。 **0** は、プッシュサブスクリプションが許可されていないことを示します。|  
|allow_pull|**int**|指定されたパブリケーションに対してプルサブスクリプションを作成できるかどうかを決定します。 **0** は、プルサブスクリプションが許可されていないことを示します。|  
|allow_anonymous|**int**|指定されたパブリケーションに対して匿名サブスクリプションを作成できるかどうかを決定します。 **0** は、匿名サブスクリプションが許可されていないことを示します。|  
|centralized_conflicts|**int**|指定されたパブリッシャーに競合レコードを格納するかどうかを決定します。<br /><br /> **0** = 競合レコードは、競合の原因となったパブリッシャーとサブスクライバーの両方に格納されます。<br /><br /> **1** = すべての競合レコードはパブリッシャーに格納されます。|  
|priority|**float (8)**|ループバック サブスクリプションの優先度。|  
|snapshot_ready|**tinyint**|このパブリケーションのスナップショットが使用できる状態にあるかどうかを示します。<br /><br /> **0** = スナップショットは使用する準備ができています。<br /><br /> **1** = スナップショットは使用する準備ができていません。|  
|publication_type|**int**|パブリケーションの種類:<br /><br /> **0** = スナップショット。<br /><br /> **1** = トランザクション。<br /><br /> **2** = Merge。|  
|pubid|**uniqueidentifier**|このパブリケーションの一意識別子です。|  
|snapshot_jobid|**binary(16)**|スナップショット エージェントのジョブ ID。 [Sysjobs](../../relational-databases/system-tables/dbo-sysjobs-transact-sql.md)システムテーブルでスナップショットジョブのエントリを取得するには、この16進値を**uniqueidentifier**に変換する必要があります。|  
|enabled_for_internet|**int**|パブリケーションがインターネットに対して有効になっているかどうかを判断します。 **1**の場合、パブリケーションの同期ファイルはディレクトリに格納され `C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\Ftp` ます。 ユーザーは、ファイル転送プロトコル (FTP) ディレクトリを作成する必要があります。 **0**の場合、パブリケーションはインターネットアクセスに対して有効になっていません。|  
|dynamic_filter|**int**|パラメーター化された行フィルターが使用されていることを示します。 **0** は、パラメーター化された行フィルターを使用しないことを意味します。|  
|has_subscription|**bit**|パブリケーションにサブスクリプションがあるかどうかを示します。 **0** は、このパブリケーションに対するサブスクリプションが現在存在しないことを示します。|  
|snapshot_in_default_folder|**bit**|スナップショットファイルを既定のフォルダーに格納するかどうかを指定します。<br /><br /> **1**の場合、スナップショットファイルは既定のフォルダーにあります。<br /><br /> **0**の場合、スナップショットファイルは**alt_snapshot_folder**によって指定された別の場所に格納されます。 別のサーバー、ネットワークドライブ、またはリムーバブルメディア (CD-ROM やリムーバブルディスクなど) 上に配置できます。 スナップショットファイルを FTP サイトに保存して、後でサブスクライバーが取得できるようにすることもできます。<br /><br /> 注: このパラメーターには true を指定できますが、 **alt_snapshot_folder** パラメーターには位置があります。 この組み合わせでは、スナップショットファイルが既定の場所と代替の場所の両方に格納されることを指定します。|  
|alt_snapshot_folder|**nvarchar (255)**|スナップショットの代替フォルダーの場所を指定します。|  
|pre_snapshot_script|**nvarchar (255)**|サブスクライバーでスナップショットを適用するときに、レプリケートされたオブジェクトスクリプトの前にマージエージェントが実行する **.sql** ファイルへのポインターを指定します。|  
|post_snapshot_script|**nvarchar (255)**|初期同期中に、レプリケートされた他のすべてのオブジェクトスクリプトとデータが適用された後にマージエージェント実行する **.sql** ファイルへのポインターを指定します。|  
|compress_snapshot|**bit**|**Alt_snapshot_folder**の場所に書き込まれるスナップショットを CAB 形式で圧縮することを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] ます。|  
|ftp_address|**sysname**|ディストリビューター用の FTP サービスのネットワーク アドレスです。 マージエージェントが取得するパブリケーションスナップショットファイルの場所を指定します。|  
|ftp_port|**int**|ディストリビューター用の FTP サービスのポート番号です。 **ftp_port** の既定値は **21**です。 マージ エージェントが検索するパブリケーション スナップショット ファイルの場所を示します。|  
|ftp_subdirectory|**nvarchar (255)**|FTP を使用してスナップショットを配信するときに、マージエージェントがスナップショットファイルを取得できる場所を指定します。|  
|ftp_login|**sysname**|FTP サービスへの接続に使用するユーザー名です。|  
|conflict_retention|**int**|競合を保持する保有期間を日数で指定します。 指定の日数が経過すると、競合テーブルから競合行が削除されます。|  
|keep_partition_changes|**int**|このパブリケーションに対して同期の最適化が行われているかどうかを指定します。 **keep_partition_changes** の既定値は **0**です。 値が **0** の場合、同期は最適化されず、パーティション内のデータが変更されると、すべてのサブスクライバーに送信されるパーティションが検証されます。<br /><br /> **1** は同期が最適化され、変更されたパーティション内の行を持つサブスクライバーだけが影響を受けることを示します。<br /><br /> 注: 既定では、マージパブリケーションは事前計算済みパーティションを使用します。これにより、このオプションよりも高いレベルの最適化が提供されます。 詳細については、「パラメーター化された[行フィルター](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md) 」および「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンスの最適化](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)|  
|allow_subscription_copy|**int**|このパブリケーションをサブスクライブするサブスクリプションデータベースをコピーする機能が有効になっているかどうかを指定します。 値 **0** は、コピーが許可されていないことを意味します。|  
|allow_synctoalternate|**int**|代替同期パートナーがこのパブリッシャーと同期できるようにするかどうかを指定します。 値 **0** は、同期パートナーが許可されていないことを意味します。|  
|validate_subscriber_info|**nvarchar (500)**|サブスクライバー情報を取得し、パラメーター化された行フィルター条件をサブスクライバーで検証するために使用される関数の一覧を示します。 は、各マージで情報が一貫してパーティション分割されていることを確認するのに役立ちます。|  
|backward_comp_level|**int**|データベースの互換性レベルは、次のいずれかになります。<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP1<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_activedirectory|**bit**|パブリケーション情報が Active Directory にパブリッシュされるかどうかを指定します。 値が **0** の場合は、Active Directory からパブリケーション情報を取得できないことを意味します。<br /><br /> このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のためにのみサポートされています。 Active Directory にパブリケーション情報を追加できなくなりました。|  
|max_concurrent_merge|**int**|同時マージプロセスの数。 **0**の場合、特定の時点で同時に実行されているマージプロセスの数に制限はありません。|  
|max_concurrent_dynamic_snapshots|**int**|マージパブリケーションに対して実行できる、フィルター選択されたデータスナップショットセッションの最大数。 **0**の場合、任意の時点でパブリケーションに対して同時に実行できるフィルター選択されたデータスナップショットセッションの最大数に制限はありません。|  
|use_partition_groups|**int**|事前計算済みパーティションを使用するかどうかを決定します。 値 **1** は、事前計算済みパーティションが使用されることを意味します。|  
|num_of_articles|**int**|パブリケーション内のアーティクルの数。|  
|replicate_ddl|**int**|パブリッシュされたテーブルに対するスキーマ変更がレプリケートされるかどうかを示します。 値 **1** は、スキーマの変更がレプリケートされることを意味します。|  
|publication_number|**smallint**|このパブリケーションに割り当てられた番号。|  
|allow_subscriber_initiated_snapshot|**bit**|サブスクライバーがフィルター選択されたデータスナップショット生成処理を開始できるかどうかを決定します。 値 **1** は、サブスクライバーがスナップショットプロセスを開始できることを意味します。|  
|allow_web_synchronization|**bit**|パブリケーションが Web 同期に対して有効になっているかどうかを示します。 値 **1** は、Web 同期が有効になっていることを示します。|  
|web_synchronization_url|**nvarchar (500)**|Web 同期に使用されるインターネット URL。|  
|allow_partition_realignment|**bit**|パブリッシャーで行を変更するときに、削除をサブスクライバーに送信するかどうかを決定します。 値 **1** は、削除がサブスクライバーに送信されることを意味します。  詳細については、「 [sp_addmergepublication &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)」を参照してください。|  
|retention_period_unit|**tinyint**|保有期間を定義するときに使用する単位を定義します。 次のいずれかの値を指定できます。<br /><br /> **0** = 日<br /><br /> **1** = 週<br /><br /> **2** = 月<br /><br /> **3** = 年|  
|has_downloadonly_articles|**bit**|パブリケーションに属しているアーティクルがダウンロード専用アーティクルであるかどうかを示します。 値が **1** の場合は、ダウンロード専用の記事があることを示します。|  
|decentralized_conflicts|**int**|競合の原因となったサブスクライバーに競合レコードが格納されているかどうかを示します。 値が **0** の場合は、競合レコードがサブスクライバーに格納されていないことを示します。 値 1 は、競合レコードがサブスクライバーで格納されることを表します。|  
|generation_leveling_threshold|**int**|生成に含まれる変更の数を指定します。 生成とは、パブリッシャーまたはサブスクライバーに配信される変更のコレクションです。|  
|automatic_reinitialization_policy|**bit**|自動再初期化を実行する前に、サブスクライバーから変更をアップロードするかどうかを示します。 値 **1** は、自動再初期化が行われる前に変更がサブスクライバーからアップロードされることを示します。 値 0 は、自動再初期化の前に変更がアップロードされないことを表します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 sp_helpmergepublication は、マージ レプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 パブリケーションのパブリケーション アクセス リストのメンバーは、そのパブリケーションに対して sp_helpmergepublication を実行できます。 パブリケーション データベースの db_owner 固定データベース ロールのメンバーは、sp_helpmergepublication を実行してすべてのパブリケーションに関する情報を取得できます。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_helpmergepublication](../../relational-databases/replication/codesnippet/tsql/sp-helpmergepublication-_1.sql)]  
  
## <a name="see-also"></a>参照  
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
