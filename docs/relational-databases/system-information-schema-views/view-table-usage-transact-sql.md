---
description: VIEW_TABLE_USAGE (Transact-SQL)
title: VIEW_TABLE_USAGE (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- VIEW_TABLE_USAGE_TSQL
- VIEW_TABLE_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.VIEW_TABLE_USAGE view
- VIEW_TABLE_USAGE view
ms.assetid: 0aeefb3f-02ef-457e-8c42-84ddb26f1c88
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4ab6d2bb6b1abff0eb2d6a4d30e29464bf7485f8
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753555"
---
# <a name="view_table_usage-transact-sql"></a>VIEW_TABLE_USAGE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ビューで使用される現在のデータベース内のテーブルごとに 1 行のデータを返します。 この情報スキーマビューでは、現在のユーザーがアクセス許可を持っているオブジェクトに関する情報が返されます。  
  
 これらのビューから情報を取得するには、INFORMATION_SCHEMA の完全修飾名を指定し **ます。**_view_name_。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**VIEW_CATALOG**|**nvarchar (** 128 **)**|ビュー修飾子。|  
|**VIEW_SCHEMA**|**nvarchar (** 128 **)**|ビューを含むスキーマの名前です。<br /><br /> **&#42;&#42; 重要な **  のは、オブジェクトのスキーマを検索する信頼できる方法は、 &#42;&#42;カタログビューに対してクエリを実行することだけです。|  
|**VIEW_NAME**|**sysname**|ビューの名前。|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|テーブル修飾子。|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|ベース テーブルを含むスキーマの名前<br /><br /> **&#42;&#42; 重要な **  のは、オブジェクトのスキーマを検索する信頼できる方法は、 &#42;&#42;カタログビューに対してクエリを実行することだけです。|  
|**TABLE_NAME**|**sysname**|ビューの基になるベース テーブル|  
  
## <a name="see-also"></a>参照  
 [システムビュー &#40;Transact-sql&#41;](../../t-sql/language-reference.md)   
 [情報スキーマビュー &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_dependencies &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-sql-dependencies-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
