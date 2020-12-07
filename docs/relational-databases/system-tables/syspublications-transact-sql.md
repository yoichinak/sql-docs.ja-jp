---
description: syspublications (Transact-sql)
title: syspublications (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syspublications
- syspublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspublications system table
ms.assetid: a86eb4f5-1f7b-493e-af55-3d15cf878228
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 20b5615cc4f0b11b05eb69f4233e20f7a7379378
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550977"
---
# <a name="syspublications-transact-sql"></a>syspublications (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベースで定義されているパブリケーションごとに1行のデータを格納します。 このテーブルは、パブリケーションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**description**|**nvarchar (255)**|パブリケーションの説明エントリです。|  
|**name**|**sysname**|パブリケーションに関連付けられている一意の名前です。|  
|**pubid**|**int**|パブリケーションの一意の ID を提供する id 列。|  
|**repl_freq**|**tinyint**|レプリケーションの頻度:<br /><br /> **0** = トランザクションベース。<br /><br /> **1** = テーブルの定期更新。|  
|**status**|**tinyint**|状態:<br /><br /> **0** = 非アクティブ。<br /><br /> **1** = アクティブ。|  
|**sync_method**|**tinyint**|同期方法:<br /><br /> **0** = ネイティブモードの一括コピープログラムユーティリティ (**BCP**)。<br /><br /> **1** = キャラクターモードの BCP。<br /><br /> **3** = 同時実行。ネイティブモードの BCP が使用されますが、スナップショットの実行中にテーブルがロックされることはありません。<br /><br /> **4** = Concurrent_c。キャラクターモードの BCP が使用されますが、スナップショットの実行中にテーブルがロックされることはありません。|  
|**snapshot_jobid**|**binary(16)**|スケジュールされたタスク ID。|  
|**independent_agent**|**bit**|このパブリケーションに対して、スタンドアロンのディストリビューション エージェントがあるかどうかを示します。<br /><br /> **0** = パブリケーションは共有ディストリビューションエージェントを使用し、各パブリッシャーデータベース/サブスクライバーデータベースのペアには1つの共有エージェントがあります。<br /><br /> **1** = このパブリケーションには、スタンドアロンのディストリビューションエージェントがあります。|  
|**immediate_sync**|**bit**|スナップショットエージェントを実行するたびに同期ファイルを作成または再作成するかどうかを示します。 **1** は、エージェントを実行するたびに同期ファイルが作成されることを意味します。|  
|**enabled_for_internet**|**bit**|ファイル転送プロトコル (FTP) およびその他のサービスを介して、パブリケーションの同期ファイルがインターネットに公開されているかどうかを示します。 **1** は、インターネットからアクセスできることを意味します。|  
|**allow_push**|**bit**|パブリケーションでプッシュサブスクリプションが許可されているかどうかを示します。 **1** は、このパブリケーションが許可されていることを示します。|  
|**allow_pull**|**bit**|パブリケーションでプルサブスクリプションが許可されているかどうかを示します。 **1** は、このパブリケーションが許可されていることを示します。|  
|**allow_anonymous**|**bit**|パブリケーションで匿名サブスクリプションが許可されているかどうかを示します。 **1** は、このサブスクリプションが許可されていることを示します。|  
|**immediate_sync_ready**|**bit**|スナップショットがスナップショット エージェントによって生成されたかどうか、および新しいサブスクリプションで使用できるかどうかを示します。 即時更新パブリケーションでのみ意味を持ちます。 **1** は、スナップショットの準備ができていることを示します。|  
|**allow_sync_tran**|**bit**|パブリケーションで即時更新サブスクリプションを許可するかどうかを指定します。 **1** は、即時更新サブスクリプションが許可されることを示します。|  
|**autogen_sync_procs**|**bit**|即時更新サブスクリプションの同期ストアドプロシージャがパブリッシャーで生成されるかどうかを指定します。 **1** は、パブリッシャーで生成されることを意味します。|  
|**保有**|**int**|指定されたパブリケーションに対して保存する変更の量 (時間単位)。|  
|**allowed_queued_tran**|**bit**|変更をパブリッシャーで適用できるようになるまで、サブスクライバーで変更をキューに保持するかどうかを示します。 **1**の場合、サブスクライバーでの変更はキューに登録されます。|  
|**snapshot_in_defaultfolder**|**bit**|スナップショットファイルを既定のフォルダーに格納するかどうかを指定します。<br /><br /> **0** = スナップショットファイルは、 *alternate_snapshot_folder*によって指定された別の場所に格納されています。<br /><br /> **1** = スナップショットファイルは既定のフォルダーにあります。|  
|**alt_snapshot_folder**|**nvarchar (255)**|スナップショットの代替フォルダーの場所を指定します。|  
|**pre_snapshot_script**|**nvarchar (255)**|**.Sql**ファイルの場所へのポインターを指定します。 ディストリビューション エージェントは、サブスクライバー側でスナップショットを適用するとき、レプリケートされたオブジェクト スクリプトより前に、プリスナップショット スクリプトを実行します。|  
|**post_snapshot_script**|**nvarchar (255)**|**.Sql**ファイルの場所へのポインターを指定します。 ディストリビューションエージェントは、他のすべてのレプリケートされたオブジェクトスクリプトとデータが初期同期中に適用された後に、ポストスナップショットスクリプトを実行します。|  
|**compress_snapshot**|**bit**|*Alt_snapshot_folder*の場所に書き込まれるスナップショットを CAB 形式で圧縮することを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] ます。**1**は、スナップショットが圧縮されることを意味します。|  
|**ftp_address**|**sysname**|ディストリビューター用の FTP サービスのネットワークアドレス。 ディストリビューション エージェントが受け取るパブリケーション スナップショット ファイルの場所を示します。|  
|**ftp_port**|**int**|ディストリビューターの FTP サービスのポート番号。 ディストリビューションエージェントが取得するパブリケーションスナップショットファイルの場所を指定します。|  
|**ftp_subdirectory**|**nvarchar (255)**|パブリケーションで FTP を使用したスナップショットの配布がサポートされている場合に、ディストリビューションエージェントでスナップショットファイルを取得できる場所を指定します。|  
|**ftp_login**|**sysname**|FTP サービスへの接続に使用するユーザー名。|  
|**ftp_password**|**nvarchar (524)**|FTP サービスへの接続に使用するユーザーパスワード。|  
|**allow_dts**|**bit**|パブリケーションがデータ変換を許可するかどうかを指定します。 **1** は、DTS 変換が許可されることを指定します。|  
|**allow_subscription_copy**|**bit**|このパブリケーションをサブスクライブするサブスクリプションデータベースをコピーする機能が有効になっているかどうかを指定します。 **1** は、コピーが許可されることを意味します。|  
|**centralized_conflicts**|**bit**|競合レコードがパブリッシャーに格納されるかどうかを示します。<br /><br /> **0** = 競合レコードは、競合の原因となったパブリッシャーとサブスクライバーの両方に格納されます。<br /><br /> **1** = 競合レコードはパブリッシャーに格納されます。|  
|**conflict_retention**|**int**|競合の保有期間を日数で指定します。|  
|**conflict_policy**|**int**|キュー更新サブスクライバーオプションを使用する場合の競合解決ポリシーを指定します。 次のいずれかの値を指定します。<br /><br /> **1** = パブリッシャー優先。<br /><br /> **2** = サブスクライバー優先。<br /><br /> **3** = サブスクリプションは再初期化されます。|  
|**queue_type**|**int**|使用されるキューの種類。 次のいずれかの値を指定します。<br /><br /> **1** = msmq は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] メッセージキューを使用してトランザクションを格納します。<br /><br /> **2** = sql: を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクションを格納します。<br /><br /> 注: [!INCLUDE[msCoName](../../includes/msconame-md.md)] メッセージキューの使用は推奨されておらず、使用できなくなりました。|  
|**ad_guidname**|**sysname**|パブリケーションが Active Directory でパブリッシュされるかどうかを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] ます。 有効なグローバル一意識別子 (GUID) は、パブリケーションが Active Directory にパブリッシュされることを指定します。 GUID は、対応する Active Directory パブリケーションオブジェクトの **objectGUID**です。 NULL の場合、パブリケーションは Active Directory でパブリッシュされません。|  
|**backward_comp_level**|**int**|データベースの互換性レベル。次のいずれかの値になります。<br /><br /> **90**  =  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。<br /><br /> **100**  =  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 。<br /><br /> **110**  =  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 。<br /><br /> **120**  =  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。|  
|**allow_initialize_from_backup**|**bit**|サブスクライバーが、初期スナップショットではなくバックアップから、このパブリケーションに対するサブスクリプションを初期化できるかどうかを示します。 **1** は、サブスクリプションをバックアップから初期化できることを意味します。 **0** は、サブスクリプションが使用できないことを意味します。 詳細については、「 [スナップショットを使用しないトランザクション サブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)を使用して、サブスクリプションを手動で初期化する方法について説明します。|  
|**min_autonosync_lsn**|**[バイナリ]**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|パブリケーションでスキーマレプリケーションがサポートされているかどうかを示します。 **1** は、パブリッシャーで実行されるデータ定義言語 (DDL) ステートメントがレプリケートされることを示し、 **0** は ddl ステートメントがレプリケートされないことを示します。 詳細については、「[パブリケーション データベースでのスキーマの変更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)」を参照してください。|  
|**options**|**int**|追加のパブリッシングオプションを指定するビットマップ。ビットごとのオプションの値は次のとおりです。<br /><br /> **0x1** -ピアツーピアレプリケーションに対して有効になります。<br /><br /> **0x2** -ピアツーピアレプリケーションのローカル変更のみをパブリッシュします。<br /><br /> **0x4** -以外のサブスクライバーに対して有効 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。<br /><br /> **0x8** -ピアツーピア競合検出に対して有効です。|  
|**originator_id**|**smallint**|競合検出のためにピア ツー ピア レプリケーション トポロジの各ノードを識別します。 詳細については、「 [ピア ツー ピア レプリケーションにおける競合検出](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addpublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
