---
description: STNumGeometries (geography データ型)
title: STNumGeometries (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- STNumGeometries (geography Data Type)
- STNumGeometries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumGeometries method
ms.assetid: 6ae7fac2-62f1-420f-9fc9-a09606be9605
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 21dfb949f48d8717062cc2df6abb7ac3d30c7d23
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99202118"
---
# <a name="stnumgeometries-geography-data-type"></a>STNumGeometries (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** インスタンスを構成する **ジオメトリ** の数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STNumGeometries ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **int**  
  
 CLR の戻り値の型: **SqlInt32**  
  
## <a name="remarks"></a>解説  
 このメソッドは、**geography** インスタンスが **MultiPoint**、**MultiLineString**、**MultiPolygon**、**GeometryCollection** インスタンスではない場合に 1 を返し、**geography** インスタンスが空の場合に 0 を返します。  
  
## <a name="examples"></a>例  
 `MultiPoint` インスタンスを作成し、`STNumGeometries()` を使用して **ジオメトリ** の数を確認する例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT((-122.360 47.656), (-122.343 47.656))', 4326);  
SELECT @g.STNumGeometries();  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
