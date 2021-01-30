---
description: cdc.lsn_time_mapping (Transact-sql)
title: cdc.lsn_time_mapping (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- cdc.lsn_time_mapping
- cdc.lsn_time_mapping_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.lsn_time_mapping
ms.assetid: 1cb7aedc-48a4-486e-9b91-d30c4bd4084e
author: cawrites
ms.author: chadam
ms.openlocfilehash: 6cf48f0c68e5e376b186e7f51361a479c9d1e67c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99203635"
---
# <a name="cdclsn_time_mapping-transact-sql"></a>cdc.lsn_time_mapping (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  変更テーブル内の行を保持しているトランザクションごとに1行の値を返します。 このテーブルは、ログシーケンス番号 (LSN) のコミット値とトランザクションがコミットされた時刻の間のマッピングに使用されます。 変更テーブルエントリがないエントリもログに記録される場合があります。 これにより、変更アクティビティが少ないか、まったくない場合に、LSN 処理の完了をテーブルに記録できます。  
  
 システムテーブルに対して直接クエリを実行しないことをお勧めします。 代わりに、transact-sql [&#41;&#40;sys.fn_cdc_map_lsn_to_time ](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) を実行し、 [transact-sql &#40;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) システム関数を sys.fn_cdc_map_time_to_lsn します。  
    
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**start_lsn**|**binary(10)**|コミットされたトランザクションの LSN。|  
|**tran_begin_time**|**datetime**|LSN に関連付けられているトランザクションが開始された時刻。|  
|**tran_end_time**|**datetime**|トランザクションが終了した時刻。|  
|**tran_id**|**varbinary (10)**|トランザクションの ID。|  
  
## <a name="see-also"></a>参照  
 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [cdc. &#60;capture_instance&#62;_CT &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)  
  
  
