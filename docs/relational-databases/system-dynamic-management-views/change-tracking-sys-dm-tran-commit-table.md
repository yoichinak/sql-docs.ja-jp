---
description: Change Tracking-sys. dm_tran_commit_table
title: dm_tran_commit_table (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_commit_table
- dm_tran_commit_table_TSQL
- sys.dm_tran_commit_table
- sys.dm_tran_commit_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_commit_table dynamic management view
ms.assetid: 732d23c5-1f6c-4e96-bc85-8f29b520cf0e
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4b35493324a0a7585c7f07a11b8dc234048b4e3f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537698"
---
# <a name="change-tracking---sysdm_tran_commit_table"></a>Change Tracking-sys. dm_tran_commit_table
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  変更の追跡によって追跡されているテーブルに対してコミットされたトランザクションごとに1つの行を表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 サポート用に提供されている sys.dm_tran_commit_table 管理ビューには、トランザクション関連の情報が表示されます。この情報は、変更の追跡によって sys.syscommittab システム テーブルに格納されます。 sys.syscommittab テーブルは、データベース固有のトランザクション ID からトランザクションのコミット ログ シーケンス番号 (LSN) とコミット タイムスタンプへの、効率的かつ永続的なマッピングを提供します。 sys.syscommittab テーブルに格納され、この管理ビューで公開されるデータは、変更の追跡が構成されたときに指定された保有期間に従ってクリーンアップされます。  
  
> [!NOTE]  
>  またはからこれを呼び出すに [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] は [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 、 **dm_pdw_nodes_tran_commit_table**という名前を使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|commit_ts|**bigint**|コミットされたトランザクションごとにデータベース固有のタイムスタンプとして機能する、単調に増加する数値。|  
|xdes_id|**bigint**|トランザクションのデータベース固有の内部 ID。|  
|commit_lbn|**bigint**|トランザクションのコミットログレコードを含むログブロックの番号。|  
|commit_csn|**bigint**|トランザクションのインスタンス固有のコミットシーケンス番号。|  
|commit_time|**smalldatetime**|トランザクションがコミットされた時刻。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [変更の追跡について &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
  


