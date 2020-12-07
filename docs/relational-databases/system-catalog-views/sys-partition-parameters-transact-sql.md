---
description: sys.partition_parameters (Transact-SQL)
title: partition_parameters (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- partition_parameters_TSQL
- partition_parameters
- sys.partition_parameters_TSQL
- sys.partition_parameters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.partition_parameters catalog view
ms.assetid: 2012ed9d-3ea3-4c29-9b78-dfa54a392dce
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4d0231c80c4c122703bd3ede4315e13362e49c34
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542526"
---
# <a name="syspartition_parameters-transact-sql"></a>sys.partition_parameters (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  パーティション関数の各パラメーターの行を保持します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**function_id**|**int**|このパラメーターが属するパーティション関数の ID です。|  
|**parameter_id**|**int**|パラメーターの ID。 パーティション関数内で一意であり、1から始まります。|  
|**system_type_id**|**tinyint**|パラメーターのシステム型の ID。 は、 **system_type_id** 列に対応してい **ます。型** のカタログビューです。|  
|**max_length**|**smallint**|パラメーターの最大長 (バイト単位)。|  
|**有効桁数 (precision)**|**tinyint**|数値ベースの場合のパラメーターの有効桁数。それ以外の場合は0です。|  
|**scale**|**tinyint**|数値ベースの場合はパラメーターの小数点以下桁数。それ以外の場合は0です。|  
|**collation_name**|**sysname**|文字ベースの場合は、パラメーターの照合順序の名前。それ以外の場合は NULL。|  
|**user_type_id**|**int**|型の ID です。 データベース内で一意です。 システムデータ型の場合は、 **user_type_id**  =  **system_type_id**ます。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [パーティション関数のカタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.partition_functions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-functions-transact-sql.md)   
 [sys.partition_range_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-range-values-transact-sql.md)  
  
  
