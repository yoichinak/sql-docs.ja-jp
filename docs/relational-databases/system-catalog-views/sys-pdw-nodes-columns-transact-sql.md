---
description: sys.pdw_nodes_columns (Transact-sql)
title: sys.pdw_nodes_columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 268c77b7-1d71-4197-a2ed-5e2b2b8fc260
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 8865ca09c1c0aad0da1388a514c522ba89a71e97
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037415"
---
# <a name="syspdw_nodes_columns-transact-sql"></a>sys.pdw_nodes_columns (Transact-sql)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  ユーザー定義テーブルとユーザー定義ビューの列を表示します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|この列が所属するオブジェクトの ID。||  
|name|**sysname**|列の名前です。 オブジェクト内で一意です。||  
|column_id|**int**|列の ID。 オブジェクト内で一意です。||  
|system_type_id|**tinyint**|列のシステム型の ID。||  
|user_type_id|**int**|ユーザーが定義した列の型の ID。||  
|max_length|**smallint**|列の最大長 (バイト単位) です。|サポートされていない列の型には-1 (無効) が含まれています。|  
|精度|**tinyint**|数値ベースの場合は、列の有効桁数です。それ以外の場合は、0 です。||  
|scale|**tinyint**|数値ベースの場合の列の小数点以下桁数それ以外の場合は0です。||  
|collation_name|**sysname**|文字ベースの場合は、列の照合順序の名前です。それ以外の場合は、NULL です。||  
|is_nullable|**bit**|1 = 列で NULL 値を使用できます。||  
|is_ansi_padded|**bit**|1 = 列文字、バイナリ、またはバリアントの場合は、動作に ANSI_PADDING が使用されます。|常に 0 です。|  
|is_rowguidcol|**bit**|1 = 列は宣言された ROWGUIDCOL です。|常に 0 です。|  
|is_identity|**bit**|1 = 列には id 値があります。|常に 0 です。|  
|is_computed|**bit**|1 = 列は計算列です。|常に 0 です。|  
|is_filestream|**bit**|1 = 列は FILESTREAM 列です。|常に 0 です。|  
|is_replicated|**bit**|1 = 列はレプリケートされています。|常に 0 です。|  
|is_non_sql_subscribed|**bit**|1 = 列には、SQL 以外のサブスクライバーがあります。|常に 0 です。|  
|is_merge_published|**bit**|1 = 列はマージパブリッシュされています。|常に 0 です。|  
|is_dts_replicated|**bit**|1 = 列は、SSIS を使用してレプリケートされます。|常に 0 です。|  
|is_xml_document|**bit**|1 = コンテンツは完全な XML ドキュメントです。|常に 0 です。|  
|xml_collection_id|**int**|0 = XML スキーマコレクションがありません。|常に 0 です。|  
|default_object_id|**int**|既定のオブジェクトの ID。0 = 既定値はありません。|常に 0 です。|  
|rule_object_id|**int**|列にバインドされているスタンドアロンルールの ID。 <br />0 = スタンドアロンルールはありません。|常に 0 です。|  
|is_sparse|**bit**|1 = 列はスパース列です。|常に 0 です。|  
|is_column_set|**bit**|1 = 列は列セットです。|常に 0 です。|  
|pdw_node_id|**int**|ノードの一意識別子 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。|NOT NULL|  
  
## <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [Azure Synapse Analytics と Parallel Data Warehouse のカタログ ビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.all_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)  
  
  
