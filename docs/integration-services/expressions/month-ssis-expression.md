---
description: MONTH (SSIS 式)
title: MONTH (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], MONTH
- MONTH function
ms.assetid: b5a47a11-c2ef-49bd-bd70-235632ff7bf6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 24ab080c25e240ce62260ff708d8cfee137f462f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477574"
---
# <a name="month-ssis-expression"></a>MONTH (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  ある日付の、月の日付要素を表す整数値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
MONTH(date)  
```  
  
## <a name="arguments"></a>引数  
 *date*  
 任意の日付形式の日付です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>注釈  
 引数が NULL の場合、MONTH は NULL を返します。  
  
 日付リテラルは、日付データ型のいずれかに明示的にキャストされる必要があります。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
> [!NOTE]  
>  日付リテラルが DT_DBTIMESTAMPOFFSET と DT_DBTIMESTAMP2 のいずれかの日付データ型に明示的にキャストされると、式の検証は失敗します。  
  
 MONTH 関数を使用すると、DATEPART("MONTH", date) 関数を使用する場合と同じ結果を、より簡単に取得できます。  
  
## <a name="expression-examples"></a>式の例  
 この例では、日付リテラルの月を表す数値が返されます。 データが "mm/dd/yyyy" 形式の場合、この例では 11 が返されます。  
  
```  
MONTH((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 この例では、 **ModifiedDate** 列内の月を表す整数が返されます。  
  
```  
MONTH(ModifiedDate)  
```  
  
 この例では、現在の日付の月を表す整数が返されます。  
  
```  
MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>関連項目  
 [DATEADD &#40;SSIS 式&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS 式&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;SSIS 式&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;SSIS 式&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [YEAR &#40;SSIS 式&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
