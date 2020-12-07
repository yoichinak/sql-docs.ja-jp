---
description: 空間データ型の概要
title: 空間データ型の概要 | Microsoft Docs
ms.date: 07/21/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], understanding
- geography data type [SQL Server], spatial data
- planar spatial data [SQL Server], geometry data type
- spatial data types [SQL Server]
ms.assetid: 1615db50-69de-4778-8be6-4e058c00ccd4
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a5eca8f5329c6d4727c622c78d7b66000ad50935
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006214"
---
# <a name="spatial-data-types-overview"></a>空間データ型の概要

[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  
空間データには 2 つの型があります。 **geometry** データ型は平面 (ユークリッド (平面地球)) データをサポートしています。 **geometry** データ型 (平面) は、*Open Geospatial Consortium (OGC) Simple Features for SQL Specification* version 1.1.0 および SQL MM (ISO 標準) の両方に準拠しています。
また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**geography** データ型もサポートされています。このデータ型は、GPS の緯度経度座標などの楕円体 (球体地球) データを格納します。

## <a name="spatial-data-objects"></a>空間データ オブジェクト

**geometry** と **geography** の各データ型は、16 種類の空間データ オブジェクト (インスタンス型) をサポートしています。 ただし、"*インスタンス化可能*" なインスタンス型、つまりデータベース内でインスタンスを作成して使用することができる (インスタンス化できる) インスタンス型は、そのうちの 11 種類のみです。 これらのインスタンスによって、親データ型から特定のプロパティが派生されます。

次の図は geometry の階層を表しており、**geometry** と **geography** の各データ型はこれに基づいています。 **geometry** と **geography** のインスタンス化可能な型は青で示されています。  

![geom_hierarchy](../../relational-databases/spatial/media/geom-hierarchy.png)

geography データ型には、インスタンス化可能な型がもう 1 つあります: **FullGlobe**。 **geometry** 型および **geography** 型は、特定のインスタンスが適切な形式のインスタンスである限り、明示的に定義されていない場合でも、そのインスタンスを認識できます。 たとえば、STPointFromText() メソッドを使用して **Point** インスタンスを明示的に定義した場合、そのインスタンスは、メソッドの入力が適切な形式である限り、**geometry** と **geography** によって **Point**として認識されます。 `STGeomFromText()` メソッドを使用して同じインスタンスを定義した場合は、 **geometry** データ型と **geography** データ型の両方で **Point**として認識されます。  

geometry 型および geography 型のサブタイプには、単純型とコレクション型があります。  `STNumCurves()` などのメソッドは、単純型でのみ機能します。  

単純型:

- [Point](../../relational-databases/spatial/point.md)  
- [LineString](../../relational-databases/spatial/linestring.md)  
- [CircularString](../../relational-databases/spatial/circularstring.md)  
- [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
- [Polygon](../../relational-databases/spatial/polygon.md)  
- [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  

コレクション型:

- [MultiPoint](../../relational-databases/spatial/multipoint.md)  
- [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
- [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
- [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  

## <a name="geometry-and-geography-data-type-differences"></a>geometry と geography の各データ型の違い

多くの場合、2 つの空間データの型は同じように動作します。 データの格納方法と操作方法に重要な違いがいくつかあります。  

### <a name="how-connecting-edges-are-defined"></a>接続エッジの定義方法

**LineString** 型と **Polygon** 型の定義データは頂点のみです。 geometry 型の 2 つの頂点間の接続エッジは直線です。 一方、geography 型の 2 つの頂点間の接続エッジは、2 つの頂点を結ぶ短い方の大楕円弧です。 大楕円は、楕円体とその中心を通る平面の交差部分です。 大楕円弧は、大楕円の円弧セグメントです。  

### <a name="how-circular-arc-segments-are-defined"></a>円弧セグメントの定義方法

geometry 型の円弧セグメントは、XY デカルト座標平面上に定義されます (Z 値は無視されます)。 geography 型の円弧セグメントは、参照球の曲線セグメントによって定義されます。 参照球の平行線は、両方の円弧の点に一定の緯度角がある、2 つの補助的な円弧によって定義できます。  

### <a name="measurements-in-spatial-data-types"></a>空間データ型の測定

平面 (平面地球) 座標系では、距離や面積の測定値は座標と同じ測定単位で表されます。 **geometry** データ型を使用した場合、(2, 2) と (5, 6) の間の距離は、使用されている単位に関係なく 5 単位になります。  

楕円体 (球体地球) 座標系では、座標は緯度と経度で表されます。 ただし、長さと面積は、**geography** インスタンスの[空間参照系識別子](./spatial-reference-identifiers-srids.md)によっても異なりますが、通常はメートルと平方メートルで測定されます。 メートルは、 **geography** データ型の最も一般的な測定単位です。  

### <a name="orientation-of-spatial-data"></a>空間データの方向

平面座標系では、ポリゴンのリングの方向は重要ではありません。 *OGC Simple Features for SQL Specification* では、リングの順序は定められていません。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でもリングの順序は強制されません。  

楕円体座標系では、ポリゴンは方向がないと意味がなくなります (あいまいになります)。 たとえば、赤道の周りのリングが北半球を表すのか南半球を表すのかがわからなくなります。 **geography** データ型を使用して空間インスタンスを格納する場合は、リングの方向を指定し、インスタンスの位置を正確に示す必要があります。

楕円体座標系でのポリゴンの内部は、"左手の法則" によって定義されています。geography のポリゴンのリングに沿って歩いていると想像する場合、点が一覧表示されている順序に従って、左側の領域がポリゴンの内部として扱われ、右側の領域がポリゴンの外部として扱われます。

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で互換性レベルが 100 以下である場合、 **geography** データ型には次の制約があります。

- 各 **geography** インスタンスが 1 つの半球に収まる必要があります。 半球よりも大きい空間オブジェクトを格納することはできません。

- Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現または Well-Known Binary (WKB) 表現の **geography** インスタンスでは、半球より大きいオブジェクトが生成される場合に **ArgumentException**がスローされます。  

- 2 つの **geography** インスタンスの入力を必要とする **geography** データ型のメソッド (STIntersection()、STUnion()、STDifference()、STSymDifference() など) では、メソッドの結果が 1 つの半球に収まらない場合に null が返されます。 STBuffer() でも、出力が 1 つの半球に収まらない場合に null が返されます。  

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の **FullGlobe** は、球全体を覆う特殊な多角形です。 領域はありますが、境界や頂点はありません。  

### <a name="outer-and-inner-rings-in-geography-data-type"></a>`geography` データ型の外部および内部のリング

*OGC Simple Features for SQL Specification* では外部リングと内部リングが取り上げられていますが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** データ型ではこの区別はほとんど意味を持ちません。ポリゴンのリングはすべて外部リングと見なすことができます。  

OGC 仕様の詳細については、以下のドキュメントを参照してください。

- [OGC の仕様、簡易機能アクセス Part 1 - 共通アーキテクチャ](https://go.microsoft.com/fwlink/?LinkId=93627)  
- [OGC の仕様、簡易機能アクセス Part 2 - SQL オプション](https://go.microsoft.com/fwlink/?LinkId=93628)  

## <a name="circular-arc-segments"></a>円弧セグメント

円弧セグメントでは、次の 3 つのインスタンス化可能な型を使用できます:**CircularString**、**CompoundCurve**、**CurvePolygon**。  円弧セグメントは、2 次元平面内の 3 つの点によって定義されます。3 番目のポイントを最初のポイントと同じにすることはできません。 円弧セグメントの例をいくつか次に示します。

![circular_arc_segments](../../relational-databases/spatial/media/7e382f76-59da-4b62-80dc-caf93e637c14.gif)

最初の 2 つの例は、一般的な円弧セグメントを示しています。 3 つの点が 1 つの円周上にあることに注意してください。  

他の 2 つの例は、直線セグメントを円弧セグメントとして定義できる方法を示しています。 2 つの点のみによって定義できる通常の直線セグメントとは異なり、円弧セグメントを定義するには 3 つの点が必要です。

円弧型を操作するメソッドは、直線セグメントを使用して大まかな円弧を作成します。大まかな円を作成するために使用される直線セグメントの数は、円弧の長さと曲率によって異なります。Z 値は、円弧セグメントの種類ごとに格納できますが、計算には使用されません。  

> [!NOTE]  
> Z 値が円弧セグメントに指定されている場合、円弧セグメントが入力として許容されるようにするには、円弧セグメント内のすべての点で Z 値が同じである必要があります。 たとえば、 `CIRCULARSTRING(0 0 1, 2 2 1, 4 0 1)` は許容されますが、 `CIRCULARSTRING(0 0 1, 2 2 2, 4 0 1)` は許容されません。  

### <a name="linestring-and-circularstring-comparison"></a>LineString と CircularString の比較

この例は、**LineString** インスタンスと **CircularString** インスタンスの両方を使用して同一の二等辺三角形を格納する方法を示しています。  

```sql
DECLARE @g1 geometry;
DECLARE @g2 geometry;
SET @g1 = geometry::STGeomFromText('LINESTRING(1 1, 5 1, 3 5, 1 1)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(1 1, 3 1, 5 1, 4 3, 3 5, 2 3, 1 1)', 0);
IF @g1.STIsValid() = 1 AND @g2.STIsValid() = 1
  BEGIN
      SELECT @g1.ToString(), @g2.ToString()
      SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length]
  END
```  

**CircularString** インスタンスは、三角形を定義するために 7 つの点が必要であることに注意してください。 **LineString** インスタンスは、三角形を定義するために 4 つの点のみが必要です。 その理由は、 **CircularString** インスタンスは直線セグメントではなく円弧セグメントを格納するためです。 **CircularString** インスタンスに格納されている三角形の辺は ABC、CDE、および EFA です。 **LineString** インスタンスに格納されている三角形の辺は、AC、CE、および EA です。  

次の例を確認してください。  

```sql
SET @g1 = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 4 0)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(0 0, 2 2, 4 0)', 0);
SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length];
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```sql
LS Length    CS Length
5.65685...   6.28318...
```

**CircularString** インスタンスでは **LineString** インスタンスよりも少ない点を使用して、さらに高い精度で曲面境界を格納します。 **CircularString** インスタンスは、たとえば特定の点から半径 20 マイルの検索を行う際など、円形境界を格納する場合に便利です。 **LineString** インスタンスは、四角い都市区画のような直線的な境界を格納する場合に適しています。  

### <a name="linestring-and-compoundcurve-comparison"></a>LineString と CompoundCurve の比較

次のコード例は、 **LineString** インスタンスと **CompoundCurve** インスタンスを使用して同じ図を格納する方法を示します。

```sql
SET @g = geometry::Parse('LINESTRING(2 2, 4 2, 4 4, 2 4, 2 2)');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2), (4 2, 4 4), (4 4, 2 4), (2 4, 2 2))');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2, 4 4, 2 4, 2 2))');
```

上の例では、 **LineString** インスタンスまたは **CompoundCurve** インスタンスで図を格納できます。  次の例では、 **CompoundCurve** を使用して円のスライスを格納します。  

```sql
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(2 2, 1 3, 0 2),(0 2, 1 0, 2 2))');  
```  

**CompoundCurve** インスタンスは円弧セグメント (2 2, 1 3, 0 2) を直接格納できますが、**LineString** インスタンスでは曲線をいくつかの小さな直線セグメントに変換する必要があります。  

### <a name="circularstring-and-compoundcurve-comparison"></a>CircularString と CompoundCurve の比較

次のコード例は、 **CircularString** インスタンスに円のスライスを格納する方法を示します。  

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');
SELECT @g.ToString(), @g.STLength();
```

**CircularString** インスタンスを使用して円のスライスを格納するには、各直線セグメントで 3 つの点を使用する必要があります。 中間点が不明な場合は、中間点を計算するか、次のスニペットで示すように直線セグメントの端点を二重にする必要があります。  

```sql
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 3 6.3246, 3 6.3246, 0 7, -3 6.3246, 0 0, 0 0)');
```

**CompoundCurve** インスタンスは **LineString** コンポーネントおよび **CircularString** コンポーネントを許可して、認識される必要がある点が、円のスライスの直線セグメントの 2 点だけになるようにします。  このコード例は、 **CompoundCurve** を使用して同じ図を格納する方法を示します。

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING( 3 6.3246, 0 7, -3 6.3246), (-3 6.3246, 0 0, 3 6.3246))');
SELECT @g.ToString(), @g.STLength();
```

### <a name="polygon-and-curvepolygon-comparison"></a>Polygon と CurvePolygon の比較

**CurvePolygon** インスタンスは、外部リングと内部リングを定義するときに **CircularString** インスタンスと **CompoundCurve** インスタンスを使用できます。 **Polygon** インスタンスはできません。

## <a name="see-also"></a>関連項目

- [空間データ (SQL Server)](./spatial-data-sql-server.md)
- [geometry データ型メソッド リファレンス](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)
- [geography データ型メソッド リファレンス](../../t-sql/spatial-geography/spatial-types-geography.md)
- [STNumCurves &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)
- [STNumCurves &#40;geography データ型&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)
- [STGeomFromText#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stgeomfromtext-geometry-data-type.md)
- [STGeomFromText #40;geography データ型&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)