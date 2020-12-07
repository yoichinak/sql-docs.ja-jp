---
description: STConvexHull (geography データ型)
title: STConvexHull (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STConvexHull method (geography)
ms.assetid: fb435db7-31bb-4243-9d8b-35379184cfb4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0db7ad59585b2ff0c57526ca40f7caa3576e99fc
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88479339"
---
# <a name="stconvexhull-geography-data-type"></a>STConvexHull (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** インスタンスの凸包を表すオブジェクトを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STConvexHull ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型: **SqlGeography**  
  
## <a name="remarks"></a>解説  
 エンベロープの角度が 90°より大きい **geography** インスタンスに対して `FullGlobe` オブジェクトを返します。  
  
 空の **geography** インスタンスに対して空の **geography** コレクションを返します。  
  
 初期化されていない **geography** インスタンスに対して **null** を返します。  
  
## <a name="examples"></a>例  
  
### <a name="a-using-stconvexhull-on-an-uninitialized-geography-instance"></a>A. 初期化されていない geography インスタンスに STConvexHull() を使用する  
 次の例では、初期化されていない **geography** インスタンスに `STConvexHull()` を使用します。  
  
```
 DECLARE @g geography;  
 SELECT @g.STConvexHull();
 ```  
  
### <a name="b-using-stconvexhull-on-an-empty-geography-instance"></a>B. 空の geography インスタンスに STConvexHull を使用する  
 次の例では、空の `Polygon` インスタンスに `STConvexHull()` を使用します。  
  
```
 DECLARE @g geography = 'POLYGON EMPTY';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
### <a name="c-finding-the-convex-hull-of-a-non-convex-polygon-instance"></a>C. 凸のない Polygon インスタンスの凸包を見つける  
 次の例では、`STConvexHull()` を使用して、凸のない `Polygon` インスタンスの凸包を見つけます。  
  
```  
 DECLARE @g geography;  
 SET @g = geography::Parse('POLYGON((-120.533 46.566, -118.283 46.1, -122.3 47.45, -120.533 46.566))');  
 SELECT @g.STConvexHull().ToString();  
```  
  
### <a name="d-finding-the-convex-hull-on-a-geography-instance-with-an-envelope-angle-larger-than-90-degrees"></a>D. エンベロープの角度が 90 度より大きい geography インスタンスで凸包を見つける  
 次の例では、エンベロープの角度が 90 度より大きい **geography** インスタンスで `STConvexHull()` を使用します。  
  
```
 DECLARE @g geography = 'POLYGON((20.533 46.566, -18.283 46.1, -22.3 47.45, 20.533 46.566))';  
 SELECT @g.STConvexHull().ToString();
 ```  
  
  
