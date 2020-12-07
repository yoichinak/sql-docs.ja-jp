---
description: backupset (Transact-sql)
title: backupset (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupset
- backupset_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backupset system table
- backup media [SQL Server], backupset system table
- backup sets [SQL Server]
ms.assetid: 6ff79bbf-4acf-4f75-926f-38637ca8a943
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 84c61b1e6517bc98e8acb32a8215f2dad853d7e5
ms.sourcegitcommit: 985e2e8e494badeac6d6b652cd35765fd9c12d80
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328597"
---
# <a name="backupset-transact-sql"></a>backupset (Transact-sql)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  バックアップ セットごとに 1 行のデータを格納します。 *バックアップ セット* には、正常に終了した 1 つのバックアップ操作のバックアップが含まれます。 RESTORE、RESTORE FILELISTONLY、RESTORE HEADERONLY、および RESTORE VERIFYONLY ステートメントは、単一または複数の指定バックアップ デバイス上のメディア セット内にある単一のバックアップ セットに対して機能します。  
  
 このテーブルは、 **msdb** データベースに格納されます。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|バックアップセットを識別する一意のバックアップセット識別番号。 Id、主キー。|  
|**backup_set_uuid**|**uniqueidentifier**|バックアップセットを識別する一意のバックアップセット識別番号。|  
|**media_set_id**|**int**|バックアップセットを含むメディアセットを識別する一意のメディアセット識別番号。 **Backupmediaset (media_set_id)** を参照します。|  
|**first_family_number**|**tinyint**|バックアップセットが開始されるメディアのファミリ番号。 NULL にすることができます。|  
|**first_media_number**|**smallint**|バックアップセットが開始されるメディアのメディア番号。 NULL にすることができます。|  
|**last_family_number**|**tinyint**|バックアップ セットの最終メディアのファミリ番号。 NULL にすることができます。|  
|**last_media_number**|**smallint**|バックアップ セットの最終メディアのメディア番号。 NULL にすることができます。|  
|**catalog_family_number**|**tinyint**|バックアップ セット ディレクトリの先頭を含むメディアのファミリ番号。 NULL にすることができます。|  
|**catalog_media_number**|**smallint**|バックアップ セット ディレクトリの先頭を含むメディアのメディア番号。 NULL にすることができます。|  
|**position**|**int**|適切なバックアップセットとファイルを検索するために復元操作で使用されるバックアップセットの位置。 NULL にすることができます。 詳細については、「FILE in [BACKUP &#40;transact-sql&#41;](../../t-sql/statements/backup-transact-sql.md)」を参照してください。|  
|**expiration_date**|**datetime**|バックアップ セットの期限が切れる日付と時刻。 NULL にすることができます。|  
|**software_vendor_id**|**int**|バックアップ メディア ヘッダーを記述するソフトウェア ベンダーの識別番号。 NULL にすることができます。|  
|**name**|**nvarchar(128)**|バックアップ セットの名前。 NULL にすることができます。|  
|**description**|**nvarchar (255)**|バックアップセットの説明です。 NULL にすることができます。|  
|**user_name**|**nvarchar(128)**|バックアップ操作を実行するユーザー名。 NULL にすることができます。|  
|**software_major_version**|**tinyint**|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メジャーバージョン番号。 NULL にすることができます。|  
|**software_minor_version**|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマイナー バージョン番号。 NULL にすることができます。|  
|**software_build_version**|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のビルド番号。 NULL にすることができます。|  
|**time_zone**|**smallint**|バックアップ操作の開始時のタイムゾーン情報を使用して、ローカル時刻 (バックアップ操作が実行されている場所) と世界協定時刻 (UTC) の差を15分間隔で指定します。 値は、-48 ~ + 48 の範囲で指定できます。 値 127 は、不明な状態を表します。 たとえば、-20 は東部標準時刻 (EST) を表し、これは UTC の 5 時間前にあたります。 NULL にすることができます。|  
|**mtf_minor_version**|**tinyint**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Tape Format のマイナー バージョン番号。 NULL にすることができます。|  
|**first_lsn**|**numeric(25,0)**|バックアップセット内の最初または最も古いログレコードのログシーケンス番号。 NULL にすることができます。|  
|**last_lsn**|**numeric(25,0)**|バックアップ セットの次のログ レコードのログ シーケンス番号。 NULL にすることができます。|  
|**checkpoint_lsn**|**numeric(25,0)**|再実行を開始する必要があるログ レコードのログ シーケンス番号。 NULL にすることができます。|  
|**database_backup_lsn**|**numeric(25,0)**|データベース全体の最新バックアップのログ シーケンス番号。 NULL にすることができます。<br /><br /> **database_backup_lsn** は、バックアップの開始時にトリガーされる "チェックポイントの開始" です。 データベースがアイドル状態で、レプリケーションが構成されていないときにバックアップが実行された場合、この LSN は **first_lsn** と一致します。|  
|**database_creation_date**|**datetime**|データベースが最初に作成された日付と時刻。 NULL にすることができます。|  
|**backup_start_date**|**datetime**|バックアップ操作が開始された日付と時刻。 NULL にすることができます。|  
|**backup_finish_date**|**datetime**|バックアップ操作が終了した日付と時刻。 NULL にすることができます。|  
|**type**|**char(1)**|バックアップの種類。 次の値をとります。<br /><br /> D = データベース<br /><br /> I = データベースの差分<br /><br /> L = ログ<br /><br /> F = ファイルまたはファイル グループ<br /><br /> G = ファイルの差分<br /><br /> P = 部分的<br /><br /> Q = 部分的な差分<br /><br /> NULL にすることができます。|  
|**sort_order**|**smallint**|バックアップ操作を実行するサーバーの並べ替え順。 NULL にすることができます。 並べ替え順序と照合順序の詳細については、「 [照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。|  
|**code_page**|**smallint**|バックアップ操作を実行するサーバーのコードページです。 NULL にすることができます。 コードページの詳細については、「 [照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。|  
|**compatibility_level**|**tinyint**|データベースの互換性レベルの設定。 次の値をとります。<br /><br /> 90 = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> 100 = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]<br /><br /> 110 = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br /><br /> 120 = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]<br /><br /> NULL にすることができます。<br /><br /> 互換性レベルの詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。|  
|**database_version**|**int**|データベースのバージョン番号。 NULL にすることができます。|  
|**backup_size**|**numeric(20,0)**|バックアップ セットのサイズ (バイト単位)。 NULL にすることができます。 VSS バックアップの場合、backup_size は推定値です。|  
|**database_name**|**nvarchar(128)**|バックアップ操作に関係するデータベース名。 NULL にすることができます。|  
|**server_name**|**nvarchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップ操作を実行しているサーバー名。 NULL にすることができます。|  
|**machine_name**|**nvarchar(128)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を実行しているコンピューターの名前。 NULL にすることができます。|  
|**flags**|**int**|では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **flags** 列は非推奨とされており、次のビット列に置き換えられています。<br /><br /> **has_bulk_logged_data** <br /> **is_snapshot** <br /> **is_readonly** <br /> **is_single_user** <br /> **has_backup_checksums** <br /> **is_damaged** <br /> **begins_log_chain** <br /> **has_incomplete_metadata** <br /> **is_force_offline** <br /> **is_copy_only**<br /><br /> NULL にすることができます。<br /><br /> 以前のバージョンののバックアップセットで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、フラグビット:<br />1 = バックアップには最小限のログ データが含まれている。 <br />2 = WITH SNAPSHOT が使用されました。 <br />4 = バックアップ時にデータベースは読み取り専用でした。<br />8 = バックアップ時にデータベースがシングルユーザーモードになっています。|  
|**unicode_locale**|**int**|Unicode ロケール。 NULL にすることができます。|  
|**unicode_compare_style**|**int**|Unicode 比較スタイル。 NULL にすることができます。|  
|**collation_name**|**nvarchar(128)**|照合順序名。 NULL にすることができます。|  
|**Is_password_protected**|**bit**|バックアップセットです。<br /><br /> 保護されたパスワード:<br /><br /> 0 = 保護されていない<br /><br /> 1 = 保護されている|  
|**recovery_model**|**nvarchar(60)**|データベースの復旧モデル。<br /><br /> FULL<br /><br /> BULK-LOGGED<br /><br /> SIMPLE|  
|**has_bulk_logged_data**|**bit**|1 = バックアップには一括ログデータが含まれます。|  
|**is_snapshot**|**bit**|1 = バックアップは、SNAPSHOT オプションを使用して作成されました。|  
|**is_readonly**|**bit**|1 = バックアップ時にデータベースは読み取り専用でした。|  
|**is_single_user**|**bit**|1 = データベースはバックアップ時にシングルユーザーでした。|  
|**has_backup_checksums**|**bit**|1 = バックアップ チェックサムを含むバックアップ。|  
|**is_damaged**|**bit**|1 = バックアップの作成時、データベースの損傷が検出された。 エラーに関係なくバックアップ操作の続行が要求されました。|  
|**begins_log_chain**|**bit**|1 = 連鎖的なログ バックアップの先頭。 ログチェーンは、データベースを作成した後、または単純復旧モデルから完全復旧モデルまたは一括ログ復旧モデルに切り替えた後に作成された最初のログバックアップから始まります。|  
|**has_incomplete_metadata**|**bit**|1 = 不完全なメタデータでのログ末尾のバックアップ。 詳細については、「[ログ末尾のバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)」を参照してください。|  
|**is_force_offline**|**bit**|1 = バックアップ時、データベースが NORECOVERY オプションによってオフラインにされた。|  
|**is_copy_only**|**bit**|1 = コピーのみのバックアップ。 詳細については、「[コピーのみのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)」を参照してください。|  
|**first_recovery_fork_guid**|**uniqueidentifier**|開始復旧分岐の ID。 これは、RESTORE HEADERONLY の **Firstrecoveryforkid** に対応しています。<br /><br /> データバックアップの場合、 **first_recovery_fork_guid** は **last_recovery_fork_guid** と同じになります。|  
|**last_recovery_fork_guid**|**uniqueidentifier**|終了する復旧分岐の ID。 これは、RESTORE HEADERONLY の **Recoveryforkid** に対応しています。<br /><br /> データバックアップの場合、 **first_recovery_fork_guid** は **last_recovery_fork_guid** と同じになります。|  
|**fork_point_lsn**|**numeric(25,0)**|**First_recovery_fork_guid** が **last_recovery_fork_guid** と等しくない場合、これは分岐ポイントのログシーケンス番号です。 それ以外の場合は NULL になります。|  
|**database_guid**|**uniqueidentifier**|データベースの一意の ID。 これは、RESTORE HEADERONLY の **Bindingid** に対応します。 データベースが復元されると、新しい値が割り当てられます。|  
|**family_guid**|**uniqueidentifier**|作成時の元のデータベースの一意の ID。 この値は、データベースが復元されるときに、別の名前であっても変わりません。|  
|**differential_base_lsn**|**numeric(25,0)**|差分バックアップのベース LSN。 単一ベースの差分バックアップの場合Lsn が **differential_base_lsn** 以上の変更が、差分バックアップに含まれています。<br /><br /> マルチベースの差分では、値は NULL で、ベース LSN はファイルレベルで決定する必要があります (「 [backupfile &#40;transact-sql&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)」を参照してください)。<br /><br /> 差分以外のバックアップの種類の場合、値は常に NULL になります。|  
|**differential_base_guid**|**uniqueidentifier**|シングル ベースの差分バックアップの場合は、差分ベースの一意識別子。<br /><br /> マルチ ベースの差分バックアップの場合は NULL。差分のベースはファイル レベルで決定される必要があります。<br /><br /> 差分以外のバックアップの種類の場合、値は NULL になります。|  
|**compressed_backup_size**|**Numeric (20, 0)**|ディスクに格納されたバックアップの総バイト数。<br /><br /> 圧縮比率を計算するには、 **compressed_backup_size** と **backup_size** を使用します。<br /><br /> この値は、 **msdb** のアップグレード中に NULL に設定されます。 これは圧縮されていないバックアップを示します。|  
|**key_algorithm**|**nvarchar(32)**|バックアップの暗号化に使用される暗号化アルゴリズム。 NO_Encryption 値は、バックアップが暗号化されていないことを示しています。|  
|**encryptor_thumbprint**|**varbinary(20)**|データベースに保存されている証明書や非対称キーを検索するために使用される暗号化機能の拇印。 バックアップが暗号化されていない場合、この値は NULL になります。|  
|**encryptor_type**|**nvarchar(32)**|使用される暗号化の種類:証明書キーまたは非対称キー。 . バックアップが暗号化されていない場合、この値は NULL になります。|  
  
## <a name="remarks"></a>解説  
 LOADHISTORY を使用した *backup_device* からの RESTORE verifyonly は、 **backupmediaset** テーブルの列に、メディアセットヘッダーからの適切な値を設定します。  
  
 このテーブルおよびその他のバックアップテーブルと履歴テーブルの行の数を減らすには、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) ストアドプロシージャを実行します。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のテーブルのバックアップと復元 ](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [バックアップ中および復元中に発生する可能性があるメディア エラー &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [復旧モデル &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [Transact-sql&#41;&#40;のテーブルのバックアップと復元 ](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)  
  
  
