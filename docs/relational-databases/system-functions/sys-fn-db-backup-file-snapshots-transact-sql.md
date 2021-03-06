---
description: sys.fn_db_backup_file_snapshots (Transact-sql)
title: sys.fn_db_backup_file_snapshots (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
dev_langs:
- TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 7e0df203aaf46dfbf2ab89f68eff9e1efde8a57f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99206063"
---
# <a name="sysfn_db_backup_file_snapshots-transact-sql"></a>sys.fn_db_backup_file_snapshots (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  データベースファイルに関連付けられている Azure スナップショットを返します。 指定されたデータベースが見つからない場合、またはデータベースファイルが Microsoft Azure Blob Storage サービスに格納されていない場合、行は返されません。 このシステム関数を **sys.sp_delete_backup_file_snapshot** システムストアドプロシージャと共に使用して、孤立したバックアップスナップショットを特定および削除します。 詳細については、「 [Azure でのデータベース ファイルのファイル スナップショット バックアップ](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_db_backup_file_snapshots   
   [ ( database_name ) ]  
```  
  
## <a name="arguments"></a>引数  
 *Database_name*  
 クエリ対象のデータベースの名前。 NULL の場合、この関数は現在のデータベーススコープで実行されます。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|file_id|**int**|データベースのファイル ID。 NULL 値は許可されません。|  
|snapshot_time|**nvarchar(260)**|REST API によって返されるスナップショットのタイムスタンプ。 スナップショットが存在しない場合は NULL を返します。|  
|snapshot_url|**nvarchar(360)**|ファイルスナップショットへの完全な URL です。 スナップショットが存在しない場合は NULL を返します。|  
  
## <a name="permissions"></a>アクセス許可  
 データベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [sp_delete_backup_file_snapshot &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)   
 [sp_delete_backup (Transact-SQL)](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
