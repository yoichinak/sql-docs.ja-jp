---
description: sys.dm_db_xtp_object_stats (Transact-SQL)
title: sys.dm_db_xtp_object_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_object_stats_TSQL
- sys.dm_db_xtp_object_stats
- dm_db_xtp_object_stats
- sys.dm_db_xtp_object_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_object_stats dynamic management view
ms.assetid: 07300b59-3cab-4d3e-8138-5ea8f584f88f
author: markingmyname
ms.author: maghan
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f6d6c0d191022099e027b29a5be1b34b592da31f
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834121"
---
# <a name="sysdm_db_xtp_object_stats-transact-sql"></a>sys.dm_db_xtp_object_stats (Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  最後にデータベースを再起動してから、各オブジェクトに対する操作の影響を受けた行数を報告し [!INCLUDE[hek_2](../../includes/hek-2-md.md)] ます。 トランザクションのコミットまたはロールバックが行われたかどうかに関係なく、操作の実行時に統計が更新されます。  
  
 sys.dm_db_xtp_object_stats は、変化の著しいメモリ最適化テーブルを特定するために役立ちます。 各インデックスはパフォーマンスに影響するため、テーブル内でまったく使用されていないインデックスまたはほとんど使用されていないインデックスの削除を検討することができます。 ハッシュインデックスがある場合は、バケット数を定期的に再評価する必要があります。 詳細については、「 [Determining the Correct Bucket Count for Hash Indexes](/previous-versions/sql/)」を参照してください。  
  
 sys.dm_db_xtp_object_stats は、書き込み/書き込みの競合が発生するメモリ最適化テーブルを特定するのに役立ち、アプリケーションのパフォーマンスに影響を与える可能性があります。 たとえば、トランザクションの再試行ロジックがあれば、同じステートメントの実行が複数回必要になることがあります。 また、この情報を使用して、書き込み/書き込みエラー処理を必要とするテーブル (およびビジネスロジック) を識別することもできます。  
  
 このビューには、データベース内のメモリ最適化テーブルごとに 1 行のデータが格納されます。  
  
 詳細については、「[インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)」を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|オブジェクトの ID。|  
|row_insert_attempts|**bigint**|コミットされたトランザクションと中止されたトランザクションの両方によって最後のデータベースが再起動されてからテーブルに挿入された行数。|  
|row_update_attempts|**bigint**|コミットされたトランザクションと中止されたトランザクションの両方によって最後のデータベースが再起動された後に、テーブル内で更新された行の数。|  
|row_delete_attempts|**bigint**|コミットされたトランザクションと中止されたトランザクションの両方によって、前回のデータベースの再起動以降にテーブルから削除された行の数。|  
|write_conflicts|**bigint**|前回データベースが再起動されてから発生した書き込み競合の数。|  
|unique_constraint_violations|**bigint**|前回のデータベースの再起動以降に発生した unique 制約違反の数。|  
|object_address|**varbinary (8)**|内部使用のみです。|  
  
## <a name="permissions"></a>アクセス許可  
 現在のデータベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
