---
title: sys.dm_db_xtp_checkpoint_files (Transact-sql) |Microsoft Docs
description: ファイルサイズ、物理的な場所、トランザクション ID など、チェックポイントファイルに関する情報を表示します。 SQL Server のバージョンごとにこのビューがどのように異なるかを説明します。
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_files
- sys.dm_db_xtp_checkpoint_files_TSQL
- dm_db_xtp_checkpoint_files_TSQL
- sys.dm_db_xtp_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_files dynamic management view
ms.assetid: ac8e6333-7a9f-478a-b446-5602283e81c9
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 010b043bbaab3a5ce1712d32b1e94f800fa630d3
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92412664"
---
# <a name="sysdm_db_xtp_checkpoint_files-transact-sql"></a>sys.dm_db_xtp_checkpoint_files (Transact-sql)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  ファイルサイズ、物理的な場所、トランザクション ID など、チェックポイントファイルに関する情報を表示します。  
  
> **注:** 現在のチェックポイントが閉じていない場合は、の [状態] 列に `ys.dm_db_xtp_checkpoint_files` 新しいファイルが作成されます。 チェックポイントは、最後のチェックポイント以降のトランザクションログの増加が十分にある場合、または `CHECKPOINT` コマンド ([チェックポイント &#40;transact-sql&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)) を実行した場合に、自動的に閉じられます。  
  
 メモリ最適化ファイルグループでは、インメモリテーブルの挿入および削除された行を格納するために、追加専用のファイルが内部的に使用されます。 ファイルには2種類あります。 データファイルには挿入された行が含まれ、デルタファイルには削除された行への参照が含まれています。 
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] は、より新しいバージョンとは大幅に異なります。 [SQL Server 2014](#bkmk_2014)のトピックでは、この点について説明します。  
  
 詳細については、「 [Memory-Optimized オブジェクトのストレージの作成と管理](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)」を参照してください。  
  
##  <a name="sssql15-and-later"></a><a name="bkmk_2016"></a> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降  
 次の表では、以降のの列について説明し `sys.dm_db_xtp_checkpoint_files` **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]** ます。  
  
|列名|種類|説明|  
|-----------------|----------|-----------------|  
|container_id|**int**|データまたはデルタ ファイルが含まれているコンテナー (sys.database_files で FILESTREAM 型のファイルとして表される) の ID。 [Sys.database_files &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)の file_id と結合します。|  
|container_guid|**uniqueidentifier**|ルート、データ、またはデルタファイルが含まれているコンテナーの GUID。 Sys.database_files テーブルの file_guid と結合します。|  
|checkpoint_file_id|**uniqueidentifier**|チェックポイントファイルの GUID。|  
|relative_file_path|**nvarchar (256)**|マップ先のコンテナーを基準としたファイルの相対パス。|  
|file_type|**smallint**|-1 (無料)<br /><br /> データファイルの場合は0です。<br /><br /> デルタファイルの場合は1。<br /><br /> ルートファイルの場合は2<br /><br /> 3 (大規模なデータファイルの場合)|  
|file_type_desc|**nvarchar(60)**|FREE-空きとして保持されているすべてのファイルを割り当て可能です。 空きファイルのサイズは、システムによって予想されるニーズによって異なります。 最大サイズは 1 GB です。<br /><br /> データデータファイルには、メモリ最適化テーブルに挿入された行が含まれています。<br /><br /> デルタデルタファイルには、削除されたデータファイル内の行への参照が含まれています。<br /><br /> ルートルートファイルには、メモリ最適化オブジェクトおよびネイティブコンパイルオブジェクト用のシステムメタデータが含まれています。<br /><br /> 大規模なデータ-大規模なデータファイルには、(n) varchar (max) 列と varbinary (max) 列に挿入された値、およびメモリ最適化テーブルの列ストアインデックスの一部である列セグメントが含まれています。|  
|internal_storage_slot|**int**|内部ストレージ配列内のファイルのインデックス。 ルートの場合は NULL、状態が1以外の場合はです。|  
|checkpoint_pair_file_id|**uniqueidentifier**|対応するデータファイルまたはデルタファイル。 ルートの場合は NULL です。|  
|file_size_in_bytes|**bigint**|ディスク上のファイルのサイズ。|  
|file_size_used_in_bytes|**bigint**|まだ設定されているチェックポイントファイルペアの場合、この列は次のチェックポイントの後に更新されます。|  
|logical_row_count|**bigint**|データの場合は、挿入される行の数。<br /><br /> デルタの場合、drop table のアカウンティング後に削除される行の数。<br /><br /> Root の場合は NULL です。|  
|state|**smallint**|0-事前作成済み<br /><br /> 1-構築中<br /><br /> 2 - ACTIVE<br /><br /> 3-マージターゲット<br /><br /> 8-ログの切り捨てを待機しています|  
|state_desc|**nvarchar(60)**|PRECREATED-トランザクションの実行中に新しいファイルを割り当てるための待機を最小化または排除するために、いくつかのチェックポイントファイルが事前に割り当てられています。 これらの事前作成されたファイルのサイズは、ワークロードの予想されるニーズによって異なりますが、データは含まれません。 これは、MEMORY_OPTIMIZED_DATA ファイルグループを持つデータベースのストレージオーバーヘッドです。<br /><br /> 構築中-これらのチェックポイントファイルは構築中であり、データベースによって生成されたログレコードに基づいて設定されており、まだチェックポイントの一部ではありません。<br /><br /> アクティブ-以前に閉じられたチェックポイントから挿入または削除された行を含みます。 データベースの再起動時にトランザクションログのアクティブな部分を適用する前に、領域がメモリに読み取られるテーブルの内容を格納します。 マージ操作がトランザクションワークロードに対応していると仮定すると、これらのチェックポイントファイルのサイズは、メモリ最適化テーブルのメモリ内サイズの約2倍になると予想されます。<br /><br /> マージターゲット-マージ操作の対象。これらのチェックポイントファイルには、マージポリシーによって識別されたソースファイルから統合されたデータ行が格納されます。 マージがインストールされると、マージターゲットはアクティブ状態に遷移します。<br /><br /> [ログの切り捨てを待機しています]-マージがインストールされ、マージターゲットの CFP が永続的なチェックポイントの一部である場合、マージソースチェックポイントファイルはこの状態に遷移します。 この状態のファイルは、メモリ最適化テーブルを持つデータベースの操作の正確性を必要とします。  たとえば、永続的なチェックポイントから復旧して、時間内に戻ることができます。|  
|lower_bound_tsn|**bigint**|ファイル内のトランザクションの下限。状態が (1, 3) にない場合は null です。|  
|upper_bound_tsn|**bigint**|ファイル内のトランザクションの上限です。状態が (1, 3) にない場合は null です。|  
|begin_checkpoint_id|**bigint**|開始チェックポイントの ID です。|  
|end_checkpoint_id|**bigint**|エンドポイントの終了の ID。|  
|last_updated_checkpoint_id|**bigint**|このファイルを更新した最後のチェックポイントの ID です。|  
|encryption_status|**smallint**|0、1、2|  
|encryption_status_desc|**nvarchar(60)**|0 = 暗号化されていない><br /><br /> 1 = キー1で暗号化された><br /><br /> 2 = キー2で暗号化された>。 アクティブなファイルに対してのみ有効です。|  
  
##  <a name="sssql14"></a><a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 次の表では、の列について説明し `sys.dm_db_xtp_checkpoint_files` **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** ます。  
  
|列名|種類|説明|  
|-----------------|----------|-----------------|  
|container_id|**int**|データまたはデルタ ファイルが含まれているコンテナー (sys.database_files で FILESTREAM 型のファイルとして表される) の ID。 [Sys.database_files &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)の file_id と結合します。|  
|container_guid|**uniqueidentifier**|データファイルまたはデルタファイルが含まれているコンテナーの GUID。|  
|checkpoint_file_id|**GUID**|データファイルまたはデルタファイルの ID。|  
|relative_file_path|**nvarchar (256)**|コンテナーの場所を基準とする、データ ファイルまたはデルタ ファイルの相対パス。|  
|file_type|**tinyint**|0 はデータ ファイルに対応。<br /><br /> 1 はデルタ ファイルに対応。<br /><br /> State 列が7に設定されている場合は NULL になります。|  
|file_type_desc|**nvarchar(60)**|ファイルの種類: DATA_FILE、DELTA_FILE、または [状態] 列が7に設定されている場合は NULL です。|  
|internal_storage_slot|**int**|内部ストレージ配列内のファイルのインデックス。 State 列が2または3でない場合は NULL になります。|  
|checkpoint_pair_file_id|**uniqueidentifier**|対応するデータファイルまたはデルタファイル。|  
|file_size_in_bytes|**bigint**|使用されているファイルのサイズ。 State 列が5、6、または7に設定されている場合は NULL になります。|  
|file_size_used_in_bytes|**bigint**|使用されているファイルによる使用済みサイズ。 State 列が5、6、または7に設定されている場合は NULL になります。<br /><br /> まだ設定されているチェックポイントファイルペアの場合、この列は次のチェックポイントの後に更新されます。|  
|inserted_row_count|**bigint**|データファイル内の行の数。|  
|deleted_row_count|**bigint**|デルタファイル内の削除された行の数。|  
|drop_table_deleted_row_count|**bigint**|Drop table によって影響を受けるデータファイル内の行の数。 state 列が 1.に等しい場合にデータ ファイルに適用されます。<br /><br /> 削除されたテーブルから削除された行数を表示します。 Drop_table_deleted_row_count の統計は、削除されたテーブルからの行のメモリガベージコレクションが完了し、チェックポイントが取得された後にコンパイルされます。 テーブルの削除に関する統計情報がこの列に反映される前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動した場合、復旧操作の一環として統計情報が更新されます。 復旧プロセスでは、削除されたテーブルから行が読み込まれません。 削除されたテーブルに関する統計情報は、読み込みフェーズ中にコンパイルされ、復旧が完了するとこの列で報告されます。|  
|state|**int**|0-事前作成済み<br /><br /> 1-構築中<br /><br /> 2 - ACTIVE<br /><br /> 3-マージターゲット<br /><br /> 4-マージされたソース<br /><br /> 5-バックアップ/HA に必要<br /><br /> 6-廃棄 (TOMBSTONE) への移行<br /><br /> 7-廃棄 (TOMBSTONE)|  
|state_desc|**nvarchar(60)**|事前作成-データファイルとデルタファイルのペアの小さなセット (チェックポイントファイルペア (CFPs) とも呼ばれます) は、トランザクションの実行中に新しいファイルを割り当てるための待機を最小化または排除するために事前に割り当てられたまま保持されます。 データファイルのサイズは 128 MB、デルタファイルのサイズは 8 MB ですが、データは含まれていません。 CFP の数は、8 を最小として、論理プロセッサまたはスケジューラの数に応じて計算されます (コアにつき 1 個で、最大値なし)。 これは、メモリ最適化テーブルのあるデータベースにおける固定のストレージ オーバーヘッドです。<br /><br /> 新しく挿入された、場合によっては削除された可能性があるデータ行を最後のチェックポイント以降に格納する、構築時の CFPs のセット。<br /><br /> ACTIVE - この中には、閉じられた前のチェックポイント以降に挿入された行と削除された行が含まれます。 これらの CFP には、データベースの再起動時に、トランザクション ログのアクティブな部分を適用する前に必要とされる、必須である挿入された行と削除された行すべてが含まれます。 これらの CFPs のサイズは、マージ操作がトランザクションワークロードで最新であると仮定した場合、メモリ最適化テーブルのメモリ内サイズの約2倍になります。<br /><br /> マージターゲット-CFP は、マージポリシーによって識別された CFP から統合されたデータ行を格納します。 マージがインストールされると、マージターゲットはアクティブ状態に遷移します。<br /><br /> マージされたソース-マージ操作がインストールされると、ソース CFPs はマージされたソースとしてマークされます。 マージポリシーエバリュエーターは複数のマージを識別できますが、CFP は1つのマージ操作にのみ参加できます。<br /><br /> BACKUP/HA に必要-マージがインストールされ、マージターゲットの CFP が永続的なチェックポイントの一部である場合、マージソース Cfp はこの状態に遷移します。 この状態にある CFP は、メモリ最適化されたテーブルを持つデータベースを正しく運用するうえで必要とされます。  たとえば、永続的なチェックポイントから復旧して、時間内に戻ることができます。 ログの切り捨てポイントが CFP のトランザクション範囲を超えた位置に移動すれば、その CFP をガベージ コレクションの対象としてマークできます。<br /><br /> 廃棄 (TOMBSTONE) への移行-これらの CFPs は In-Memory OLTP エンジンでは不要であり、ガベージコレクションが可能です。 この状態は、これらの CFPs がバックグラウンドスレッドによって次の状態 (廃棄) に遷移するのを待機していることを示します。<br /><br /> 廃棄 (TOMBSTONE)-これらの CFPs は、filestream ガベージコレクターによってガベージコレクションが行われるのを待機しています。 ([sp_filestream_force_garbage_collection &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md))|  
|lower_bound_tsn|**bigint**|ファイルに格納されているトランザクションの下限。 State 列が2、3、または4以外の場合は Null になります。|  
|upper_bound_tsn|**bigint**|ファイルに格納されているトランザクションの上限。 State 列が2、3、または4以外の場合は Null になります。|  
|last_backup_page_count|**int**|前回のバックアップ時に決定された論理ページ数。 State 列が2、3、4、または5に設定されている場合に適用されます。 ページ数が不明の場合は NULL です。|  
|delta_watermark_tsn|**int**|このデルタファイルに書き込まれた最後のチェックポイントのトランザクションです。 これは、デルタファイルのウォーターマークです。|  
|last_checkpoint_recovery_lsn|**nvarchar (23)**|引き続きファイルを必要としている前回のチェックポイントの復旧ログ シーケンス番号。|  
|tombstone_operation_lsn|**nvarchar (23)**|tombstone_operation_lsn が、ログの切り捨てに関するログ シーケンス番号より少ない場合は、このファイルは削除されます。|  
|logical_deletion_log_block_id|**bigint**|状態5にのみ適用されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する `VIEW DATABASE STATE` 権限が必要です。  
  
## <a name="use-cases"></a>使用事例  
 次のように In-Memory OLTP によって使用されるストレージを見積もることができます。  
  
```  
-- total storage used by In-Memory OLTP  
SELECT SUM (file_size_in_bytes)/(1024*1024) as file_size_in_MB  
FROM sys.dm_db_xtp_checkpoint_files  
```  
  
  
状態およびファイルの種類別の記憶域使用率の内訳を表示するには、次のクエリを実行します。
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(file_size_in_bytes) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  

  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
