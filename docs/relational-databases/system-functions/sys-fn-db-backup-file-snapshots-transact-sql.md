---
description: fn_db_backup_file_snapshots (Transact-sql)
title: fn_db_backup_file_snapshots (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 45010ff2-219f-4086-9ea4-016a6c17cddd
author: rothja
ms.author: jroth
ms.openlocfilehash: 067a1d65b65c1e2cc9bde252e6f56951e87950a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427794"
---
# <a name="sysfn_db_backup_file_snapshots-transact-sql"></a>fn_db_backup_file_snapshots (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  データベースファイルに関連付けられている Azure スナップショットを返します。 指定されたデータベースが見つからない場合、またはデータベースファイルが Microsoft Azure Blob ストレージサービスに格納されていない場合、行は返されません。 このシステム関数を **sp_delete_backup_file_snapshot** システムストアドプロシージャと共に使用して、孤立したバックアップスナップショットを特定および削除します。 詳細については、「 [Azure でのデータベース ファイルのファイル スナップショット バックアップ](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)」を参照してください。  
  
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
  
  
