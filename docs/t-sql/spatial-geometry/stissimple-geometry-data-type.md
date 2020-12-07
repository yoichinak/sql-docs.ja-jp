---
description: STIsSimple (geometry データ型)
title: STIsSimple (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsSimple_TSQL
- STIsSimple (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsSimple (geometry Data Type)
ms.assetid: da8f45d4-4f9c-405d-b883-760eb5344a71
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 51e9f38a40b26ab4ff50c371519ed50e85ae984d
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88472464"
---
# <a name="stissimple-geometry-data-type"></a>STIsSimple (geometry データ型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

**geometry** インスタンスが Open Geospatial Consortium (OGC) で定義されているとおりの単純なものであれば 1 を返します。 **geometry** インスタンスが単純なものでない場合、0 を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STIsSimple ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型: **SqlBoolean**  
  
## <a name="remarks"></a>注釈  
 単純であると見なされるには、**geometry** インスタンスが次の要件をすべて満たしている必要があります。  
  
-   インスタンスの各図形が終点以外で自己交差していてはいけない。  
  
-   インスタンスの 2 つの図形が、両方の図形の境界外部の点で互いに交差していてはいけない。  
  
## <a name="examples"></a>例  
 次は、それ自体と交差する単純ではない `LineString` インスタンスを作成し、`STIsSimple()` を使用して `LineString` が単純かどうかをテストする例です。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 0 2, 2 0)', 0);  
SELECT @g.STIsSimple();  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

