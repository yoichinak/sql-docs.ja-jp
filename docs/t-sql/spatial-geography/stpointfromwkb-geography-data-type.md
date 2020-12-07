---
description: STPointFromWKB (geography データ型)
title: STPointFromWKB (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointFromWKB_TSQL
- STPointFromWKB (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointFromWKB method
ms.assetid: b3b4e3bb-47bc-4621-99c4-c97aa60cdf8b
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 70eabd3b36ad564b02d16e3ce906405d83a55730
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88459023"
---
# <a name="stpointfromwkb-geography-data-type"></a>STPointFromWKB (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Open Geospatial Consortium (OGC) Well-Known Binary (WKB) 表現から **geographyPoint** インスタンスを返します。
  
## <a name="syntax"></a>構文  
  
```  
  
STPointFromWKB ( 'WKB_point' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *WKB_point*  
 返される **geographyPoint** インスタンスの WKB 表現です。 *WKB_point* は、**varbinary(max)** 式です。  
  
 *SRID*  
 返される **geographyPoint** インスタンスの SRID (spatial reference ID) を表す **int** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型: **SqlGeography**  
  
 OGC の型: **Point**  
  
## <a name="remarks"></a>解説  
 このメソッドでは、入力が整形式でない場合に、**FormatException** がスローされます。  
  
## <a name="examples"></a>例  
 `STPointFromWKB()` を使用して `geography` インスタンスを作成する例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STPointFromWKB(0x010100000017D9CEF753D347407593180456965EC0, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>参照  
 [OGC の静的な地理メソッド](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
