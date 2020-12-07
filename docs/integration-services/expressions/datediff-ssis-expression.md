---
description: DATEDIFF (SSIS 式)
title: DATEDIFF (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DATEDIFF statement
- dates [Integration Services], DATEDIFF
ms.assetid: 449b327f-47c7-4709-8bc6-4ee9a35cc330
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3e7133fffcea2afe188e00f2c80aa51d6825386c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484430"
---
# <a name="datediff-ssis-expression"></a>DATEDIFF (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  指定された 2 つの日付間の差を、日付および時刻の単位で返します。 *datepart* パラメーターにより、差分を計算する基となる日付と時刻を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DATEDIFF(datepart, startdate, endate)  
```  
  
## <a name="arguments"></a>引数  
 *datepart*  
 比較して値を返す日付の要素を指定するパラメーターです。  
  
 *startdate*  
 間隔の開始日です。  
  
 *endate*  
 間隔の終了日です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>注釈  
 次の表に、式エバリュエーターで認識される日付要素 (datepart) と省略形を示します。  
  
|datepart|省略形|  
|--------------|-------------------|  
|Year|yy、yyyy|  
|Quarter|qq、q|  
|Month|mm、m|  
|Dayofyear|dy、y|  
|日間|dd、d|  
|週|wk、ww|  
|平日|dw、w|  
|時間|Hh|  
|分|mi、n|  
|Second|ss、s|  
|Millisecond|Ms|  
  
 引数のいずれかが NULL の場合、DATEDIFF は NULL を返します。  
  
 日付リテラルは、日付データ型のいずれかに明示的にキャストされる必要があります。 詳細については、「 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
 日付が有効でない場合、日付または時刻の単位が文字列でない場合、開始日が日付でない場合、または終了日が日付でない場合は、エラーが発生します。  
  
 終了日が開始日よりも前の日付の場合、この関数は負の値を返します。 開始日と終了日の日付が同一、または同じ間隔の範囲内である場合、この関数は 0 を返します。  
  
## <a name="ssis-expression-examples"></a>SSIS 式の例  
 この例では、2 つの日付リテラル間の日数が計算されます。 日付が "mm/dd/yyyy" 形式の場合、7 が返されます。  
  
```  
DATEDIFF("dd", (DT_DBTIMESTAMP)"8/1/2003", (DT_DBTIMESTAMP)"8/8/2003")  
```  
  
 この例では、日付リテラルと現在の日付の間の月数が返されます。  
  
```  
DATEDIFF("mm", (DT_DBTIMESTAMP)"8/1/2003",GETDATE())  
```  
  
 この例では、 **ModifiedDate** 列の日付と、 **YearEndDate** 変数の日付の間の週数が返されます。 **YearEndDate** が **date** データ型の場合、明示的なキャストは必要ありません。  
  
```  
DATEDIFF("Week", ModifiedDate,@YearEndDate)  
```  
  
## <a name="see-also"></a>関連項目  
 [DATEADD &#40;SSIS 式&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEPART &#40;SSIS 式&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;SSIS 式&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;SSIS 式&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;SSIS 式&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
