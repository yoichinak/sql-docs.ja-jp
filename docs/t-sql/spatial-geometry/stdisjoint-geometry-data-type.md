---
description: STDisjoint (geometry データ型)
title: STDisjoint (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDisjoint_TSQL
- STDisjoint (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDisjoint (geometry Data Type)
ms.assetid: 90acdb21-e826-4d81-afe8-45a71f33282a
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 43d6372bbe90146004e205d8ac3678196d76712e
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88416898"
---
# <a name="stdisjoint-geometry-data-type"></a>STDisjoint (geometry データ型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  任意の **geometry** インスタンスと別の **geometry** インスタンスが空間的に連結されていない場合、1 を返します。 それ以外の場合は 0 を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STDisjoint ( other_geometry )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *other_geometry*  
 `STDisjoint()` を呼び出したインスタンスと比較される、別の **geometry** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型: **SqlBoolean**  
  
## <a name="remarks"></a>注釈  
 地点のセットの交点が空である場合、2 つの **geography** インスタンスは連結されていません。  
  
 **geometry** インスタンスの SRID (spatial reference ID) が一致しない場合、このメソッドは常に null を返します。  
  
## <a name="examples"></a>例  
 `STDisjoint()` を使用して 2 つの **geometry** インスタンスが空間的に連結されていないかどうかをテストする例を次に示します。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STDisjoint(@h);  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
