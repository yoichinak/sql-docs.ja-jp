---
description: STLineFromText (geometry データ型)
title: STLineFromText (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLineFromText (geometry Data Type)
- STLineFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromText (geometry Data Type)
ms.assetid: 430508ad-207b-4dee-a4d1-4ddf25e6b4a9
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 77d76ddaeab5952db35f6395d0d2b14a5b904290
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88427044"
---
# <a name="stlinefromtext-geometry-data-type"></a>STLineFromText (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

インスタンスに格納されている Z (標高) 値と M (メジャー) 値で補完された、Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現を基に **geometry** インスタンスを返します。
  
## <a name="syntax"></a>構文  
  
```  
  
STLineFromText ( 'linestring_tagged_text' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *linestring_tagged_text*  
 返される **geometryLineString** インスタンスの WKT 表現です。 *linestring_tagged_text* は **nvarchar(max)** 式です。  
  
 *SRID*  
 返される **geometryLineString** インスタンスの SRID (spatial reference ID) を表す **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR 戻り値の型: **SqlGeometry**  
  
 OGC の型: **LineString**  
  
## <a name="remarks"></a>注釈  
このメソッドでは、入力が整形式でない場合に、**FormatException** がスローされます。 SQL 仕様バージョン 1.2.1 の Open Geospatial Consortium (OGC) Simple Features の 3 次元ジオメトリと測定ジオメトリの WKT 表記はサポートされていません。 Z (標高) 値と M (メジャー) 値のサポートされている表現の例を参照してください。
  
## <a name="examples"></a>例  
 `STLineFromText()` を使用して `geometry` インスタンスを作成する例を次に示します。

### <a name="example-1-two-dimension-geometry-wkt"></a>例 1:2 次元ジオメトリ WKT
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100, 200 200)', 0);  
SELECT @g.ToString();  
```  
  
### <a name="example-2-three-dimension-geometry-wkt"></a>例 2:3 次元ジオメトリ WKT
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 100, 200 200 200)', 0);  
SELECT @g.ToString();  
``` 

### <a name="example-3-two-dimension-measured-geometry-wkt"></a>例 3: 2 次元測定ジオメトリ WKT
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 NULL 100, 200 200 NULL 200)', 0);  
SELECT @g.ToString();  
``` 

### <a name="example-4-three-dimension-measured-geometry-wkt"></a>例 4: 3 次元測定ジオメトリ WKT
```  
DECLARE @g geometry;  
SET @g = geometry::STLineFromText('LINESTRING (100 100 100 100, 200 200 200 200)', 0);  
SELECT @g.ToString();  
``` 
## <a name="see-also"></a>参照  
 [OGC の静的なジオメトリ メソッド](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

