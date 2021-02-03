---
description: Z (geometry データ型)
title: Z (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- Z (geometry Data Type)
- Z_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Z (geometry Data Type)
ms.assetid: a62ed736-44df-4591-9109-ce90e1df9bd3
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: dcd85bac5ba2be71a49761dfe609092761fd3fc0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99194709"
---
# <a name="z-geometry-data-type"></a>Z (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

インスタンスの Z (標高) 値です。 標高値のセマンティクスはユーザーが定義します。
  
## <a name="syntax"></a>構文  
  
```  
  
.Z  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の型: **float**  
  
 CLR の型:**SqlDouble**  
  
## <a name="remarks"></a>解説  
 geometry インスタンスが Point ではない場合や、**Point** インスタンスにこのプロパティの値が設定されていない場合は、このプロパティの値は null になります。  
  
 このプロパティは読み取り専用です。  
  
 Z 座標値はライブラリが行う計算では使用されません。また、ライブラリが行う計算によって渡されることもありません。  
  
## <a name="examples"></a>例  
 次の例では、Z (標高) 値と M (メジャー) 値を含む `Point` インスタンスを作成し、`Z` を使用してインスタンスの Z 値をフェッチします。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.Z;  
```  
  
## <a name="see-also"></a>参照  
 [M &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [AsTextZM &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)   
 [geometry インスタンスの拡張メソッド](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

