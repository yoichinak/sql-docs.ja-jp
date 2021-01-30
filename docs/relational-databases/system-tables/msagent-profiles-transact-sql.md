---
description: MSagent_profiles (Transact-sql)
title: MSagent_profiles (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSagent_profiles
- MSagent_profiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSagent_profiles system table
ms.assetid: 4ab1b2ae-b6d9-42b7-9b31-98547dbb7f99
author: cawrites
ms.author: chadam
ms.openlocfilehash: 1ac49f809e023dfe08d289f746197f23d181c0a1
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99160516"
---
# <a name="msagent_profiles-transact-sql"></a>MSagent_profiles (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSagent_profiles** テーブルには、定義されているレプリケーションエージェントプロファイルごとに1つの行が含まれています。 このテーブルは、 **msdb** データベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**profile_id**|**int**|プロファイル ID。|  
|**profile_name**|**sysname**|エージェントの種類に固有のプロファイル名です。|  
|**agent_type**|**int**|エージェントの種類。<br /><br /> **1** = スナップショットエージェント<br /><br /> **2** = ログリーダーエージェント<br /><br /> **3** = ディストリビューションエージェント<br /><br /> **4** = マージエージェント<br /><br /> **9** = キューリーダーエージェント|  
|**type**|**int**|プロファイルの種類です。<br /><br /> **0** = システム **1** = カスタム|  
|**description**|**nvarchar (3000)**|プロファイルの説明。|  
|**def_profile**|**bit**|このプロファイルがこの種類のエージェントの既定のプロファイルかどうかを指定します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
