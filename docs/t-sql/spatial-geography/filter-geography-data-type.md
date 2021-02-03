---
description: Filter (geography データ型)
title: Filter (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- Filter
- Filter_TSQL
- Filter (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- Filter method
ms.assetid: 82a8f54a-3a47-4e20-b13a-b148029c5448
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 4d3d5975a0e1d01a0b4dfbea123f483d8e004ab2
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99176313"
---
# <a name="filter-geography-data-type"></a>Filter (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  インデックスが使用可能である場合に、**geography** インスタンスが別の **geography** インスタンスと交差するかどうかを判断する、高速のインデックス専用積集合メソッドを提供するメソッドです。  
  
 **geography** インスタンスがもう一方の **geography** インスタンスと交差している可能性がある場合、1 を返します。 このメソッドは偽陽性の戻り値を生成する場合があり、正確な結果はプランによって異なります。 **geography** インスタンスの交差が見つからない場合は、正確な 0 値 (真陰性の戻り値) を返します。  
  
 インデックスが使用できない場合、または使用されていない場合、このメソッドは、同じパラメーターを使用して呼び出した場合の **STIntersects()** と同じ値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.Filter ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *other_geography*  
 Filter() を呼び出したインスタンスと比較される、別の **geography** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型: **SqlBoolean**  
  
## <a name="remarks"></a>注釈  
 このメソッドは決定的でなく、正確ではありません。  
  
## <a name="examples"></a>例  
 `Filter()` を使用して 2 つの `geography` インスタンスが相互に交差しているかどうかを調べる例を次に示します。  
  
```  
CREATE TABLE sample (id int primary key, g geography);  
INSERT INTO sample VALUES  
   (0, geography::Point(45, -120, 4326)),  
   (1, geography::Point(45, -120.1, 4326)),  
   (2, geography::Point(45, -120.2, 4326)),  
   (3, geography::Point(45, -120.3, 4326)),  
   (4, geography::Point(45, -120.4, 4326));  
  
CREATE SPATIAL INDEX sample_idx on sample(g);  
SELECT id  
FROM sample   
WHERE g.Filter(geography::Parse(  
   'POLYGON((-120.1 44.9, -119.9 44.9, -119.9 45.1, -120.1 45.1, -120.1 44.9))')) = 1;  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [STIntersects &#40;geography データ型&#41;](../../t-sql/spatial-geography/stintersects-geography-data-type.md)  
  
  
