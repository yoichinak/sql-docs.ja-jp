---
description: ToString (geometry データ型)
title: ToString (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- ToString (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- ToString (geometry Data Type)
ms.assetid: 2e55fa98-aa22-4baa-a516-7c233a33e212
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0527c29cc0e49575df91095fd6ab605245b8a4f6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99158624"
---
# <a name="tostring-geometry-data-type"></a>ToString (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

インスタンスに格納されている Z (標高) 値および M (メジャー) 値で補完された geometry インスタンスについて、Open Geospatial Consortium (OGC) Well-Known Text (WKT) 表現を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.ToString ()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **nvarchar(max)**  
  
 CLR の戻り値の型: **SqlString**  
  
## <a name="remarks"></a>注釈  
 このメソッドは、NULL インスタンスに対して呼び出されたときに、文字列 "Null" を返します。  
  
 NULL 以外のインスタンスでは、このメソッドは `AsTextZM().` を使用することと同じです。  
  
## <a name="examples"></a>例  
 `LineString` インスタンスを作成し、`ToString()` を使用してこのインスタンスの記述をフェッチする例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>関連項目  
 [STAsText &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)   
 [geometry インスタンスの拡張メソッド](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

