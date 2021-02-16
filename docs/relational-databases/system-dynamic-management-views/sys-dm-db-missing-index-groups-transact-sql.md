---
description: sys.dm_db_missing_index_groups (Transact-sql)
title: sys.dm_db_missing_index_groups (Transact-sql)
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sys.dm_db_missing_index_groups
- sys.dm_db_missing_index_groups_TSQL
- dm_db_missing_index_groups
- dm_db_missing_index_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_groups dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_groups dynamic management view
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 203e3f190a76299899098cc0cc5a185947ce0428
ms.sourcegitcommit: c6cc0b669b175ae290cf5b08952010661ebd03c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/16/2021
ms.locfileid: "100530831"
---
# <a name="sysdm_db_missing_index_groups-transact-sql"></a>sys.dm_db_missing_index_groups (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  この DMV は、空間インデックスを除く、特定のインデックスグループに欠落しているインデックスに関する情報を返します。 
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、動的管理ビューは、データベースの包含に影響する情報を公開することも、ユーザーがアクセスできる他のデータベースに関する情報を公開することもできません。 この情報を公開しないように、接続されたテナントに属していないデータを含むすべての行がフィルターで除外されます。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**index_group_handle**|**int**|欠落インデックス グループの識別子|  
|**index_handle**|**int**|**index_group_handle** で示されたグループに属する、欠落インデックスの識別子<br /><br /> インデックス グループには、インデックスが 1 つだけ含まれます。|  
  
## <a name="remarks"></a>Remarks  
 **sys.dm_db_missing_index_groups** によって返される情報は、クエリ オプティマイザーでクエリが最適化されるときに更新されますが、保存されません。 欠落インデックスの情報が保持されるのは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の再起動までです。 欠落インデックスの情報を、サーバーの再利用後も保持する場合は、データベース管理者が情報のバックアップ コピーを定期的に作成する必要があります。  
  
 出力結果セットの列はどちらもキーではありませんが、組み合わせるとインデックス キーになります。  

  >[!NOTE]
  >この DMV の結果セットは、600行に制限されています。 各行には、欠落しているインデックスが1つ含まれています。 検出されたインデックスの数が600を超えている場合は、既存の不足しているインデックスに対処して、新しいインデックスを表示できるようにする必要があります。
  
## <a name="permissions"></a>アクセス許可  
 この動的管理ビューをクエリするには、VIEW SERVER STATE 権限、または VIEW SERVER STATE が暗黙的に与えられる権限が許可されている必要があります。  
  
## <a name="see-also"></a>参照  
 [sys.dm_db_missing_index_columns &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
 [sys.dm_db_missing_index_group_stats_query &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-query-transact-sql.md)    