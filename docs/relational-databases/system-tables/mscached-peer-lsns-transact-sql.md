---
description: MScached_peer_lsns (Transact-sql)
title: MScached_peer_lsns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MScached_peer_lsns_TSQL
- MScached_peer_lsns
dev_langs:
- TSQL
helpviewer_keywords:
- MScached_peer_lsns system table
ms.assetid: f8b6089a-0230-45f9-8c34-9fe0d2a3a74e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 23d4339d7a907cd755934df4803e38f5ba769b5e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551014"
---
# <a name="mscached_peer_lsns-transact-sql"></a>MScached_peer_lsns (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MScached_peer_lsns**テーブルは、ピアツーピアレプリケーションで特定のサブスクライバーに返すコマンドを決定するために使用される、トランザクションログの LSN 値を追跡するために使用されます。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
## <a name="definition"></a>定義  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**agent_id**|**int**|ディストリビューションエージェントの ID。|  
|**送信者**|**sysname**|発信元のパブリッシャーの名前。|  
|**originator_db**|**sysname**|元のパブリケーションデータベースの名前。|  
|**originator_publication_id**|**int**|発信元のパブリケーションを識別します。|  
|**originator_db_version**|**int**|発信元のデータベースのバージョン番号識別子。|  
|**originator_lsn**|**varbinary(16)**|発信元のトランザクションの LSN。|  
  
## <a name="remarks"></a>解説  
 LSN 値は挿入直後にのみ使用され、システムでは永続的な意味を持ちません。  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
