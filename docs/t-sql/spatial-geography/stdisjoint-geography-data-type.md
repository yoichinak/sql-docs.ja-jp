---
description: STDisjoint (geography データ型)
title: STDisjoint (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- STDisjoint (geography Data Type)
- STDisjoint_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STDisjoint
ms.assetid: 98328a02-e018-47d6-aa93-de162b8aef62
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 96cde2c956d745ab27c64118874c033b76670959
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99157325"
---
# <a name="stdisjoint-geography-data-type"></a>STDisjoint (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  任意の **geography** インスタンスと別の **geography** インスタンスが空間的に連結されていない場合、1 を返します。 それ以外の場合は 0 を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STDisjoint ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *other_geography*  
 STDisjoint() を呼び出したインスタンスと比較される、別の **geography** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型: **SqlBoolean**  
  
## <a name="remarks"></a>注釈  
 比較する 2 つのインスタンスに含まれる地点のセットの交点が空である場合、これらの **geography** インスタンスは連結されていません。  
  
 2 つの **geography** インスタンスの SRID (spatial reference ID) が一致しない場合、このメソッドは常に null を返します。  
  
## <a name="examples"></a>例  
 `STDisjoint()` を使用して、2 つの `geography` インスタンスが空間的に連結されていないかどうかをテストする例を次に示します。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDisjoint(@h);  
```  
  
## <a name="see-also"></a>参照  
 [geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
