---
description: データ コレクターのビュー (Transact-SQL)
title: データコレクタービュー (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- data collector view
- data collector [SQL Server], views
ms.assetid: a005e885-7813-4c7e-b332-b01d9e9d4054
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: bf304e44eb5f4374d4fdc1de21d7dc73fee2d72e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99184302"
---
# <a name="data-collector-views-transact-sql"></a>データ コレクターのビュー (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  データコレクターには、データコレクターの構成に関する情報を表示するための次のビューが用意されています。これには、コレクター型のプロパティ、コレクションセット、コレクションセットの項目、およびコレクションセットの実行時に取得される実行の統計情報が表示されます。 これらのビューは、 **msdb** データベースにあり、基になるテーブルの抽象レイヤーも提供します。 この抽象化により、テーブルへの直接アクセスを防止しながら、関連付けられているアプリケーションに影響を与えることなくテーブルを変更できるようにすることで、セキュリティが強化されます。  

:::row:::
    :::column:::
        [syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)
        
        [syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)
        
        [syscollector_execution_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-transact-sql.md)
        
        [syscollector_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)
    :::column-end:::
    :::column:::
        [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)
        
        [syscollector_config_store &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)
        
        [syscollector_execution_log_full &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql.md)
    :::column-end:::
:::row-end:::
  
## <a name="see-also"></a>参照  
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
