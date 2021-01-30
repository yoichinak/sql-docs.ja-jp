---
description: IHpublishers (Transact-sql)
title: IHpublishers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- IHpublishers
- IHpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishers system table
ms.assetid: 77007246-f10b-4b87-8edf-7afc3c2096af
author: cawrites
ms.author: chadam
ms.openlocfilehash: fd1632e18831779d33b5faa572b179eb1226379b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99201648"
---
# <a name="ihpublishers-transact-sql"></a>IHpublishers (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHpublishers** システムテーブルには、現在のディストリビューターを使用する非 SQL Server パブリッシャーごとに1つの行が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|SQL Server 以外のパブリッシャーを識別します。|  
|**vendor**|**sysname**|SQL&#xA0;Server 以外のデータベースの製造元の名前です。|  
|**publisher_guid**|**uniqueidentifier**|SQL Server 以外のパブリッシャーを識別する GUID。|  
|**flush_request_time**|**datetime**|メタデータキャッシュを更新するためにログリーダーエージェントが必要とした、アーティクルメタデータに対して最後に変更が行われた日時を示します。|  
|**version**|**sysname**|SQL&#xA0;Server 以外のパブリッシャーのバージョンの特徴を表すテキスト文字列です。|  
  
## <a name="see-also"></a>参照  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーションビュー &#40;Transact-sql&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)  
  
  
