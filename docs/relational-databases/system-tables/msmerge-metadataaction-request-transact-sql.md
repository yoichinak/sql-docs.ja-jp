---
description: MSmerge_metadataaction_request (Transact-sql)
title: MSmerge_metadataaction_request (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_metadataaction_request
- MSmerge_metadataaction_request_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_metadataaction_request system table
ms.assetid: cd31a114-900a-4218-ab58-d959e547c647
author: cawrites
ms.author: chadam
ms.openlocfilehash: ceef4e122ced8e8f14bdc52cae86ef358f9c3a6e
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98102041"
---
# <a name="msmerge_metadataaction_request-transact-sql"></a>MSmerge_metadataaction_request (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_metadataaction_request** テーブルには、必要な補正アクションごとに1つの行が格納されます。 Web 同期を使用すると、エラーが発生し、同期を再試行する必要がある場合に、 **MSmerge_metadataaction_request** にエントリが作成されます。 その後のマージのアップロードフェーズでは、同期されているパブリケーションに属するすべてのアーティクルに対する要求がこのテーブルから取得され、アップロードされます。 同期が正常に完了すると、 **MSmerge_metadataaction_request** テーブルの対応する行が削除されます。 このテーブルは、パブリッシャー側のパブリケーションデータベースに格納され、サブスクライバー側のサブスクリプションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|パブリッシュされたテーブルのニックネーム。|  
|**rowguid**|**uniqueidentifier**|指定された行の行識別子。|  
|**action**|**tinyint**|必要な補正アクションの識別子。|  
|**generation**|**bigint**|補正アクションが必要なジェネレーションの値。|  
|**後**|**int**|内部使用のみ。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [マージ レプリケーションの Web 同期](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
