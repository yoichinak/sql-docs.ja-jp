---
description: Parse (geometry データ型)
title: Parse (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Parse (geometry Data Type)
ms.assetid: 6e080919-4b64-46cd-8dd2-254a9c232e53
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 2774f83d167ec61d0e1a2d68b391c2d5d3318535
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88416948"
---
# <a name="parse-geometry-data-type"></a>Parse (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現を基に **geometry** インスタンスを返します。 `Parse()` は、パラメーターとして SRID (spatial reference ID) の値を 0 と想定している点を除いて、[STGeomFromText()](../../t-sql/spatial-geometry/parse-geometry-data-type.md) と同じです。 入力には、オプションとして Z (標高) 値と M (メジャー) 値が含まれる場合があります。
  
## <a name="syntax"></a>構文  
  
```  
  
Parse ( 'geometry_tagged_text' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *geometry_tagged_text*  
 返される **geometry** インスタンスの WKT 表現です。 *geometry_tagged_text* は **nvarchar** 式です。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR 戻り値の型: **SqlGeometry**  
  
## <a name="remarks"></a>解説  
 `Parse()` によって返された **geometry** インスタンスの OGC 型は、対応する WKT 入力に設定されます。  
  
 "NULL" 文字列は、**geography** の NULL インスタンスと解釈されます。  
  
 このメソッドでは、入力が正しい形式でない場合に、**FormatException** をスローします。  
  
## <a name="examples"></a>例  
 `Parse()` を使用して `geometry` インスタンスを作成する例を次に示します。  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Parse('LINESTRING (100 100, 20 180, 180 180)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>参照  
 [STGeomFromText](../../t-sql/spatial-geometry/parse-geometry-data-type.md)   
 [拡張された静的なジオメトリ メソッド](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  

