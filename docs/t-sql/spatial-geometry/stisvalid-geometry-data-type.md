---
description: STIsValid (geometry データ型)
title: STIsValid (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsValid (geometry Data Type)
- STIsValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid (geometry Data Type)
ms.assetid: 6da39bea-0f67-4660-98fc-d7214f9b2138
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 65e86550626b1461cb8b0abc5e7fb354e6b4e3a4
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88472427"
---
# <a name="stisvalid-geometry-data-type"></a>STIsValid (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Open Geospatial Consortium (OGC) の型に基づいて **geometry** インスタンスが整形式になっている場合は、true を返します。 **geometry** インスタンスが整形式になっていない場合は false を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STIsValid ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型: **SqlBoolean**  
  
## <a name="remarks"></a>注釈  
 **geometry** インスタンスの OGC 型は、[STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md) を呼び出すことによって判別できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、有効な **geometry** インスタンスのみを生成しますが、無効なインスタンスの取得と格納が可能です。 無効なインスタンスと同じ地点のセットを表す有効なインスタンスは、`MakeValid()` メソッドを使用して取得できます。  
  
## <a name="examples"></a>例  
 `geometry` インスタンスを作成し、`STIsValid()` を使用してこのインスタンスが有効かどうかをテストする例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsValid();  
```  
  
## <a name="see-also"></a>参照  
 [STGeometryType &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [MakeValid &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

