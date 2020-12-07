---
description: STMPolyFromWKB (geography データ型)
title: STMPolyFromWKB (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMPolyFromWKB (geography Data Type)
- STMPolyFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPolyFromWKB method
ms.assetid: c4d0e649-0abb-4343-a3f0-3a702c8bbbdb
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 76adf5bfff925c74f728d19b6781f346646354fa
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88306184"
---
# <a name="stmpolyfromwkb-geography-data-type"></a>STMPolyFromWKB (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Open Geospatial Consortium (OGC) Well-Known Binary (WKB) 表現から **geographyMultiPolygon** インスタンスを返します。
  
## <a name="syntax"></a>構文  
  
```  
  
STMPolyFromWKB ( 'WKB_multipolygon' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *WKB_multipolygon*  
 返される **geographyMultiPolygon** インスタンスの WKB 表現です。 *WKB_multipolygon* は、**varbinary (max)** 式です。  
  
 *SRID*  
 返される **geographyMultiPolygon** インスタンスの SRID (spatial reference ID) を表す **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型: **SqlGeography**  
  
 OGC の型: **MultiPolygon**  
  
## <a name="examples"></a>例  
 `STMPolyFromWKB()` を使用して `geography` インスタンスを作成する例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STMPolyFromWKB(0x01060000000200000001030000000100000004000000F4FDD478E9965EC0DD24068195D3474083C0CAA145965EC0508D976E12D34740F4FDD478E9965EC04E62105839D44740F4FDD478E9965EC0DD24068195D3474001030000000100000004000000E7FBA9F1D2955EC08716D9CEF7D34740E7FBA9F1D2955EC0F853E3A59BD447405839B4C876965EC0F853E3A59BD44740E7FBA9F1D2955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>参照  
 [OGC の静的な地理メソッド](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
