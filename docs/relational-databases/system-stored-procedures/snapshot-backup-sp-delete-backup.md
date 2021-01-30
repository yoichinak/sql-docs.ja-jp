---
description: sp_delete_backup (Transact-sql)
title: sp_delete_backup (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
dev_langs:
- TSQL
ms.assetid: 808e50ae-ff6e-4520-9ce2-530591d3d59b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 003b6422fe2485c1e7c7da43aa5f5168a75b797e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99186009"
---
# <a name="sp_delete_backup-transact-sql"></a>sp_delete_backup (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  指定されたデータベースからスナップショットバックアップセットを構成するすべてのスナップショットとバックアップファイルを削除します。 このシステムストアドプロシージャは、スナップショットバックアップセットの管理に推奨される唯一の方法です。 詳細については、「 [Azure でのデータベース ファイルのファイル スナップショット バックアップ](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_delete_backup   
    [ @backup_url = ] backup_metadata_file_url  
    ,[ [ @db_name = ] database_name | NULL ]  
```  
  
## <a name="arguments"></a>引数  
 *[ @backup_url =] backup_meta_file_url*  
 削除するバックアップの URL。これにより、バックアップファイル自体を含む、指定したバックアップセットを構成するすべてのスナップショットが削除されます。  
  
 *[ @db_name =] database_name*  
 削除するスナップショットを含むデータベースの名前です。 データベース名を指定すると、指定されたバックアップ URL が指定されたデータベースのバックアップ URL であることを確認し、 [sp_delete_backup_file_snapshot &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) を使用して各スナップショットを削除します。 データベース名が指定されていない場合、このデータベースのチェックは実行されません。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER ANY DATABASE 権限、または指定されたデータベースに対する ALTER 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [sys.fn_db_backup_file_snapshots &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup_file_snapshot (Transact-SQL)](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
