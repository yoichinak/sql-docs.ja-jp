---
description: MSpeer_lsns (Transact-SQL)
title: MSpeer_lsns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSpeer_lsns
- MSpeer_lsns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_lsns system table
ms.assetid: 0ba33907-601b-4c3d-8099-2663f680a161
author: cawrites
ms.author: chadam
ms.openlocfilehash: 8316d023cb030e2eba09aff82d4e941cf551d1a5
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99205855"
---
# <a name="mspeer_lsns-transact-sql"></a>MSpeer_lsns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Mspeer_lsns** テーブルは、ピアツーピアレプリケーショントポロジ内の各トランザクションをサブスクリプションにマップするために使用されます。 このテーブルは、ピアツーピアレプリケーショントポロジ内のすべてのパブリケーションデータベースと、ピアツーピアパブリケーションのすべてのサブスクライバーのサブスクリプションデータベースに格納されます。 この種類のトランザクションレプリケーショントポロジの詳細については、「 [ピアツーピアトランザクションレプリケーション](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)」を参照してください。 このテーブルは、パブリケーションデータベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ピアツーピア LSN を識別します。|  
|**last_updated**|**datetime**|最後の行の更新が行われた **日時** 。|  
|**送信者**|**sysname**|トランザクションを開始したパブリッシャーの名前。|  
|**originator_db**|**sysname**|トランザクションが発生したデータベースの名前。|  
|**originator_publication**|**sysname**|トランザクションが発生したパブリケーションの名前。|  
|**originator_publication_id**|**int**|トランザクションが発生したパブリケーションの識別子。|  
|**originator_db_version**|**int**|発信元のデータベースのバージョン番号識別子。|  
|**originator_lsn**|**int**|元のパブリケーションの LSN を識別します。|  
|**originator_version**|**int**|パブリッシャーのバージョン番号を識別します。|  
|**originator_id**|**smallint**|競合検出のためにトポロジの各ノードを識別します。 詳細については、「 [ピア ツー ピア レプリケーションにおける競合検出](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
