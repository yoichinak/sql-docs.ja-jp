---
description: M (geography データ型)
title: M (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- M (geography Data Type)
- M_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- M method
ms.assetid: cdba04f0-4e17-48f6-bafb-b1f918c5a501
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 77a79972671854e7e8538de7b943545955f61e89
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88422426"
---
# <a name="m-geography-data-type"></a>M (geography データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** インスタンスの **M** (メジャー) 値。 メジャー値のセマンティクスはユーザー自身が定義しますが、一般的には線分に沿った距離を指します。 たとえば、メジャー値を使用して、道路沿いのマイル標を追跡できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
.M  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の型: **float**  
  
 CLR の型:**SqlDouble**  
  
## <a name="remarks"></a>解説  
 **geography** インスタンスが **Point** ではない場合や、**Point** インスタンスにこのプロパティの値が設定されていない場合は、このプロパティの値は null になります。  
  
 このプロパティは読み取り専用です。  
  
 M 値は、ライブラリによる計算では使用されません。また、ライブラリによる計算によって渡されることもありません。  
  
## <a name="examples"></a>例  
 次の例では、Z (標高) 値と M (メジャー) 値を含む `Point` インスタンスを作成し、`M` を使用してインスタンスの `M` 値をフェッチします。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Z &#40;geography データ型&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
