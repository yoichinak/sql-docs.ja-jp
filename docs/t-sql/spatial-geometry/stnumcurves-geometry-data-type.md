---
description: STNumCurves (geometry データ型)
title: STNumCurves (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geometry)
ms.assetid: 20c2fa0b-656b-4519-b34c-cc8f094290d4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: fe3418284131577051e48f8300bd89df2abc0ec1
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88444966"
---
# <a name="stnumcurves-geometry-data-type"></a>STNumCurves (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

このメソッドは、**geometry** インスタンスが 1 次元の空間データ型の場合に、そこに含まれる曲線の数を返します。 1 次元の空間データ型には、**LineString**、**CircularString**、**CompoundCurve** があります。 `STNumCurves`() は単純型に対してのみ機能し、**MultiLineString** のような **geometry** コレクションでは機能しません。
  
## <a name="syntax"></a>構文  
  
```  
  
.STNumCurves()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR 戻り値の型: **SqlGeometry**  
  
## <a name="remarks"></a>解説  
 空の 1 次元 **geometry** インスタンスは 0 を返します。 **geometry** インスタンスが 1 次元のインスタンスではない場合や初期化されていない場合は、**NULL** が返されます。  
  
## <a name="examples"></a>例  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. CircularString インスタンスに対して STNumCurves() を使用する  
 次の例では、`CircularString` インスタンスに含まれる曲線の数を取得する方法を示します。  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. CompoundCurve インスタンスに対して STNumCurves() を使用する  
 次の例では、`STNumCurves()` を使用して、`CompoundCurve` インスタンスに含まれる曲線の数を返します。  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>参照  
 [空間データ型の概要](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

