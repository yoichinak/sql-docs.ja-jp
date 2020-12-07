---
description: AsGml (geography データ型)
title: AsGml (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsGml_(geography_Data_Type)_TSQL
- AsGml
- AsGml_TSQL
- AsGml (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- AsGml method
ms.assetid: 67795c64-d8d3-48dc-93ef-3c8a9274deb6
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 28d810b8bf74a91a72dad7ab7d9eadce9bbfb9ae
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124367"
---
#  <a name="asgml---geography-data-type"></a>AsGml - geography データ型
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** インスタンスの Geography Markup Language (GML) 表現を返します。  
  
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
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.AsGml();  
```  
  
 このメソッドは、GML 表現を `LineString` インスタンスとして返します。  
  
```  
<LineString xmlns="https://www.opengis.net/gml"><posList>47.656 -122.36 47.656 -122.343</posList></LineString>  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
