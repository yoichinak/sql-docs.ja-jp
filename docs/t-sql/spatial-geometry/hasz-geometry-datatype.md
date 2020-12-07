---
description: HasZ (geometry データ型)
title: HasZ (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 05/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- HasZ geometry
ms.assetid: aa378943-252a-4079-848b-6c59344fcfce
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 58c43b02c466fa2f5f1bc2b06006855b894cd65c
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88497077"
---
# <a name="hasz-geometry-datatype"></a>HasZ (geometry データ型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  空間オブジェクトに少なくとも 1 つの Z 値が含まれている場合は 1 (true)、それ以外の場合は 0 (false) を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.HasZ  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **bit**  
  
 CLR 戻り値の型: **Boolean**  
  
## <a name="remarks"></a>解説  
  
## <a name="examples"></a>例  
  
```sql  
DECLARE @p GEOMETRY = 'Point(1 1 1 1)'  
SELECT @p.HasZ   
--Returns: 1 (true)  
```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの拡張メソッド](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  
