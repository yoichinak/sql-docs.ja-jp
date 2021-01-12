---
description: MSrepl_version (Transact-sql)
title: MSrepl_version (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_version
- MSrepl_version_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_version system table
ms.assetid: c1330f03-940b-4564-ac42-6030c6e21173
author: cawrites
ms.author: chadam
ms.openlocfilehash: 2705f8bba91c26bebf886064b795f0f27a78ec2b
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98100576"
---
# <a name="msrepl_version-transact-sql"></a>MSrepl_version (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSrepl_version** テーブルには、現在のバージョンのレプリケーションがインストールされている1つの行が含まれています。 このテーブルは、ディストリビューションデータベースに格納されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**major_version**|**int**|ディストリビューション データベースのメジャー バージョン番号。|  
|**minor_version**|**int**|ディストリビューション データベースのマイナー バージョン番号。|  
|**revision**|**int**|リビジョン番号。|  
|**db_existed**|**bit**|**Sp_adddistributiondb** が呼び出される前に、ディストリビューションデータベースが存在するかどうかを示します。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションテーブル &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
