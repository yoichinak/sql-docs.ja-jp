---
description: BufferWithTolerance (geography データ型)
title: BufferWithTolerance (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- BufferWithTolerance_TSQL
- BufferWithTolerance
dev_langs:
- TSQL
helpviewer_keywords:
- BefferWithTolerance method
ms.assetid: f1783e6b-0f17-464f-b1c7-1c3f7d8aa042
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e278c50b6a467660c827e3e59181945fdb9985e7
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96115006"
---
# <a name="bufferwithtolerance-geography-data-type"></a>BufferWithTolerance (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geography** インスタンスから各地点までの距離が指定した許容範囲内にある、すべての地点値の和集合を表すジオメトリック オブジェクトを返します。  
  
この geography データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
## <a name="syntax"></a>構文  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
_distance_  
バッファー計算の対象となる **geography** インスタンスからの距離を指定する **float** 式です。  
  
バッファーの最大距離は、0.999 \* _π_  * minorAxis \* minorAxis / majorAxis (~0.999 \*  地球の円周の 1/2) または全球を超えることはできません。  
  
_tolerance_  
バッファー距離の許容範囲を指定する **float** 式です。  
  
理想的なバッファー距離と返される線形近似との差異の最大値が _tolerance_ の値となります。  
  
たとえば、ある地点の理想的なバッファー距離は円ですが、この距離は多角形で近似する必要があります。 許容範囲が小さくなるほど、多角形に含まれる点が多くなります。 この結果により結果がより複雑になりますが、誤差が最小になります。  
  
最小値は距離の 0.1% で、それより小さい許容範囲はこの最小値に切り上げられます。  
  
_relative_  
_tolerance_ の値が相対値か絶対値かを指定する **bit** です。 値が 'TRUE' または 1 の場合、許容範囲は相対値です。 この値は、_tolerance_ パラメーターと角度 \* 楕円の赤道半径の積です。 値が 'FALSE' または 0 の場合、許容範囲は絶対値です。 _tolerance_ 値は、理想的なバッファー距離と返される線形近似との差異の絶対最大値になります。  
  
## <a name="return-types"></a>戻り値の型  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
CLR の戻り値の型: **SqlGeography**  
  
## <a name="remarks"></a>解説  
_distance_ が数値ではない (NAN) 場合、または _distance_ が正か負の無限大の場合、このメソッドは **ArgumentException** をスローします。  _tolerance_ が 0、数値ではない (NaN)、負、または正か負の無限大の場合も、このメソッドは **ArgumentException** をスローします。  
  
`STBuffer()` は、**FullGlobe** インスタンスを返すことがあります。たとえば、バッファーの距離が赤道から極地までの距離を超えている場合、`STBuffer()` は 2 つの極地の **FullGlobe** インスタンスを返します。  
  
このメソッドは、バッファーの距離が次の制限値を超えている場合、**FullGlobe** インスタンスで **ArgumentException** をスローします。  
  
0.999 \* _π_ * minorAxis \* minorAxis / majorAxis (~0.999 \* 地球の円周の 1/2)  
  
理論上のバッファーと計算されたバッファーの間の誤差は、max(tolerance, extents \* 1.E-7) です。この tolerance は _tolerance_ パラメーターの値になります。 エクステントの詳細は、「[geography データ型メソッド リファレンス](./stequals-geography-data-type.md)」を参照してください。  
  
このメソッドは正確ではありません。  
  
## <a name="examples"></a>例  
`Point` インスタンスを作成し、`BufferWithTolerance()` を使用して、インスタンスの周りの大まかなバッファーを取得する例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>関連項目  
[STBuffer &#40;geography データ型&#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)   
[Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
