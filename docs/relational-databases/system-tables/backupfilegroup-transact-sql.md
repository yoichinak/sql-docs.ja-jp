---
description: backupfilegroup (Transact-SQL)
title: backupfilegroup (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- backupfilegroup_TSQL
- backupfilegroup
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], backupfilegroup system table
- backupfilegroup system table
ms.assetid: d26e8fbe-f5c5-4e10-b2bd-0d8e16ea21f9
author: cawrites
ms.author: chadam
ms.openlocfilehash: be220cdc204488f0c2f82244b543ae324218bc49
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99198665"
---
# <a name="backupfilegroup-transact-sql"></a>backupfilegroup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  バックアップ時に、データベース内のファイルグループごとに1行のデータを格納します。 **backupfilegroup** は **msdb** データベースに格納されます。  
  
> [!NOTE]  
>  **Backupfilegroup** テーブルには、バックアップセットではなく、データベースのファイルグループの構成が表示されます。 バックアップセットにファイルが含まれているかどうかを確認するには、 [backupfile](../../relational-databases/system-tables/backupfile-transact-sql.md)テーブルの **is_present** 列を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**backup_set_id**|**int**|ファイル グループが含まれているバックアップ セット。|  
|**name**|**sysname**|ファイルグループの名前。|  
|**filegroup_id**|**int**|ファイルグループの ID。データベース内で一意です。 は、 **data_space_id** に **対応します**。|  
|**filegroup_guid**|**uniqueidentifier**|ファイルグループのグローバル一意識別子。 NULL にすることができます。|  
|**type**|**char(2)**|コンテンツの種類。次のいずれかになります。<br /><br /> FG = "Rows" ファイルグループ<br /><br /> SL = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ ファイル グループ|  
|**type_desc**|**nvarchar(60)**|関数の種類の説明。次のいずれかになります。<br /><br /> ROWS_FILEGROUP<br /><br /> SQL_LOG_FILEGROUP |  
|**is_default**|**bit**|既定のファイルグループ。 CREATE TABLE または CREATE INDEX でファイルグループが指定されていない場合に使用されます。|  
|**is_readonly**|**bit**|1 = ファイルグループは読み取り専用です。|  
|**log_filegroup_guid**|**uniqueidentifier**|NULL にすることができます。|  
  
## <a name="remarks"></a>コメント  
  
> [!IMPORTANT]  
>  同じファイルグループ名を別のデータベースに表示できます。ただし、各ファイルグループには独自の GUID があります。 したがって、 **(backup_set_id、filegroup_guid)** は、 **backupfilegroup** 内のファイルグループを識別する一意のキーです。  
  
 LOADHISTORY を使用した *backup_device* からの RESTORE verifyonly は、 **backupmediaset** テーブルの列に、メディアセットヘッダーからの適切な値を設定します。  
  
 このテーブルおよびその他のバックアップテーブルと履歴テーブルの行の数を減らすには、 [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) ストアドプロシージャを実行します。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のテーブルのバックアップと復元 ](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
