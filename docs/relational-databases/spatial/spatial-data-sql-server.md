---
description: 空間データ (SQL Server)
title: 空間データ (SQL Server) | Microsoft Docs
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server], spatial storage design
- planar spatial data [SQL Server], designing
- spatial data types [SQL Server]
- geodetic spatial data [SQL Server]
- geometry data type [SQL Server], spatial storage design
- spatial storage [SQL Server]
- geodetic spatial data [SQL Server], designing
ms.assetid: 41a132a1-09e2-4426-b9df-225270cb8e15
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 43ec99d77ea10b33dd06427f97444c995534dba2
ms.sourcegitcommit: 9386ae1b90705a39d37d5541b70c5e8a6564f253
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91662141"
---
# <a name="spatial-data-sql-server"></a>空間データ (SQL Server)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  空間データは、幾何学的オブジェクトの物理的な場所と形状に関する情報を表します。 これらのオブジェクトは、ポイントの場所や、国、道路、湖などのより複雑なオブジェクトである可能性があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **geometry** と **geography** の 2 つの空間データ型がサポートされています。  
  
-   **geometry** 型は、ユークリッド (平面) 座標系のデータを表します。  
  
-   **geography** 型は、球体地球座標系のデータを表します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、どちらのデータ型も .NET 共通言語ランタイム (CLR) のデータ型として実装されています。  
  
##  <a name="related-tasks"></a><a name="reltasks"></a> 関連タスク  
 [geometry インスタンスの作成、構築、およびクエリ](../../relational-databases/spatial/create-construct-and-query-geometry-instances.md)  
 geometry データ型のインスタンスで使用できるメソッドについて説明します。  
  
 [geography インスタンスの作成、構築、およびクエリ](../../relational-databases/spatial/create-construct-and-query-geography-instances.md)  
 geography データ型のインスタンスで使用できるメソッドについて説明します。  
  
 [空間データに対するニアレスト ネイバーのクエリ](../../relational-databases/spatial/query-spatial-data-for-nearest-neighbor.md)  
 特定の空間オブジェクトに最も近い空間オブジェクトを検索するための一般的なクエリ パターンについて説明します。  
  
 [空間インデックスの作成、変更、および削除](../../relational-databases/spatial/create-modify-and-drop-spatial-indexes.md)  
 空間インデックスの作成、変更、および削除に関する情報を提供します。  
  
## <a name="related-content"></a>関連コンテンツ  
 [空間データ型の概要](../../relational-databases/spatial/spatial-data-types-overview.md)  
 空間データ型について説明します。  
  
-   [Point](../../relational-databases/spatial/point.md)  
  
-   [LineString](../../relational-databases/spatial/linestring.md)  
  
-   [CircularString](../../relational-databases/spatial/circularstring.md)  
  
-   [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
  
-   [Polygon](../../relational-databases/spatial/polygon.md)  
  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  
  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
  
-   [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  
  
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)  
 空間インデックス、テセレーション、テセレーション スキームについて説明します。  
  
  
