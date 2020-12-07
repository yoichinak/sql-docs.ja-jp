---
description: dm_db_missing_index_details (Transact-sql)
title: dm_db_missing_index_details (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_details
- dm_db_missing_index_details
- sys.dm_db_missing_index_details_TSQL
- dm_db_missing_index_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- missing indexes feature [SQL Server], sys.dm_db_missing_index_details dynamic management view
- sys.dm_db_missing_index_details dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f88249c10b9e6c58e1ae68b598cfb92a876bf56a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89518817"
---
# <a name="sysdm_db_missing_index_details-transact-sql"></a>dm_db_missing_index_details (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  空間インデックスを除く、欠落インデックスに関する詳細情報を返します。  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、動的管理ビューは、データベースの包含に影響する情報を公開することも、ユーザーがアクセスできる他のデータベースに関する情報を公開することもできません。 この情報を公開しないように、接続されたテナントに属していないデータを含むすべての行がフィルターで除外されます。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**index_handle**|**int**|特定の欠落インデックスの識別子。 識別子はサーバー全体で一意です。 **index_handle** は、このテーブルのキーです。|  
|**database_id**|**smallint**|欠落インデックスを含むテーブルがあるデータベースの識別子。|  
|**object_id**|**int**|インデックスが欠落しているテーブルの識別子。|  
|**equality_columns**|**nvarchar (4000)**|次の形式の等値述語に使用できる列のコンマ区切り一覧。<br /><br /> *表. 列*  =*constant_value*|  
|**inequality_columns**|**nvarchar (4000)**|次の形式のような不等値述語に使用できる列のコンマ区切り一覧。<br /><br /> *表. 列*  > *constant_value*<br /><br /> "=" 以外の比較演算子はすべて、不等値を表します。|  
|**included_columns**|**nvarchar (4000)**|クエリの包括列として必要な列のコンマ区切り一覧。 カバリング列または付加列の詳細については、「 [付加列を使用したインデックスの作成](../../relational-databases/indexes/create-indexes-with-included-columns.md)」を参照してください。<br /><br /> メモリ最適化インデックス (ハッシュとメモリ最適化された非クラスター化) の場合は、 **included_columns**を無視します。 すべてのメモリ最適化インデックスには、テーブルのすべての列が含まれています。|  
|**statement**|**nvarchar (4000)**|インデックスが欠落しているテーブルの名前。|  
  
## <a name="remarks"></a>解説  
 **sys.dm_db_missing_index_details** によって返される情報は、クエリ オプティマイザーでクエリが最適化されるときに更新されますが、保存されません。 欠落インデックスの情報が保持されるのは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の再起動までです。 欠落インデックスの情報を、サーバーの再利用後も保持する場合は、データベース管理者が情報のバックアップ コピーを定期的に作成する必要があります。  
  
 特定の欠落インデックスが属する欠落インデックス グループを特定するには、**sys.dm_db_missing_index_groups** 動的管理ビューをクエリできます。これには、**index_handle** 列を基準に、このビューを **sys.dm_db_missing_index_details** と等結合します。  

  >[!NOTE]
  >この DMV の結果セットは、600行に制限されています。 各行には、欠落しているインデックスが1つ含まれています。 検出されたインデックスの数が600を超えている場合は、既存の不足しているインデックスに対処して、新しいインデックスを表示できるようにする必要があります。 
  
## <a name="using-missing-index-information-in-create-index-statements"></a>CREATE INDEX ステートメントでの欠落インデックス情報の使用  
 メモリ最適化インデックスとディスクベースインデックスの両方について、 **sys. dm_db_missing_index_details** によって返された情報を CREATE index ステートメントに変換するには、等値列を非等値列の前に配置し、それらを組み合わせてインデックスのキーを作成する必要があります。 付加列は、INCLUDE 句を使用して CREATE INDEX ステートメントに追加します。 等値の列の有効な順序を決定するには、選択度の最も高い列を左の先頭に指定し、選択度が高い順に並べます。  
  
 メモリ最適化インデックスの詳細については、「 [メモリ最適化テーブルのインデックス](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)」を参照してください。  
  
## <a name="transaction-consistency"></a>トランザクションの一貫性  
 トランザクションでテーブルを作成または削除する場合、削除されたオブジェクトに関する欠落インデックス情報を含む行は、トランザクションの一貫性を保持するためこの動的管理オブジェクトから削除されます。  
  
## <a name="permissions"></a>アクセス許可

で [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] は、 `VIEW SERVER STATE` 権限が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium レベルでは、データベースの権限が必要です `VIEW DATABASE STATE` 。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Standard レベルおよび Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="see-also"></a>参照  
 [dm_db_missing_index_columns &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [dm_db_missing_index_groups &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [dm_db_missing_index_group_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
