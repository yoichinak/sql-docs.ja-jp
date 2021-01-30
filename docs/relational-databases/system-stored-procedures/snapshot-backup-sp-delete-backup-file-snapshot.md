---
description: sp_delete_backup_file_snapshot (Transact-sql)
title: sp_delete_backup_file_snapshot (Transact-sql) |Microsoft Docs
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.custom: ''
ms.technology: system-objects
ms.topic: reference
dev_langs:
- TSQL
ms.assetid: 5afe5530-a404-4fa5-af3c-bc7c3ca43ce6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0edcaca6a812ed5162aa94a091a5f2d27a83baab
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99186024"
---
# <a name="sp_delete_backup_file_snapshot-transact-sql"></a>sp_delete_backup_file_snapshot (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  指定されたデータベースから、指定されたバックアップスナップショットを削除します。 このシステムストアドプロシージャを **sys.fn_db_backup_file_snapshots** システム関数と組み合わせて使用して、孤立したバックアップスナップショットを特定および削除します。 詳細については、「 [Azure でのデータベース ファイルのファイル スナップショット バックアップ](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)」を参照してください。  

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_delete_backup_file_snapshot  
    [ @db_name = ] N'<database_name>  
    , [ @snapshot_url = ] N'<snapshot_url>  
```  
  
## <a name="arguments"></a>引数  
 *[ @db_name =] database_name*  
 削除するスナップショットを含むデータベースの名前を Unicode 文字列として指定します。  
  
 *[ @snapshot_url =] snapshot_url*  
 削除するスナップショットの URL を Unicode 文字列として指定します。  
  
## <a name="permissions"></a>アクセス許可  
 ALTER ANY DATABASE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [sys.fn_db_backup_file_snapshots &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)   
 [sp_delete_backup (Transact-SQL)](../../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
  
  
