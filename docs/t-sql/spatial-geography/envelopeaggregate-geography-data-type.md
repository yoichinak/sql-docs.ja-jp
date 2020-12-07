---
description: EnvelopeAggregate (geography データ型)
title: EnvelopeAggregate (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAggregate_TSQL
- EnvelopeAggregate
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAggregate method (geography)
ms.assetid: 4947797f-edb8-490f-beca-37df9ec06954
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9b14db5a616f41049b5cabc845cd822356e34522
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96114992"
---
# <a name="envelopeaggregate-geography-data-type"></a>EnvelopeAggregate (geography データ型)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

特定の **geography** オブジェクト セットの境界オブジェクトを返します。 結果として得られる **geography** オブジェクトには、複数の円弧セグメントが含まれます。
  
## <a name="syntax"></a>構文  
  
```  
  
EnvelopeAggregate ( geography_operand )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *geography_operand*  
 エンベロープ集計操作を実行する **geography** オブジェクト セットを保持する **geography** 型のテーブルの列を指定します。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
## <a name="remarks"></a>解説  
 結果の境界オブジェクトが半球より大きい場合は、**FullGlobe** オブジェクトが返されます。 このメソッドは正確ではありません。  
  
 入力の SRID が異なる場合、メソッドでは **null** が返されます。 「[&#40;SRIDs&#41; Spatial Reference Identifiers](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)」を参照してください。  
  
 メソッドでは、**null** 入力は無視されます。  
  
> [!NOTE]  
>  メソッドは、入力された値がすべて **null** の場合、**null** を返します。  
  
## <a name="examples"></a>例  
 次の例は、都市内の **geography** ロケーション ポイントのセットで `EnvelopeAggregate` を実行します。  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::EnvelopeAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>参照  
 [拡張された静的な地理メソッド](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
