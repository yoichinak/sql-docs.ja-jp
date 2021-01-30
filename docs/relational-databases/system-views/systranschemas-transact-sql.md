---
description: systranschemas (Transact-SQL)
title: systranschemas (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- systranschemas
- systranschemas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- systranschemas system table
ms.assetid: 864c3966-cb61-4f2b-8939-ccda112de853
author: stevestein
ms.author: sstein
ms.openlocfilehash: 78242bbe5df333aa23dfd2b8c22688ef5e2e6284
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99181538"
---
# <a name="systranschemas-transact-sql"></a>systranschemas (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Systranschemas** テーブルは、トランザクションパブリケーションおよびスナップショットパブリケーションでパブリッシュされたアーティクルのスキーマ変更を追跡するために使用されます。 このテーブルは、publication データベースと subscription データベースの両方に保存されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**tabid**|**int**|スキーマ変更が発生したテーブルアーティクルを識別します。|  
|**startlsn**|**[バイナリ]**|スキーマ変更開始時の LSN 値です。|  
|**endlsn**|**[バイナリ]**|スキーマ変更の最後にある LSN 値。|  
|**typeid**|**int**|スキーマ変更のタイプです。|  
  
## <a name="see-also"></a>参照  
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
