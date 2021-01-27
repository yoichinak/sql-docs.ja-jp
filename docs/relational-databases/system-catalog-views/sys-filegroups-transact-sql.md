---
description: sys. ファイルグループ (Transact-sql)
title: sys. ファイルグループ (Transact-sql)
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.filegroups_TSQL
- filegroups
- sys.filegroups
- filegroups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filegroups catalog view
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 887de718575970346d3953fcff1bd996e78840b8
ms.sourcegitcommit: 00be343d0f53fe095a01ea2b9c1ace93cdcae724
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98812978"
---
# <a name="sysfilegroups-transact-sql"></a>sys. ファイルグループ (Transact-sql)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ファイルグループであるデータ領域ごとに1行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|--|このビューが継承する列の一覧については、「 [sys.data_spaces &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)」を参照してください。|  
|**filegroup_guid**|**uniqueidentifier**|ファイルグループの GUID。<br /><br /> NULL = プライマリファイルグループ|  
|**log_filegroup_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この値は NULL です。|  
|**is_read_only**|**bit**|1 = ファイルグループは読み取り専用です。<br /><br /> 0 = ファイル グループは読み取り/書き込み可能です。|  
|**is_autogrow_all_files**|**bit**|[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)].<br /><br /> 1 = ファイルグループ内のファイルが自動拡張のしきい値を満たしている場合、ファイルグループ内のすべてのファイルが拡張されます。<br /><br /> 0 = ファイルグループ内のファイルが自動拡張のしきい値を満たしている場合、そのファイルだけが拡張されます。 既定値です。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [データ領域 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)  
  
