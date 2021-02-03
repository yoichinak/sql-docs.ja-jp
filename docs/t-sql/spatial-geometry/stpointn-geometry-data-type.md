---
description: STPointN (geometry データ型)
title: STPointN (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- STPointN_TSQL
- STPointN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN (geometry Data Type)
ms.assetid: 8f0bb3b7-5cd9-42c2-b9f8-f04628653bd0
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 78db87953b38208585bd9ea68c75766cfd3765b1
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99184637"
---
# <a name="stpointn-geometry-data-type"></a>STPointN (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** インスタンス内の指定した地点を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STPointN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *式 (expression)*  
 1 から **geometry** インスタンス内の地点の数までの **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR 戻り値の型: **SqlGeometry**  
  
 Open Geospatial Consortium (OGC) の型: **Point**  
  
## <a name="remarks"></a>解説  
 ユーザーが作成した **geometry** インスタンスの場合、`STPointN()` は、最初に入力した順序で地点を並べ替えることで、*expression* で指定された地点を返します。  
  
 システムによって作成された **geometry** インスタンスの場合、`STPointN()` は、出力する順序ですべての地点を並べ替えることで、*expression* で指定された地点を返します。出力する順序にするには、geometry、geometry 内のリング (必要な場合)、リング内の地点の順序に並べ替えます。 この順序は決定的です。  
  
 1 未満の値を指定してこのメソッドを呼び出すと、**ArgumentOutOfRangeException** がスローされます。  
  
 インスタンス内の地点の数より大きい値を指定してこのメソッドを呼び出すと、メソッドは NULL を返します。  
  
## <a name="examples"></a>例  
 `LineString` インスタンスを作成し、`STPointN()` を使用して、このインスタンスの記述に含まれる 2 番目の地点を取得する例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

