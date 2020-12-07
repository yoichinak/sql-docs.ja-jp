---
description: STBuffer (geography データ型)
title: STBuffer (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STBuffer (geography Data Type)
- STBuffer_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STBuffer (geography Data Type)
ms.assetid: cb4deab8-642b-44d9-b3d9-85114d64021e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 1d39e58c6dd4fa648d8d4118414925777eb3535b
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "92038319"
---
# <a name="stbuffer-geography-data-type"></a>STBuffer (geography データ型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  **geography** インスタンスからの距離が指定した値以下となる、すべての地点の和集合を表す geography オブジェクトを返します。  
  
 この geography データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STBuffer ( distance )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *distance*  
 **float** 型 (.NET Framework では **double** 型) の値であり、バッファー計算の対象とする **geography** インスタンスからの距離を指定します。  
  
 バッファーの最大距離は、0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 地球の円周の 1/2) で求められる値または全球を超えることはできません。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型: **SqlGeography**  
  
## <a name="remarks"></a>解説  
 STBuffer() は、*tolerance* = abs(distance) \* .001 および *relative* = **false** を指定して [BufferWithTolerance](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md) を呼び出すのと同じ方法でバッファーを計算します。  
  
 バッファーに負の値を指定すると、**geography** インスタンスの境界から、指定された距離の範囲内にある地点がすべて削除されます。  
  
 `STBuffer()` は、**FullGlobe** インスタンスを返すことがあります。たとえば、バッファーの距離が赤道から極地までの距離を超えている場合、`STBuffer()` は 2 つの極地の **FullGlobe** インスタンスを返します。 バッファーは全球を超えることはできません。  
  
 このメソッドは、バッファーの距離が次の制限値を超えている場合、**FullGlobe** インスタンスで **ArgumentException** をスローします。  
  
 0.999 \* *π* * minorAxis \* minorAxis / majorAxis (~0.999 \* 地球の円周の 1/2)  
  
 最大距離の制限により、バッファーを構築する際の柔軟性が最大限に高まります。  
  
 理論上のバッファーと計算されたバッファーの間の誤差は、max(tolerance, extents * 1.E-7) です。tolerance は distance \* .001 になります。 エクステントの詳細は、「[geography データ型メソッド リファレンス](./stequals-geography-data-type.md)」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、`LineString``geography` インスタンスを作成します。 次に、`STBuffer()` を使用して、インスタンスから 1 m 以内にある領域を返します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STBuffer(1).ToString();  
```  
  
## <a name="see-also"></a>参照  
 [BufferWithTolerance &#40;geography データ型&#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)   
 [geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
