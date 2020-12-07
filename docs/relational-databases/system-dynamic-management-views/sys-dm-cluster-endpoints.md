---
description: dm_cluster_endpoints (Transact-sql)
title: dm_cluster_endpoints (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, big-data-clusters
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_cluster_endpoints
- dm_cluster_endpoints_TSQL
- dm_cluster_endpoints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cluster_endpoints dynamic management view
ms.assetid: ''
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 7df88a6be24e5378a8bd588514c9806e8258eb0e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542340"
---
# <a name="sysdm_cluster_endpoints-transact-sql"></a>dm_cluster_endpoints (Transact-sql)
[!INCLUDE[sqlserver2019](../../includes/applies-to-version/sqlserver2019.md)]

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|name|`sysname`|SQL ビッグデータクラスターで外部に公開されるサービスの名前。 エンドポイントの一意の識別子。 このビューのキー。 NULL 値は許可されません。 |  
|description|`nvarchar(4000)`|サービスの説明。 NULL 値は許可されません。 |
|endpoint|`sysname`|エンドポイント url または接続属性。 NULL 値は許可されません。 |
|protocol_desc|`sysname`|エンドポイントプロトコルの説明 |

## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。

## <a name="see-also"></a>参照

[概要 [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ss-nover.md)] ](../../big-data-cluster/big-data-cluster-overview.md)
