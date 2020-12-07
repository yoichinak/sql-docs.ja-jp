---
description: table_types (Transact-sql)
title: table_types (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- table_types_TSQL
- sys.table_types
- sys.table_types_TSQL
- table_types
dev_langs:
- TSQL
helpviewer_keywords:
- table types [SQL Server]
- table-valued parameters, sys.table_types
- sys.table_types
- UDTT
ms.assetid: c05fd873-aff2-4a89-9936-a54c2ea09996
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dd8ea2fe8960115b5ef638490a38291ed9cdd559
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548666"
---
# <a name="systable_types-transact-sql"></a>table_types (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  ユーザー定義テーブル型のプロパティを表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 テーブル型は、テーブル変数またはテーブル値パラメーターを宣言できる型です。 各テーブル型には、 [sys. objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)カタログビューの外部キーである**type_table_object_id**があります。 この ID 列を使用すると、通常のテーブルの **object_id** 列に似た方法でさまざまなカタログビューに対してクエリを実行し、列や制約などのテーブル型の構造を検出することができます。    
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|*\<inherited columns>*||このビューが継承する列の一覧については、「 [sys &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)」を参照してください。|  
|**type_table_object_id**|**int**|オブジェクト ID 番号。 この数値は、データベース内で一意です。|  
|**is_memory_optimized**|**bit**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。<br /><br /> 使用できる値を次に示します。<br /><br /> 0 = メモリ最適化ではありません<br /><br /> 1 = メモリ最適化済み<br /><br /> 値 0 が既定の値です。<br /><br /> テーブル型は、常に DURABILITY = SCHEMA_ONLY で作成されます。 スキーマはディスクにのみ保存されます。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [テーブル値パラメーターを使用する &#40;データベースエンジン&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
