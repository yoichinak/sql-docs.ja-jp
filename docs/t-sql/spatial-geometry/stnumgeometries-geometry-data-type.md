---
description: STNumGeometries (geometry データ型)
title: STNumGeometries (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 8ef4aa6a47bdb974803d111a023b473c0c49cf0b
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88444948"
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** インスタンスを構成するジオメトリの数を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STNumGeometries ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **int**  
  
 CLR の戻り値の型: **SqlInt32**  
  
## <a name="remarks"></a>解説  
 このメソッドは、**geometry** インスタンスが **MultiPoint**、**MultiLineString**、**MultiPolygon**、**GeometryCollection** インスタンスではない場合に 1 を返し、**geometry** インスタンスが空の場合に 0 を返します。  
  
> [!NOTE]  
>  **GeometryCollection** に入れ子になった空の要素がある場合は、`STNumGeometries()` は 0 を返しません。 **GeometryCollection** インスタンス内の要素は空ですが、インスタンス自体は空のセットではありません。  
  
  

