---
description: STMLineFromText (geography データ型)
title: STMLineFromText (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- STMLineFromText (geography Data Type)
- STMLineFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromText method
ms.assetid: 66dfd722-a9bd-45d3-9788-f1946dd23e17
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 093261aa0794c4615e720411fc55c4173f531f0e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99195343"
---
# <a name="stmlinefromtext-geography-data-type"></a>STMLineFromText (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現を基に **geography** インスタンスを返します。インスタンスに格納されている Z (標高) 値と M (メジャー) 値で補完されています。
  
## <a name="syntax"></a>構文  
  
```  
  
STMLineFromText ( 'multilinestring_tagged_text' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *multilinestring_tagged_text*  
 返される **geographyMultiLineString** インスタンスの WKT 表現です。 *multilinestring_tagged_text* は **nvarchar(max)** 式です。  
  
 *SRID*  
 返される **geographyMultiLineString** インスタンスの SRID (spatial reference ID) を表す **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型: **SqlGeography**  
  
 OGC の型: **MultiLineString**  
  
## <a name="remarks"></a>解説  
 このメソッドでは、入力が整形式でない場合に、**FormatException** がスローされます。  
  
## <a name="examples"></a>例  
 `STMLineFromText()` を使用して `geography` インスタンスを作成する例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STMLineFromText('MULTILINESTRING ((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653), (-122.357 47.654, -122.357 47.657, -122.349 47.657, -122.349 47.650, -122.357 47.654))', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>参照  
 [OGC の静的な地理メソッド](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
