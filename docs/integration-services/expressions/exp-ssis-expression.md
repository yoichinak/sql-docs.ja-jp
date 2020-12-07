---
description: EXP (SSIS 式)
title: EXP (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 09848aaee36990b8fd56e1f73cb4ba0f5c934095
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425484"
---
# <a name="exp-ssis-expression"></a>EXP (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  数値式の e を基数とする指数を返します。 EXP 関数は LN 関数の逆関数であり、真数と呼ばれる場合もあります。  
  
## <a name="syntax"></a>構文  
  
```  
  
EXP(numeric_expression)  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 有効な数値式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_R8  
  
## <a name="remarks"></a>注釈  
 数値式は、指数の計算前に DT_R8 データ型にキャストされます。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 返される結果は、常に正の数値です。  
  
## <a name="expression-examples"></a>式の例  
 この例では、正の値、負の値、および 0 に、EXP 関数を適用します。  
  
```  
EXP(74)  
```  
  
 1.373382979540176E+32 が返されます。  
  
```  
EXP(-27)  
```  
  
 1.879528816539083E-12 が返されます。  
  
```  
EXP(0)  
```  
  
 1 が返されます。  
  
## <a name="see-also"></a>関連項目  
 [LOG (SSIS 式)](../../integration-services/expressions/log-ssis-expression.md)   
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
