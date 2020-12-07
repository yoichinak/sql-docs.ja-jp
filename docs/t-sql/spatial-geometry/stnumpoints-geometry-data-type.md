---
description: STNumPoints (geometry データ型)
title: STNumPoints (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumPoints_TSQL
- STNumPoints (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints (geometry Data Type)
ms.assetid: a19520fc-7f91-4a2c-856f-4d8b99a7e496
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 60c48dd009ed98e4faf5229f9f005f3bd5fb6ad9
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88467385"
---
# <a name="stnumpoints-geometry-data-type"></a>STNumPoints (geometry データ型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  **geometry** インスタンス内の各図形に含まれる地点の合計数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STNumPoints ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **int**  
  
 CLR の戻り値の型: **SqlInt32**  
  
## <a name="remarks"></a>解説  
 このメソッドは、**geometry** インスタンスの記述に含まれている地点をカウントします。 重複する地点はカウントされます。 このインスタンスが **コレクション** 型の場合、このメソッドは各要素内の地点の合計数を返します。  
  
## <a name="examples"></a>例  
 `LineString` インスタンスを作成し、`STNumPoints()` を使用して、インスタンスの記述で使用されている地点の数を確認する例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STNumPoints();  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
