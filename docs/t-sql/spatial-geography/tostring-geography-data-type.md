---
description: ToString (geography データ型)
title: ToString (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- ToString (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- ToString method
ms.assetid: 045c12fa-8fc6-441a-9500-7021cb4ff13e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d7d2d4b6d4f786c7962155e11b7fe89bbb491a7d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99187739"
---
# <a name="tostring-geography-data-type"></a>ToString (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  インスタンスに格納されている Z (標高) 値および M (メジャー) 値で補完された **geography** インスタンスについて、Open Geospatial Consortium (OGC) Well-Known Text (WKT) 表現を返します。  
  
 この geography データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
## <a name="syntax"></a>構文  
  
```  
  
.ToString ()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **nvarchar(max)**  
  
 CLR の戻り値の型: **SqlString**  
  
## <a name="remarks"></a>注釈  
 このメソッドは、NULL インスタンスで呼び出されたときに文字列 "Null" を返します。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では、サーバー上で使用可能な結果セットが **FullGlobe** インスタンスに拡張されています。 このメソッドは、`AsTextZM()` と同じ値を返します。  
  
 このメソッドは正確ではありません。  
  
## <a name="examples"></a>例  
 `LineString` インスタンスを作成し、`ToString()` を使用してインスタンスの記述を返す例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [AsTextZM &#40;geography データ型&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
  
