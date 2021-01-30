---
title: sys.remote_data_archive_tables (Transact-sql) |Microsoft Docs
description: Stretch が有効なローカルテーブルのデータを格納するリモートテーブルごとに1行のデータを格納 sys.remote_data_archive_tables 方法について説明します。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: reference
f1_keywords:
- sys.remote_data_archive_tables
- sys.remote_data_archive_tables_TSQL
- remote_data_archive_tables
- remote_data_archive_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_tables catalog view
ms.assetid: 765069b7-60fd-414c-875f-3455460b75cd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: cd0c62c78c93557c011c299c7cf0e65c7285fba8
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99209037"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_tables"></a>カタログビューの Stretch Database-sys.remote_data_archive_tables
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Stretch が有効なローカルテーブルのデータを格納するリモートテーブルごとに1行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Stretch が有効なローカルテーブルのオブジェクト ID。|  
|**remote_database_id**|**int**|リモートデータベースの自動生成されたローカル識別子。|  
|**remote_table_name**|**sysname**|Stretch が有効なローカルテーブルに対応するリモートデータベースのテーブルの名前。|  
|**filter_predicate**|**nvarchar(max)**|移行するテーブル内の行を識別するフィルター述語 (存在する場合)。 値が null の場合、テーブル全体が移行の対象になります。<br /><br /> 詳細については、「 [テーブルの Stretch Database を有効にする](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md) 」および「 [フィルター述語を使用して移行する行を選択](~/sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)する」を参照してください。|  
|**migration_direction**|**tinyint**|データが現在移行されている方向。 使用できる値は次のとおりです。<br/>1 (送信)<br/>2 (受信)|  
|**migration_direction_desc**|**nvarchar(60)**|データが現在移行されている方向の説明。 使用できる値は次のとおりです。<br/>送信 (1)<br/>受信 (2)|  
|**is_migration_paused**|**bit**|移行が現在一時停止されているかどうかを示します。|  
|**is_reconciled**|**bit**| リモートテーブルと SQL Server テーブルが同期されているかどうかを示します。<br/><br/>**Is_reconciled** の値が 1 (true) の場合、リモートテーブルと SQL Server テーブルが同期され、リモートデータを含むクエリを実行できます。<br/><br/>**Is_reconciled** の値が 0 (false) の場合、リモートテーブルと SQL Server テーブルは同期されていません。最近移行された行は、再度移行する必要があります。 このエラーは、リモートの Azure データベースを復元した場合、またはリモートテーブルから手動で行を削除した場合に発生します。 テーブルを調整するまで、リモートデータを含むクエリを実行することはできません。 テーブルを調整するには、 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)を実行します。 |  
  
## <a name="see-also"></a>参照  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  

