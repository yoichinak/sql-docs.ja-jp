---
description: managed_backup。 fn_available_backups (Transact-sql)
title: managed_backup。 fn_available_backups (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_available_backups
- smart_admin.fn_available_backups_TSQL
- fn_available_backups_TSQL
- fn_available_backups
dev_langs:
- TSQL
helpviewer_keywords:
- fn_available_backups
- smart_admin.fn_available_backups
ms.assetid: 7aa84474-16e5-49bd-a703-c8d1408ef107
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 23c7f7cb176bf91494b41cf8b81435b287d261fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419536"
---
# <a name="managed_backupfn_available_backups-transact-sql"></a>managed_backup。 fn_available_backups (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  指定されたデータベースに使用可能なバックアップ ファイルの 0 行、1 行、または複数の行から成るテーブルを返します。 返されるバックアップファイルは、によって作成されたバックアップです [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
managed_backup.fn_available_backups ([@database_name = ] 'database name')  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引数  
 @database_name  
 データベースの名前。 @database_nameは NVARCHAR (512) です。  
  
## <a name="table-returned"></a>返されるテーブル  
 テーブルには、(database_guid、backup_start_date、および first_lsn、backup_type) に対して一意のクラスター化された制約があります。   
データベースを削除してから再作成すると、すべてのデータベースのバックアップ セットが返されます。 出力は、各データベースを一意に識別する database_guid に従って並べ替えられます。   
LSN にギャップがある場合は、ログチェーンが中断されていることを意味します。テーブルには、欠落している LSN セグメントごとに特殊な行が含まれます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|Backup_path|NVARCHAR(260) COLLATE Latin1_General_CI_AS_KS_WS|バックアップファイルの URL。|  
|backup_type|NVARCHAR (6)|データベースバックアップ用の ' DB ' (ログバックアップの場合)|  
|expiration_date|DATETIME|このファイルが削除される予定の日付。 これは、指定された保有期間内の特定の時点にデータベースを復旧する機能に基づいて設定されます。|  
|database_guid|一意|指定されたデータベースの GUID 値。  GUID はデータベースを一意に識別します。|  
|first_lsn|数値 (25, 0)|バックアップセット内の最初または最も古いログレコードのログシーケンス番号。 NULL にすることができます。|  
|last_lsn|数値 (25, 0)|バックアップ セットの次のログ レコードのログ シーケンス番号。 NULL にすることができます。|  
|backup_start_date|DATETIME|バックアップ操作が開始された日付と時刻。|  
|backup_finish_date|NVARCHAR (128)|バックアップ操作が終了した日付と時刻。|  
|machine_name|NVARCHAR (128)|SQL Server インスタンスがインストールされ、実行されているコンピューターの名前 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。|  
|last_recovery_fork_id|一意|最後の復旧分岐の id 番号。|  
|first_recovery_fork_id|一意|開始復旧分岐の ID。 データバックアップの場合、first_recovery_fork_guid は last_recovery_fork_guid と同じになります。|  
|fork_point_lsn|数値 (25, 0)|first_recovery_fork_id が last_recovery_fork_id に等しくない場合は、分岐ポイントのログ シーケンス番号。 これらが同じである場合、この値は NULL になります。|  
|availability_group_guid|一意|データベースが Always On データベースの場合、これが可用性グループの GUID になります。 それ以外の場合、この値は NULL になります。|  
  
## <a name="return-code-value"></a>リターン コード値  
 0 (成功) または 1 (失敗)。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 この関数に対する **SELECT** 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] データベース ' MyDB ' に対してバックアップされている利用可能なすべてのバックアップを一覧表示します。  
  
```  
SELECT *   
FROM msdb.managed_backup.fn_available_backups ('MyDB')  
  
```  
  
## <a name="see-also"></a>参照  
 [マネージバックアップを Microsoft Azure に SQL Server](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)   
 [Microsoft Azure に格納されたバックアップからの復元](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
  
  
