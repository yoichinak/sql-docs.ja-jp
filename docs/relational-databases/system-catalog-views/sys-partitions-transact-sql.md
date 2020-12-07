---
description: sys.partitions (Transact-SQL)
title: sys. partition (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- partitions
- partitions_TSQL
- sys.partitions_TSQL
- sys.partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partitions catalog view
ms.assetid: 1c19e1b1-c925-4dad-a652-581692f4ab5e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0947a58b607d781b05eb5633b0664d7f0da4d107
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546753"
---
# <a name="syspartitions-transact-sql"></a>sys.partitions (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  データベース内のすべてのテーブルとほとんどの種類のインデックスのパーティションごとに 1 行のデータを保持します。 フルテキスト、空間、XML などの特殊なインデックスの種類は、このビューには含まれていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルとインデックスは、明示的にパーティション分割されているかどうかに関係なく、1 つ以上のパーティションが保持されているものと見なされます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|パーティション ID を示します。 データベース内で一意です。|  
|object_id|**int**|このパーティションが所属するオブジェクトの ID を示します。 すべてのテーブルまたはビューは、少なくとも1つのパーティションで構成されます。|  
|index_id|**int**|このパーティションが所属するオブジェクト内のインデックスの ID を示します。<br /><br /> 0 = ヒープ<br />1 = クラスター化インデックス<br />2以上 = 非クラスター化インデックス|  
|partition_number|**int**|所有しているインデックスまたはヒープ内で 1 から始まるパーティション番号です。 パーティション分割されていないテーブルとインデックスの場合、この列の値は1です。|  
|hobt_id|**bigint**|このパーティションの行を含むデータヒープまたは B ツリー (HoBT) の ID を示します。|  
|rows|**bigint**|このパーティション内の行の概数を示します。|  
|filestream_filegroup_id|**smallint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> このパーティションに格納されている FILESTREAM ファイルグループの ID を示します。|  
|data_compression|**tinyint**|各パーティションの圧縮の状態を示します。<br /><br /> 0 = NONE <br />1 = 行 <br />2 = ページ <br />3 = 列ストア: 以降**に適用さ**れます。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]<br />4 = COLUMNSTORE_ARCHIVE:**以降に適用さ**れます。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]<br /><br /> **注:** フルテキストインデックスは、のどのエディションでも圧縮され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|data_compression_desc|**nvarchar(60)**|各パーティションの圧縮の状態を示します。 行ストア テーブルに指定できる値は、NONE、ROW、および PAGE です。 列ストアテーブルに指定できる値は、列ストアと COLUMNSTORE_ARCHIVE です。|  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
