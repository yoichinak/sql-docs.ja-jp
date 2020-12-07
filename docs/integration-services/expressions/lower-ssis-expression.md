---
description: LOWER (SSIS 式)
title: LOWER (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fccd74824087b5b57eeaee5a091e94123e0b0f5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457228"
---
# <a name="lower-ssis-expression"></a>LOWER (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  大文字が小文字に変換された状態の文字式を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
LOWER(character_expression)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 小文字に変換する文字式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>解説  
 LOWER は DT_WSTR データ型でのみ機能します。 *character_expression* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、LOWER による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。 詳しくは、「[Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」および「[Cast &#40;SSIS 式&#41;](../../integration-services/expressions/cast-ssis-expression.md)」をご覧ください。  
  
 引数が NULL の場合、LOWER は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 この例では、文字列リテラルを小文字に変換します。 返される結果は "new york" です。  
  
```  
LOWER("New York")  
```  
  
 この例では、 **Color** 入力列の最初の文字を除くすべての文字を小文字に変換します。 Color が YELLOW の場合、返される結果は "Yellow" です。 詳細については、「[SUBSTRING &#40;SSIS 式&#41;](../../integration-services/expressions/substring-ssis-expression.md)」を参照してください。  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 この例では、 **CityName** 変数の値を小文字に変換します。  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>関連項目  
 [UPPER (SSIS 式)](../../integration-services/expressions/upper-ssis-expression.md)   
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
