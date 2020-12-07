---
description: fulltext_index_fragments (Transact-sql)
title: fulltext_index_fragments (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_index_fragments
- sys.fulltext_index_fragments_TSQL
- fulltext_index_fragments_TSQL
- sys.fulltext_index_fragments
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], fragments
- full-text indexes [SQL Server], metadata
- troubleshooting [SQL Server], full-text search
- sys.fulltext_index_fragments catalog view
ms.assetid: a82e5018-5d88-45c0-9a47-c251e17a6cdb
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 953bf5145712d81acf0ed193719d290cc2397e43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88401368"
---
# <a name="sysfulltext_index_fragments-transact-sql"></a>fulltext_index_fragments (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  フルテキストインデックスでは、 *フルテキストインデックスフラグメント* と呼ばれる内部テーブルを使用して、逆インデックスデータを格納します。 このビューを使用すると、これらのフラグメントに関するメタデータをクエリできます。 このビューは、フルテキスト インデックスが含まれているすべてのテーブルのフルテキスト インデックス フラグメントごとに 1 行のデータを格納しています。  
 
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|table_id|**int**|フルテキスト インデックス フラグメントが含まれているテーブルのオブジェクト ID。|  
|fragment_object_id|**int**|フラグメントに関連付けられている内部テーブルのオブジェクト ID。|  
|fragment_id|**int**|フルテキスト インデックス フラグメントの論理 ID。 テーブルのすべてのフラグメントで一意です。|  
|timestamp|**timestamp**|フラグメントの作成に関連付けられているタイムスタンプ。 新しいフラグメントのタイムスタンプが、古いフラグメントのタイムスタンプよりも大きくなっています。|  
|data_size|**int**|フラグメントの論理サイズ (バイト単位)。|  
|row_count|**int**|フラグメント内の個々の行の数。|  
|status|**int**|フラグメントの状態。次のいずれかになります。<br /><br /> 0 = 新たに作成され、まだ使用されていません。<br /><br /> 1 = フルテキストインデックスの作成時またはマージ時に挿入に使用される<br /><br /> 4 = 閉じています。 クエリの準備完了<br /><br /> 6 = マージ入力のために使用されています。クエリを実行できます。<br /><br /> 8 = 削除用にマークされています。 クエリおよびマージソースには使用されません。<br /><br /> 状態が4または6の場合、フラグメントは論理フルテキストインデックスの一部であるため、クエリを実行できます。つまり、 *クエリ* 可能なフラグメントです。|  
  
## <a name="remarks"></a>解説  
 sys.fulltext_index_fragments カタログ ビューを使用すると、フルテキスト インデックスを構成するフラグメントの数を照会できます。 フルテキスト クエリのパフォーマンスに問題がある場合は、次のように、sys.fulltext_index_fragments を使用してフルテキスト インデックス内のクエリ可能なフラグメント (状態が 4 または 6 のフラグメント) の数を照会します。  
  
```  
SELECT table_id, status FROM sys.fulltext_index_fragments  
   WHERE status=4 OR status=6;  
```  
  
 クエリ可能なフラグメントが多数存在する場合は、フルテキストインデックスを含むフルテキストカタログを再編成してフラグメントをマージすることをお勧めします。 フルテキストカタログのを再構成するには、 [ALTER フルテキストカタログ](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)を使用して再編成*catalog_name*ます。 たとえば、データベース内のという名前のフルテキストカタログを再編成するには、次のように `ftCatalog` `AdventureWorks2012` 入力します。  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT CATALOG ftCatalog REORGANIZE;  
GO  
```  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [フルテキスト インデックスの作成](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
