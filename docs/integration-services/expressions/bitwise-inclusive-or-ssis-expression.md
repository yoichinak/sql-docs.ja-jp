---
description: '| (ビット演算包含的 OR) (SSIS 式)'
title: '| (ビット演算包含的 OR) (SSIS 式) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '| (bitwise inclusive OR)'
- bitwise inclusive OR (|)
ms.assetid: 4dce9eb2-3680-4adc-81a3-816ea52cef49
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6736267708612a67314959b74cb4c91d0f6f39c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430624"
---
# <a name="-bitwise-inclusive-or-ssis-expression"></a>| (ビット演算包含的 OR) (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  2 つの整数値の OR 演算をビット単位で実行します。 最初のオペランドの各ビットを 2 番目のオペランドの対応するビットと比較します。 どちらかのビットが 1 の場合、対応する結果のビットは 1 に設定されます。 それ以外の場合、対応する結果ビットはゼロ (0) に設定されます。  
  
 どちらの条件も符号付き整数データ型か、または、どちらの条件も符号なし整数データ型である必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
  
integer_expression1 | integer_expression2  
  
```  
  
## <a name="arguments"></a>引数  
 *integer_expression1 ,integer_ expression2*  
 符号付きまたは符号なし整数データ型の任意の有効な式です。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 2 つの引数のデータ型によって決まります。 詳しくは、「 [式における Integration Services データ型](../../integration-services/expressions/integration-services-data-types-in-expressions.md)」をご覧ください。  
  
## <a name="remarks"></a>注釈  
 条件のいずれかが NULL の場合、式の結果は NULL になります。  
  
## <a name="expression-examples"></a>式の例  
 この例では、変数 **NumberA** と **NumberB**間で包含的 OR 演算をビット単位で実行します。 **NumberA** には 3 (00000011) が、 **NumberB** には 9 (00001001) が含まれます。  
  
```  
@NumberA | @NumberB  
```  
  
 式は 11 (00001011) に評価されます。  
  
 00000011  
  
 00001001  
  
 ----------\-  
  
 00001011  
  
 この例では、 **ReorderPoint** 列と **SafetyStockLevel** 列の間でビット演算子包含的 OR を実行します。  
  
```  
ReorderPoint | SafetyStockLevel  
```  
  
 **ReorderPoint** が 10 で **SafetyStockLevel** が 8 の場合、式は 10 (00001010) に評価されます。  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001010  
  
 この例では、2 つの整数間の包含的 OR 演算をビット単位で実行します。  
  
```  
3 | 5   
```  
  
 式は 7 (00001011) に評価されます。  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000111  
  
## <a name="see-also"></a>関連項目  
 [&#124;&#124; (論理 OR) (SSIS 式)](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [^ &#40;ビット演算子排他的 OR&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [演算子の優先順位と結合規則](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
