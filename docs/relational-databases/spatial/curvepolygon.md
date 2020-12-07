---
description: CurvePolygon
title: CurvePolygon | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e000a1d8-a049-4542-bfeb-943fd6ab3969
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f117b284799ba4849131254b90a018a397824e7b
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006330"
---
# <a name="curvepolygon"></a>CurvePolygon
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  **CurvePolygon** は、1 つの外部境界リングと 0 個以上の内部リングによって定義された、位相的に閉じた表面です  
  
> [!IMPORTANT]  
> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]CurvePolygon **サブタイプを含む、** で導入された空間機能の詳細な説明とサンプルについては、 [SQL Server 2012 の新しい空間機能](https://go.microsoft.com/fwlink/?LinkId=226407)に関するホワイト ペーパーをダウンロードして参照してください。  
  
 **CurvePolygon** インスタンスの属性を定義する条件を次に示します。  
  
-   **CurvePolygon** インスタンスの境界は、外部リングとすべての内部リングによって定義されます。  
  
-   **CurvePolygon** インスタンスの内部は、外部リングとすべての内部リングとの間にある空間です。  
  
 **CurvePolygon** インスタンスが **Polygon** インスタンスと異なるのは、 **CurvePolygon** インスタンスは円弧 ( **CircularString** および **CompoundCurve**) を含む場合があるという点です。  
  
## <a name="compoundcurve-instances"></a>CompoundCurve インスタンス  
 有効な **CurvePolygon** の図を次に示します。  
  
### <a name="accepted-instances"></a>許容されるインスタンス  
 **CurvePolygon** インスタンスが許容されるためには、空であるか、または許容される円弧リングのみを含んでいる必要があります。 許容される円弧リングは、次の要件を満たしています。  
  
1.  許容される **LineString**、 **CircularString**または **CompoundCurve** インスタンスです。 許容されるインスタンスの詳細については、「 [LineString](../../relational-databases/spatial/linestring.md)」、「 [CircularString](../../relational-databases/spatial/circularstring.md)」、および「 [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)」を参照してください。  
  
2.  4 つ以上の点があること。  
  
3.  始点および終点の X 座標と Y 座標が同じであること。  

    > [!NOTE]  
    > Z 値および M 値は無視されます。  
  
次の例は、許容される **CurvePolygon** インスタンスを示しています。  
  
```sql  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0, 0 0))';  
DECLARE @g3 geometry = 'CURVEPOLYGON((0 0 1, 0 0 2, 0 0 3, 0 0 3))'  
DECLARE @g4 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
DECLARE @g5 geography = 'CURVEPOLYGON((-122.3 47, 122.3 -47, 125.7 -49, 121 -38, -122.3 47))';  
```  
  
`@g3` 始点と終点の Z 値が異なりますが Z 値は無視されるため、許容されます。 `@g5`**geography** 型インスタンスは無効ですが、許容されます。  
  
次の例では、 `System.FormatException`がスローされます。  
  
```sql  
DECLARE @g1 geometry = 'CURVEPOLYGON((0 5, 0 0, 0 0, 0 0))';  
DECLARE @g2 geometry = 'CURVEPOLYGON((0 0, 0 0, 0 0))';  
```  
  
`@g1` 始点と終点の Y 値が同じでないため、許容されません。 `@g2` リングに十分な数の点が含まれていないため、許容されません。  
  
### <a name="valid-instances"></a>有効なインスタンス  
**CurvePolygon** インスタンスを有効にするためには、外部リングと内部リングの両方が次の条件を満たす必要があります。  
  
1.  1 つの接点でのみ接していること。  
2.  互いに交差していないこと。  
3.  それぞれのリングに 4 つ以上の点が含まれていること。  
4.  それぞれのリングは許容される curve 型であること。  
  
さらに、**CurvePolygon** インスタンスは、 **geometry** データ型であるかまたは **geography** データ型であるかに応じて、特定の条件を満たす必要があります。  
  
#### <a name="geometry-data-type"></a>geometry データ型  
有効な **geometryCurvePolygon** インスタンスは、次の属性を持つ必要があります。  
  
1.  すべての内部リングが外部リング内に含まれていること。  
2.  複数の内部リングを含むことはできますが、内部リング内に別の内部リングを含めることはできません。  
3.  リングがそれ自体または別のリングと交差していないこと。  
4.  リングどうしは、1 つの接点でのみ接することができます (リングが接する点の数は有限であることが必要です)。  
5.  多角形の内部が接続されていること。  
  
次の例は、有効な **geometryCurvePolygon** インスタンスを示しています。  
  
```sql  
DECLARE @g1 geometry = 'CURVEPOLYGON EMPTY';  
DECLARE @g2 geometry = 'CURVEPOLYGON(CIRCULARSTRING(1 3, 3 5, 4 7, 7 3, 1 3))';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
CurvePolygon インスタンスには Polygon インスタンスと同じ妥当性規則が適用されますが、例外として、CurvePolygon インスタンスでは新しい円弧型が許容されます。 他の有効または無効なインスタンスの例については、「 [Polygon](../../relational-databases/spatial/polygon.md)」を参照してください。  
  
#### <a name="geography-data-type"></a>geography データ型  
有効な **geographyCurvePolygon** インスタンスは、次の属性を持つ必要があります。  
  
1.  多角形の内部が左辺ルールを使用して接続されている必要があります。  
2.  リングがそれ自体または別のリングと交差していないこと。  
3.  リングどうしは、1 つの接点でのみ接することができます (リングが接する点の数は有限であることが必要です)。  
4.  多角形の内部が接続されていること。  
  
次の例は、有効な geography CurvePolygon インスタンスを示しています。  
  
```sql  
DECLARE @g geography = 'CURVEPOLYGON((-122.3 47, 122.3 47, 125.7 49, 121 38, -122.3 47))';  
SELECT @g.STIsValid();  
```  
  
## <a name="examples"></a>例  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-curvepolygon"></a>A. 空の CurvePolygon を使用して geometry インスタンスをインスタンス化する  
 次の例は、空の **CurvePolygon** インスタンスを作成する方法を示しています。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-with-a-curvepolygon-in-the-same-statement"></a>B. CurvePolygon を同じステートメント内で使用して geometry インスタンスを宣言およびインスタンス化する  
 このコード スニペットは、 **CurvePolygon** を同じステートメント内で使用して geometry インスタンスを宣言およびインスタンス化する方法を示しています。  
  
```sql  
DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))'  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-curvepolygon"></a>C. CurvePolygon を使用して geography インスタンスをインスタンス化する  
 このコード スニペットは、 **geography** を使用して **CurvePolygon**インスタンスを宣言およびインスタンス化する方法を示しています。  
  
```sql  
DECLARE @g geography = 'CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-curvepolygon-with-only-an-exterior-bounding-ring"></a>D. 外部境界リングのみを含む CurvePolygon を格納する  
 この例は、単純な円を **CurvePolygon** インスタンスに格納する方法を示しています (外部境界リングのみを使用して円が定義されています)。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
### <a name="e-storing-a-curvepolygon-containing-interior-rings"></a>E. 内部リングを含む CurvePolygon を格納する  
 この例では、 **CurvePolygon** インスタンス内にドーナツを作成しています (ドーナツは外部境界リングと内部リングの両方を使用して定義されています)。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 4, 4 0, 8 4, 4 8, 0 4), CIRCULARSTRING(2 4, 4 2, 6 4, 4 6, 2 4))');  
SELECT @g.STArea() AS Area;  
```  
  
 次の例は、内部リングを使用した場合の有効な **CurvePolygon** インスタンスと無効なインスタンスの両方を示しています.  
  
```sql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (-2 2, 2 2, 2 -2, -2 -2, -2 2))');  
IF @g1.STIsValid() = 1  
  BEGIN  
     SELECT @g1.STArea();  
  END  
SET @g2 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 5, 5 0, 0 -5, -5 0, 0 5), (0 5, 5 0, 0 -5, -5 0, 0 5))');  
IF @g2.STIsValid() = 1  
  BEGIN  
     SELECT @g2.STArea();  
  END  
SELECT @g1.STIsValid() AS G1, @g2.STIsValid() AS G2;  
```  
  
 `@g1` と `@g2` はどちらも同じ外部境界リング (半径 5 の円) を使用し、内部リングに正方形を使用しています。  しかし、インスタンス `@g1` は有効ですが、インスタンス `@g2` は無効です。 @g2 が無効な理由は、外部リングによって範囲指定された内部空間が内部リングによって 4 つの別個の領域に分割されているためです。 この状況を次の図に示します。  
  
## <a name="see-also"></a>関連項目  
 [Polygon](../../relational-databases/spatial/polygon.md)   
 [CircularString](../../relational-databases/spatial/circularstring.md)   
 [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)   
 [geometry データ型メソッド リファレンス](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md)   
 [geography データ型メソッド リファレンス](../../t-sql/spatial-geography/stequals-geography-data-type.md)   
 [空間データ型の概要](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
