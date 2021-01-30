---
description: MSpublication_access (Transact-sql)
title: MSpublication_access (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- MSpublication_access_TSQL
- MSpublication_access
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublication_access system table
ms.assetid: 7bebe47e-3153-4579-8092-5723667a24c6
author: cawrites
ms.author: chadam
ms.openlocfilehash: f0ed7d178deb2ac4eae5089e6e7aad92bc8661d7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99191182"
---
# <a name="mspublication_access-transact-sql"></a>MSpublication_access (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSpublication_access** テーブルには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定のパブリケーションまたはパブリッシャーへのアクセス権を持つログインごとに1行の値が格納されます。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**publication_id**|**int**|パブリケーションの ID です。|  
|**ログイン (login)**|**sysname**|パブリッシャーとディストリビューターの両方に存在する [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows アカウントです。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
