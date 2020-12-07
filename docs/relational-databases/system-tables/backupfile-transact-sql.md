---
description: backupfile (Transact-sql)
title: backupfile (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- backupfile
- backupfile_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- file backups [SQL Server], backupfile system table
- backupfile system table
ms.assetid: f1a7fc0a-f4b4-47eb-9138-eebf930dc9ac
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e59789c2d4de9174a43b34881e7b45a914cfd2c3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89525555"
---
# <a name="backupfile-transact-sql"></a>backupfile (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベースの各データまたは各ログ ファイルに対して 1 行のデータを格納します。 各列では、バックアップ作成時のファイル構成の詳細が示されます。 ファイルがバックアップに含まれるかどうかは、 **is_present** 列によって決まります。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|バックアップ セットを格納するファイルの一意な識別番号。 **Backupset (backup_set_id)** を参照します。|  
|**first_family_number**|**tinyint**|このバックアップファイルが含まれている最初のメディアのファミリ番号。 NULL にすることができます。|  
|**first_media_number**|**smallint**|バックアップ ファイルが保存されている先頭のメディアのメディア番号。 NULL にすることができます。|  
|**filegroup_name**|**nvarchar(128)**|バックアップされたデータベースファイルを含むファイルグループの名前。 NULL にすることができます。|  
|**page_size**|**int**|ページのサイズ (バイト単位)。|  
|**file_number**|**numeric (10, 0)**|データベース内で一意なファイル識別番号 ( **database_files**に対応し**ます。file_id**)。|  
|**backed_up_page_count**|**numeric (10, 0)**|バックアップされたページ数。 NULL にすることができます。|  
|**file_type**|**char(1)**|バックアップされたファイル。次のいずれかです。<br /><br /> D = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ ファイル<br /><br /> L = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログファイル。<br /><br /> F = フルテキスト カタログ<br /><br /> NULL にすることができます。|  
|**source_file_block_size**|**numeric (10, 0)**|バックアップ時に元のデータファイルまたはログファイルが格納されていたデバイス。 NULL にすることができます。|  
|**file_size**|**numeric(20,0)**|バックアップされたファイルの長さ (バイト単位)。 NULL にすることができます。|  
|**logical_name**|**nvarchar(128)**|バックアップされたファイルの論理名。 NULL にすることができます。|  
|**physical_drive**|**nvarchar(260)**|物理ドライブまたはパーティション名。 NULL にすることができます。|  
|**physical_name**|**nvarchar(260)**|残りの物理 (オペレーティングシステム) ファイル名。 NULL にすることができます。|  
|**状態**|**tinyint**|ファイルの状態。次のいずれかになります。<br /><br /> 0 = ONLINE<br /><br /> 1 = 復元中<br /><br /> 2 = 回復中<br /><br /> 3 = RECOVERY PENDING <br /><br /> 4 = 問題あり<br /><br /> 6 = OFFLINE <br /><br /> 7 = DEFUNCT<br /><br /> 8 = ドロップされました<br /><br /> 注: 値5はスキップされるので、これらの値はデータベースの状態の値に対応します。|  
|**state_desc**|**nvarchar (64)**|ファイルの状態の説明。次のいずれかになります。<br /><br /> ONLINE RESTORING <br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT OFFLINE DEFUNCT|  
|**create_lsn**|**numeric(25,0)**|ファイルが作成されたときのログ シーケンス番号。|  
|**drop_lsn**|**numeric(25,0)**|ファイルが削除されたときのログ シーケンス番号。 NULL にすることができます。<br /><br /> ファイルが削除されていない場合、この値は NULL です。|  
|**file_guid**|**uniqueidentifier**|ファイルの一意識別子。|  
|**read_only_lsn**|**numeric(25,0)**|このファイルを含むファイル グループが、前回読み書き可能から読み取り専用に変更されたときのログ シーケンス番号。 NULL にすることができます。|  
|**read_write_lsn**|**numeric(25,0)**|このファイルを含むファイル グループが、前回読み取り専用から読み書き可能に変更されたときのログ シーケンス番号。 NULL にすることができます。|  
|**differential_base_lsn**|**numeric(25,0)**|差分バックアップのベース LSN。 差分バックアップには、 **differential_base_lsn**以上のログシーケンス番号を持つデータエクステントのみが含まれます。<br /><br /> その他の種類のバックアップの場合、この値は NULL です。|  
|**differential_base_guid**|**uniqueidentifier**|差分バックアップの場合、ファイルの差分ベースとなる最新のデータ バックアップの一意識別子。この値が NULL の場合、ファイルは差分バックアップに含まれますが、ベースの作成後に追加されています。<br /><br /> その他の種類のバックアップの場合、この値は NULL です。|  
|**backup_size**|**numeric(20,0)**|このファイルのバックアップ サイズ (バイト単位)。|  
|**filegroup_guid**|**uniqueidentifier**|ファイル グループの ID。 Backupfilegroup テーブルでファイルグループの情報を検索するには、 **backup_set_id**で**filegroup_guid**を使用します。|  
|**is_readonly**|**bit**|1 = ファイルは読み取り専用です。|  
|**is_present**|**bit**|1 = ファイルはバックアップ セットに含まれる。|  
  
## <a name="remarks"></a>解説  
 LOADHISTORY を使用した *backup_device* からの RESTORE verifyonly は、 **backupmediaset** テーブルの列に、メディアセットヘッダーからの適切な値を設定します。  
  
 このテーブルおよびその他のバックアップテーブルと履歴テーブルの行の数を減らすには、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) ストアドプロシージャを実行します。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のテーブルのバックアップと復元 ](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
