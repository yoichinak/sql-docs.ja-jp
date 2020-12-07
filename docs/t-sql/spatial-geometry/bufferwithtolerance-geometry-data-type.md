---
description: BufferWithTolerance (geometry データ型)
title: BufferWithTolerance (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
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
- BufferWithTolerance (geometry Data Type)
ms.assetid: 7049d37a-3e72-4e93-87a1-c96a6f0e2b99
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a039118dc0abe85b065d74b96f551c2991820333
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128181"
---
# <a name="bufferwithtolerance-geometry-data-type"></a>BufferWithTolerance (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** インスタンスから各地点までの距離が指定した許容範囲内にある、すべての地点値の和集合を表すジオメトリック オブジェクトを返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.BufferWithTolerance ( distance, tolerance, relative )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *distance*  
 バッファー計算の対象となる **geometry** インスタンスからの距離を指定する **float** 式です。  
  
 *tolerance*  
 バッファー距離の許容範囲を指定する **float** 式です。  
  
 *許容範囲* とは、返された線形近似の理想的なバッファー距離の最大幅のことです。  
  
 たとえば、ある地点の理想のバッファー距離は円ですが、多角形によって近似された形状になる必要があります。 許容範囲が小さいほど、多角形の頂点の数は多くなります。つまり、計算結果の複雑性が増しますが、元の図形との差が小さくなります。  
  
 *relative*  
 *tolerance* の値が相対値か絶対値かを指定する **bit** です。 'TRUE' または 1 の場合、許容範囲は相対値であり、*tolerance* パラメーターとインスタンスに外接する四角形の直径の積として計算されます。 'FALSE' または 0 の場合、許容範囲は絶対値であり、*tolerance* 値は、返された線形近似の理想的なバッファー距離の絶対最大幅になります。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR 戻り値の型: **SqlGeometry**  
  
## <a name="exceptions"></a>例外  
 *tolerance* パラメーターには、0 より大きい値を指定する必要があります。 *tolerance* <= 0 の場合は、`System.ArgumentOutOfRangeException` がスローされます。  
  
> [!NOTE]  
>  *tolerance* は **float** 型であるため、tolerance に指定された値が非常に小さい場合、浮動小数点型の丸めの問題が原因で `System.Runtime.InteropServices.COMException` がスローされる可能性があります。  
  
## <a name="remarks"></a>解説  
 *distance* > 0 のときは、**Polygon** または **MultiPolygon** インスタンスが返されます。  
  
> [!NOTE]  
>  distance は **float** であるため、非常に小さい値は計算時に 0 と見なされることがあります。 その場合、呼び出し元の **geometry** インスタンスのコピーが返されます。 「[float 型と real 型 &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)」を参照してください。  
  
 *distance* = 0 の場合は、呼び出し元の **geometry** インスタンスのコピーが返されます。  
  
 *distance* < 0 の場合、  
  
-   インスタンスの次元数が 0 または 1 であれば、空の **GeometryCollection** インスタンスが返されます。  
  
-   インスタンスの次元数が 2 以上のとき、負の値のバッファーが返されます。  
  
    > [!NOTE]  
    >  負の値のバッファーでは、空の **GeometryCollection** インスタンスが作成されることもあります。  
  
 バッファーに負の値を指定すると、**geometry** インスタンスの境界から、指定された距離の範囲内にある地点をすべて削除します。  
  
 理論上のバッファーと計算されたバッファーの間の誤差は、max(tolerance, extents \* 1.E-7) です。この tolerance は *tolerance* パラメーターの値になります。 エクステントの詳細については、「[geometry データ型メソッド リファレンス](./spatial-types-geometry-transact-sql.md)」を参照してください。  
  
## <a name="examples"></a>例  
 `Point` インスタンスを作成し、`BufferWithTolerance()` を使用して、インスタンスの周りの大まかなバッファーを取得する例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 3)', 0);  
SELECT @g.BufferWithTolerance(1, .5, 0).ToString();  
```  
  
## <a name="see-also"></a>関連項目  
 [STBuffer &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stbuffer-geometry-data-type.md)   
 [geometry インスタンスの拡張メソッド](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
