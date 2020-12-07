---
description: '! (論理 Not) (SSIS 式)'
title: '! (論理 Not) (SSIS 式) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logical Not (!)
- '! (logical Not)'
ms.assetid: d5c4d1e1-7be4-4d25-bcd9-5b6ddb53b3b3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1643daac9dab5b1027a0df8fec56ccd190e5980a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484405"
---
# <a name="-logical-not-ssis-expression"></a>! (論理 Not) (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  ブール型のオペランドを否定します。  
  
> [!NOTE]  
>  ! 演算子は、他の演算子と組み合わせて使用することはできません。 たとえば、! 演算子と > 演算子を組み合わせて !> 演算子にすることはできません。  
  
## <a name="syntax"></a>構文  
  
```  
  
!boolean_expression  
  
```  
  
## <a name="arguments"></a>引数  
 *boolean_expression*  
 ブール型に評価される任意の有効な式です。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="result-types"></a>戻り値の型  
 DT_BOOL  
  
## <a name="remarks"></a>注釈  
 次の表は、! 操作を完了するための次の手順について引き続き調査中です。  
  
|元のブール式|! 演算子の適用後 operator|  
|---------------------------------|------------------------------------|  
|true|false|  
|NULL|NULL|  
|false|true|  
  
## <a name="expression-examples"></a>式の例  
 **Color** 列の値が "red" の場合、この例は FALSE に評価されます。  
  
```  
!(Color == "red")  
```  
  
 **MonthNumber** 変数の値が現在の月を示す整数と同じ場合、この例は TRUE に評価されます。 詳細については、「[MONTH &#40;SSIS 式&#41;](../../integration-services/expressions/month-ssis-expression.md)」および「[GETDATE &#40;SSIS 式&#41;](../../integration-services/expressions/getdate-ssis-expression.md)」をご覧ください。  
  
```  
!(@MonthNumber != MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>関連項目  
 [演算子の優先順位と結合規則](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
