---
description: external_tables (Transact-sql)
title: external_tables (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: fac4720c-b679-4ab2-864b-ff7810a9b559
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9ba3034b4cdda575f19ec436725afd4c0f43451f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550533"
---
# <a name="sysexternal_tables-transact-sql"></a>external_tables (Transact-sql)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

  現在のデータベース内の外部テーブルごとに1行のデータを格納します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|\<inherited columns>||このビューが継承する列の一覧については、「 [sys. objects &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。||  
|max_column_id_used|**int**|このテーブルで使用される最大列 ID。||  
|uses_ansi_nulls|**bit**|テーブルは、SET ANSI_NULLS データベース オプションが ON の場合に作成されます。||  
|data_source_id|**int**|外部データソースのオブジェクト ID。||  
|file_format_id|**int**|HADOOP 外部データソースの外部テーブルの場合、これは外部ファイル形式のオブジェクト ID です。||  
|location|**nvarchar (4000)**|HADOOP 外部データソースの外部テーブルの場合、これは HDFS 内の外部データのパスになります。||  
|reject_type|**tinyint**|HADOOP 外部データソースに対する外部テーブルの場合、外部データを照会するときに、拒否された行がカウントされます。|VALUE-拒否された行の数。<br /><br /> パーセント-拒否された行の割合。|  
|reject_value|**float**|HADOOP 外部データソースに対する外部テーブルの場合:<br /><br /> *Reject_type =* value の場合、これは、クエリが失敗するまでに許可する行の拒否の回数です。<br /><br /> *Reject_type* = 割合の場合は、クエリが失敗するまでに許可する行の拒否の比率です。||  
|reject_sample_value|**int**|*Reject_type* = 割合の場合、これは、拒否された行の割合を計算する前に、正常に (または失敗した) 読み込まれる行の数です。|Reject_type = VALUE の場合は NULL です。|  
|distribution_type|**int**|外部テーブルの SHARD_MAP_MANAGER 外部データソースは、基になるベーステーブルにまたがる行のデータ分散です。|0-シャード化<br /><br /> 1-レプリケート済み<br /><br /> 2-ラウンドロビン|  
|distribution_desc|**nvarchar(120)**|外部テーブルの SHARD_MAP_MANAGER 外部データソースは、文字列として表示される分布の種類です。||  
|sharding_column_id|**int**|外部テーブルの SHARD_MAP_MANAGER 外部データソースとシャード化分布の場合、これはシャーディングキー値を含む列の列 ID です。||  
|remote_schema_name|**sysname**|外部テーブルが SHARD_MAP_MANAGER 外部データソースである場合、これはベーステーブルがリモートデータベースに配置されているスキーマです (外部テーブルが定義されているスキーマとは異なる場合)。||  
|remote_object_name|**sysname**|外部テーブルの SHARD_MAP_MANAGER 外部データソースは、リモートデータベース上のベーステーブルの名前です (外部テーブルの名前と異なる場合)。||  
  
## <a name="permissions"></a>アクセス許可  
 カタログ ビューでのメタデータの表示が、ユーザーが所有しているかそのユーザーが権限を許可されている、セキュリティ保護可能なメタデータに制限されます。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [external_file_formats &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [external_data_sources &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
