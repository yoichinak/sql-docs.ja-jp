---
description: sys. ファイルグループ (Transact-sql)
title: sys. ファイルグループ (Transact-sql) |Microsoft Docs
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
ms.assetid: 9e851f72-1f8e-4515-a25d-152ebc12ed56
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 62748ef76c35378aa985a1624a23bd3f7e77676f
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809358"
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
|**is_autogrow_all_files**|**bit**|**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] から [現在のバージョン](../../sql-server/what-s-new-in-sql-server-2016.md)まで)。<br /><br /> 1 = ファイルグループ内のファイルが自動拡張のしきい値を満たしている場合、ファイルグループ内のすべてのファイルが拡張されます。<br /><br /> 0 = ファイルグループ内のファイルが自動拡張のしきい値を満たしている場合、そのファイルだけが拡張されます。 既定値です。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [データ領域 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)  
  
