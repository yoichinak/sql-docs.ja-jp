---
description: STIsRing (geometry データ型)
title: STIsRing (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsRing_TSQL
- STIsRing (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsRing (geometry Data Type)
ms.assetid: ea0063be-1c74-4cc4-ac6f-b65321ddfa54
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 06702731a47683c44d6096b354c3ec2f773aefaf
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88472494"
---
# <a name="stisring-geometry-data-type"></a>STIsRing (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** インスタンスが次の要件を満たしている場合は 1 を返します。
-   **LineString** インスタンスである。  
-   閉じている。  
-   単純である。  
-   **LineString** インスタンスが要件を満たさない場合は 0 を返します。  

 **geometry** インスタンスを閉じて、単純にする場合、[STIsClosed()](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md) と [STIsSimple()](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md) の両方がインスタンスで呼び出されたときに 1 を返す必要があります。 **geometry** のインスタンスの型を判断するには、[STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md) を使用します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STIsRing ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR の戻り値の型: **SqlBoolean**  
  
## <a name="remarks"></a>注釈  
 インスタンスが **LineString** でない場合、このメソッドは null を返します。  
  
## <a name="examples"></a>例  
 `LineString` インスタンスを作成し、`STIsRing()` を使用して、このインスタンスがリングかどうかをテストする例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0, 0 0)', 0);  
SELECT @g.STIsRing();  
```  
  
## <a name="see-also"></a>参照  
 [STIsClosed &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STGeometryType &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [STIsSimple &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stissimple-geometry-data-type.md)   
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

