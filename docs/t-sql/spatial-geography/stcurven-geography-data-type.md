---
description: STCurveN (geography データ型)
title: STCurveN (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- STCurveN
- STCurveN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveN method (geography)
ms.assetid: 99ef7100-2c4b-4f07-8d66-b343da94b023
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: fdb5dc0e5bae929b931c219937d89ea2afb9b828
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99207528"
---
# <a name="stcurven-geography-data-type"></a>STCurveN (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **LineString**、**CircularString**、または **CompoundCurve** である **geography** インスタンスから指定された曲線を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STCurveN( n )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *n*  
 1 から **geography** インスタンス内の曲線の数までの **int** 式。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型: **SqlGeography**  
  
## <a name="exceptions"></a>例外  
 n < 1 のとき、**ArgumentOutOfRangeException** がスローされます。  
  
## <a name="remarks"></a>解説  
 次の条件が発生するとき、**NULL** が返されます。  
  
-   **geography** インスタンスが宣言されるが、インスタンス化されない  
  
-   **geography** インスタンスが空である  
  
-   n が **geography** インスタンスの曲線数を超える (「[STNumCurves &#40;geography データ型&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)」参照)  
  
-   **geography** インスタンスのディメンションが等しくない (「[STDimension &#40;geography データ型&#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)」参照)  
  
## <a name="examples"></a>例  
  
### <a name="a-using-stcurven-on-a-circularstring"></a>A. CircularString に対して STCurveN() を使用する  
 次の例では、**CircularString** インスタンスで 2 番目の曲線を返します。  
  
```
 DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 この例では、以下が返されます。  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="b-using-stcurven-on-a-compoundcurve"></a>B. CompoundCurve に対して STCurveN() を使用する  
 次の例では、**CompoundCurve** インスタンスで 2 番目の曲線を返します。  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 この例では、以下が返されます。  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
### <a name="c-using-stcurven-on-a-compoundcurve-containing-three-circularstrings"></a>C. 3 つの CircularStrings を含む CompoundCurve に対して STCurveN() を使用する  
 次の例では、3 つの異なる **CircularString** インスタンスを前の例と同じ曲線シーケンスに結合した **CompoundCurve** インスタンスを使用します。  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE (CIRCULARSTRING (-122.358 47.653, -122.348 47.649, -122.348 47.658), CIRCULARSTRING(-122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STCurveN(2).ToString();
 ```  
  
 この例では、以下が返されます。  
  
 `CIRCULARSTRING (-122.348 47.658, -122.358 47.658, -122.358 47.653)`  
  
 `STCurveN()` では、使用する Well-Known Text (WKT) 形式に関係なく、同じ結果が返されます。  
  
### <a name="d-testing-for-validity-before-calling-stcurve"></a>D. STCurve() を呼び出す前に有効性をテストする  
 次の例では、STCurveN() メソッドを呼び出す前に *n* が有効かどうかを確認する方法を示しています。  
  
```
 DECLARE @g geography;  
 DECLARE @n int;  
 SET @n = 2;  
 SET @g = geography::Parse('LINESTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 IF @n >= 1 AND @n <= @g.STNumCurves()  
 BEGIN  
 SELECT @g.STCurveN(@n).ToString();  
 END
  ```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
