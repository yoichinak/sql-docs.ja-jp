---
description: InstanceOf (geography データ型)
title: InstanceOf (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 384539d8978dd8ae169ae5cfb2b7b5abcf394686
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88422386"
---
# <a name="instanceof-geography-data-type"></a>InstanceOf (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geography** インスタンスが、指定した型と同じであるかどうかをテストします。  
  
## <a name="syntax"></a>構文  
  
```sql  
  
.InstanceOf ( 'geography_type')  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
*geography_type*  
**geography** 型の階層で公開されている 16 種類の型のうちの 1 つを指定する **nvarchar(4000)** 文字列です。  
  
## <a name="return-types"></a>戻り値の型  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
CLR の戻り値の型: **SqlBoolean**  
  
## <a name="remarks"></a>注釈  
**geography** インスタンスの型が指定した型と同じである場合、または指定した型がインスタンスの型の先祖である場合は 1 を返します。それ以外の場合は 0 を返します。  
  
この **geography** データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
メソッドの入力内容は、次のいずれかの種類である必要があります。Geometry、Point、Curve、LineString、CircularString、Surface、Polygon、CurvePolygon、**GeometryCollection**、**MultiSurface**、**MultiPolygon、MultiCurve、MultiLineString**、**MultiPoint**、**FullGlobe**。  
  
上記以外の文字列を入力に使用した場合、このメソッドは `ArgumentException` をスローします。  
  
このメソッドは正確ではありません。  
  
## <a name="examples"></a>例  
`MultiPoint` インスタンスを作成し、`InstanceOf()` を使用して、このインスタンスが `GeometryCollection` であるかどうかを判定する例を次に示します。  
  
```sql  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
