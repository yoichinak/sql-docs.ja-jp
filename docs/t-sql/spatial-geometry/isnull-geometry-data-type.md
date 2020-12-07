---
description: IsNull (geometry データ型)
title: IsNull (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IsNull (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- IsNull (geometry Data Type)
ms.assetid: f95813a5-26c0-48aa-bfb8-56d2a0980788
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 02e8775089f6e8112452ff2a0ff780bc9a848f31
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88497053"
---
# <a name="isnull-geometry-data-type"></a>IsNull (geometry データ型)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** のインスタンスの型が NULL かどうかを調べます。 インスタンスが NULL でない場合は 0 を返します。
  
## <a name="syntax"></a>構文  
  
```  
.IsNull  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型: **bit**  
  
 CLR の型: **SqlBoolean**  
  
## <a name="remarks"></a>解説  
 `IsNull` を使用して、**geometry** インスタンスが NULL かどうかをテストできます。 `IsNull` は、インスタンスが NULL でない場合は 0 を返しますが、NULL の場合は NULL を返します。  
  
 このメソッドは、主に SQL Server インフラストラクチャによって使用されます。インスタンスが NULL かどうかをテストするために `IsNull` を使用することはお勧めしません。  
  

## <a name="see-also"></a>参照  
 [geometry インスタンスの拡張メソッド](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

