---
description: sys.fulltext_index_columns (Transact-SQL)
title: fulltext_index_columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_index_columns
- fulltext_index_columns
- sys.fulltext_index_columns_TSQL
- fulltext_index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], columns
- sys.fulltext_index_columns catalog view
- full-text indexes [SQL Server], properties
ms.assetid: c34b8625-e53c-4281-ace6-d46230d5cb84
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1c1dbd0b4885ef9c1320a505eba17b21b5c8964c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460654"
---
# <a name="sysfulltext_index_columns-transact-sql"></a>sys.fulltext_index_columns (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  フルテキスト インデックスの一部となっている列ごとに 1 行のデータを格納します。    
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|このが含まれているオブジェクトの ID。|  
|**column_id**|**int**|フルテキスト インデックスの一部となっている列の ID。|  
|**type_column_id**|**int**|ユーザーが指定したドキュメントファイル拡張子 (".doc"、".xls" など) を指定された行に格納する型列の ID。 型列は、フルテキスト インデックスの作成中にフィルター選択する必要のあるデータを含む列に対してのみ指定されます。 該当しない場合は NULL です。 詳細については、「 [検索用フィルターの構成と管理](../../relational-databases/search/configure-and-manage-filters-for-search.md)」を参照してください。|  
|**language_id**|**int**|このフルテキスト列にインデックスを作成するために使用されるワードブレーカーの言語の LCID です。<br /><br /> 0 = ニュートラル。<br /><br /> 詳細については、「 [sys. fulltext_languages &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)」を参照してください。|  
|**statistical_semantics**|**int**|1 = この列では、フルテキスト インデックス作成に加えて、統計的セマンティクスが有効になっています。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
