---
description: (剰余) (SSIS 式)
title: (剰余) (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '% (modulo operator)'
- remainder of division operation
- modulo operator (%)
ms.assetid: e2920821-2f5b-4c76-8db8-8b9eddf4606f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14ea6b261c63b06d5e6b3fbeb77822c0d3c6836f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457210"
---
# <a name="modulo-ssis-expression"></a>(剰余) (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  最初の数値式を 2 番目の数値式で割った剰余を整数値で返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
dividend % divisor  
  
```  
  
## <a name="arguments"></a>引数  
 *dividend*  
 除算される数値式です。 *dividend* には、有効な任意の数値式を指定できます。 詳しくは、「 [Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」をご覧ください。  
  
 *divisor*  
 被除数を除算する数値式です。 *divisor* には、0 以外の有効な任意の数値式を指定できます。  
  
## <a name="result-types"></a>戻り値の型  
 2 つの引数のデータ型によって決まります。 詳しくは、「 [式における Integration Services データ型](../../integration-services/expressions/integration-services-data-types-in-expressions.md)」をご覧ください。  
  
## <a name="remarks"></a>注釈  
 両方の式は、符号付きまたは符号なし整数データ型に評価される必要があります。  
  
 オペランドのいずれかが NULL の場合、結果は NULL になります。  
  
 剰余 0 は無効です。  
  
## <a name="expression-examples"></a>式の例  
 この例では、2 つの数値リテラルから剰余を計算します。 結果は 3 です。  
  
```  
42 % 13  
```  
  
 この例では、 **SalesQuota** 列と数値リテラルから剰余を計算します。  
  
```  
SalesQuota % 12  
```  
  
 この例では、2 つの数値変数 **Sales$** と **Month**から剰余を計算します。 変数 **Sales$** は、名前に $ 文字が含まれているため、角かっこで囲む必要があります。 詳しくは、「[識別子 &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)」をご覧ください。  
  
```  
@[Sales$] % @Month  
```  
  
 この例では、剰余演算子を使用して、 **Value** 変数の値が偶数か奇数かを判別し、条件演算子を使用して結果を示す文字列を返します。 詳しくは、「[? : &#40;条件&#41; &#40;SSIS 式&#41;](../../integration-services/expressions/conditional-ssis-expression.md)」をご覧ください。  
  
```  
@Value % 2 == 0? "even":"odd"  
```  
  
## <a name="see-also"></a>関連項目  
 [演算子の優先順位と結合規則](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
