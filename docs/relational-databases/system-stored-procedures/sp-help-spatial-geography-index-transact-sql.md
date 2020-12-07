---
description: sp_help_spatial_geography_index (Transact-sql)
title: sp_help_spatial_geography_index (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_index
- sp_help_spatial_geography_index_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_index procedure
ms.assetid: c9bf5675-eafc-4d71-bfdb-da963384fa0c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b2b519fd8e52af2a67c37941a4868622aa254599
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810348"
---
# <a name="sp_help_spatial_geography_index-transact-sql"></a>sp_help_spatial_geography_index (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Geography**空間インデックスに関する指定された一連のプロパティの名前と値を返します。 結果はテーブル形式で返されます。 プロパティのコアセットとインデックスのすべてのプロパティのどちらを返すかを選択できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_help_spatial_geography_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput' ]   
     [ , [ @query_sample = ] 'query_sample' ]   
```  
  
## <a name="arguments"></a>引数  
 「 [空間インデックスストアドプロシージャの引数とプロパティ」を](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)参照してください。  
  
## <a name="properties"></a>Properties  
 「 [空間インデックスストアドプロシージャの引数とプロパティ」を](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 プロシージャにアクセスするには、ユーザーに PUBLIC ロールが割り当てられている必要があります。 サーバーとオブジェクトに対する読み取りアクセス権限が必要です。  
  
## <a name="remarks"></a>解説  
  
## <a name="example"></a>例  
 次の例では、を使用して `sp_help_spatial_geography_index` 、 ** \@ **テーブル**geography_col**で定義されている、指定されたクエリサンプルのテーブルの**SIndx_SpatialTable_geography_col2**を調査します。 **geography** この例では、指定したインデックスのコアプロパティのみが返されます。  
  
```  
declare @qs geography  
        ='POLYGON((-90.0 -180, -90 180.0, 90 180.0, 90 -180, -90 -180.0))';  
exec sp_help_spatial_geography_index 'geography_col', 'SIndx_SpatialTable_geography_col2', 0, @qs;  
```  
  
 **Geography**インスタンスの境界ボックスは、地球全体です。  
  
## <a name="requirements"></a>必要条件  
  
## <a name="see-also"></a>参照  
 [空間インデックスストアドプロシージャ](./spatial-index-stored-procedures-arguments-and-properties.md)   
 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)   
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [空間データ &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
