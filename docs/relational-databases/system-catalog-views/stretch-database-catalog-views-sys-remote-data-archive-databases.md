---
title: sys.remote_data_archive_databases (Transact-sql) |Microsoft Docs
description: Stretch が有効なローカルデータベースのデータを格納するリモートデータベースごとに1行のデータを格納 sys.remote_data_archive_databases 方法について説明します。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: reference
f1_keywords:
- sys.remote_data_archive_databases
- sys.remote_data_archive_databases_TSQL
- remote_data_archive_databases
- remote_data_archive_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_databases catalog view
ms.assetid: 25bffb0c-9821-40b4-88cf-75f854891a09
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 8ab3672838849626ea5f72f392ae102d8565b749
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99185013"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_databases"></a>カタログビューの Stretch Database-sys.remote_data_archive_databases
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Stretch が有効なローカルデータベースのデータを格納するリモートデータベースごとに1行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|リモートデータベースの自動生成されたローカル識別子。|  
|**remote_database_name**|**sysname**|リモートデータベースの名前。|  
|**data_source_id**|**int**|リモートサーバーへの接続に使用されるデータソース|  
  
## <a name="see-also"></a>参照  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
