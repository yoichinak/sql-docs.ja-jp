---
description: AsGml (geometry データ型)
title: AsGml (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- AsGml(geometry_Data_Type)_TSQL
- AsGml
- AsGml(geometry Data Type)
- AsGml_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsGml (geometry Data Type)
ms.assetid: f6c2e130-05f3-4ef3-921b-d78b51437d48
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c932617b3f2bea916105242e7195c5302d9ca130
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99208715"
---
# <a name="asgml-geometry-data-type"></a>AsGml (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** インスタンスの Geography Markup Language (GML) 表現を返します。
  
GML (Geography Markup Language) の詳細については、Open Geospatial Consortium (OGC) の仕様書「[OGC の仕様、Geography Markup Language](https://go.microsoft.com/fwlink/?LinkId=93629)」を参照してください。
  
## <a name="syntax"></a>構文  
  
```  
  
.AsGml ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **xml**  
  
 CLR 戻り値の型: **SqlXml**  
  
## <a name="remarks"></a>解説  
  
## <a name="examples"></a>例  
 `LineString` インスタンスを作成し、`AsGML()` を使用して、インスタンスの GML 表現を返す例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0)  
SELECT @g.AsGml();  
```  
  
 このメソッドは、GML 表現を `LineString` インスタンスとして返します。  
  
```  
<LineString xmlns="https://www.opengis.net/gml">  
<posList>0 0 0 1 1 0</posList></LineString>  
```  
  
## <a name="see-also"></a>参照  
 [geometry インスタンスの拡張メソッド](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

