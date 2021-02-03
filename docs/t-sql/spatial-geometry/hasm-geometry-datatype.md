---
description: HasM (geometry データ型)
title: HasM (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- HasM geometry
ms.assetid: 15540837-c4bf-4d18-b380-13ae31f3226f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b332c6c2acf9e367318e58e3816aad63ea5e6498
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99159446"
---
# <a name="hasm-geometry-datatype"></a>HasM (geometry データ型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  空間オブジェクトに少なくとも 1 つの M 値が含まれている場合は 1 (true)、それ以外の場合は 0 (false) が返されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
.HasM  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR 戻り値の型: **Boolean**  
  
## <a name="remarks"></a>解説  
  
## <a name="examples"></a>例  
  
```sql  
DECLARE @p GEOMETRY = 'Point(1 1 1 1)'  
SELECT @p.HasM   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの拡張メソッド](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)  
  
