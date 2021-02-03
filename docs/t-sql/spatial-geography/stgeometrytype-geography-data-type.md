---
description: STGeometryType (geography データ型)
title: STGeometryType (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- STGeometryType (geography Data Type)
- STGeometryType_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryType method
ms.assetid: 3e169ead-a98e-44af-8d33-fd59a955cae4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1d88e3d81160ce431b695e0271eb4222b6a159aa
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99211263"
---
# <a name="stgeometrytype-geography-data-type"></a>STGeometryType (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** インスタンスで表される Open Geospatial Consortium (OGC) の型名を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STGeometryType ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **nvarchar(4000)**  
  
 CLR の戻り値の型: **SqlString**  
  
## <a name="remarks"></a>注釈  
 `STGeometryType()` によって返される OGC の型名は、**Point**、**LineString**、**CircularString**、**CompoundCurve**、**Polygon**、**CurvePolygon**、**GeometryCollection**、**MultiPoint**、**MultiLineString**、**MultiPolygon** および **FullGlobe** です。  
  
## <a name="examples"></a>例  
 `Polygon` インスタンスを作成し、`STGeometryType()` を使用してこれが多角形であることを確認する例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STGeometryType();  
```  
  
## <a name="see-also"></a>関連項目  
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
