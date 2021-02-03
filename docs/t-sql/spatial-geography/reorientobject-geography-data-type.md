---
description: ReorientObject (geography データ型)
title: ReorientObject (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- ReorientObject
- ReorientObject_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ReorientObject method (geography)
ms.assetid: e2a1a4f1-211b-4e82-abed-03fc7140a83c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: af0f03f5f4f1eb947b07273470b71bd93ed1fc01
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99210137"
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject (geography データ型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

内部領域と外部領域が入れ替えられた **geography** インスタンスを返します。  
  
この **geography** データ型メソッドは、半球より大きい **FullGlobe** インスタンスまたは空間インスタンスをサポートします。  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
.ReorientObject (geography)  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
_geography_  
`ReorientObject()` を呼び出したときの別の **geography** インスタンスです。  
  
## <a name="return-value"></a>戻り値  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
CLR の戻り値の型: **SqlGeography**  
  
## <a name="remarks"></a>解説  
このメソッドでは、**GeometryCollection** 内のすべての **Polygons** のリングの方向が変更されますが、指定されたコレクション内の **Points** または **Linestrings** はいずれも削除または変更されません。  
  
このメソッドに **GeometryCollection** を渡すと、そのコレクション内の各インスタンスの方向が変更されますが、コレクション全体の方向は変更されません。  
  
## <a name="examples"></a>例  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>参照  
[Geography インスタンスの拡張メソッド](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
