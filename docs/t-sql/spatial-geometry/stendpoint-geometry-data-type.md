---
description: STEndpoint (geometry データ型)
title: STEndpoint (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STEndpoint (geometry Data Type)
- STEndpoint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STEndpoint (geometry Data Type)
ms.assetid: 61773c45-b568-4e0c-94da-1310c42de7f5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1ec856db5c9f528135393bdb968ac35de4e94f2e
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88497025"
---
# <a name="stendpoint-geometry-data-type"></a>STEndpoint (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** インスタンスの終点を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STEndPoint ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR 戻り値の型: **SqlGeometry**  
  
 Open Geospatial Consortium (OGC) の型: **Point**  
  
## <a name="remarks"></a>解説  
 `STEndPoint()` は、[STPointN](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md) (x.NumPoints()) と同じです。  
  
 このメソッドは、空の **geometry** インスタンスに対して呼び出された場合は null を返します。  
  
## <a name="examples"></a>例  
 `STGeomFromText()` で `LineString` インスタンスを作成し、`STEndpoint()` を使用して、`LineString` の終点を取得する例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STEndPoint().ToString();  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

