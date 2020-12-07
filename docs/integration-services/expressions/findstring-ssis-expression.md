---
description: FINDSTRING (SSIS 式)
title: FINDSTRING (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- FINDSTRING function
ms.assetid: c83cb1b1-3c52-4496-b518-4c9253b9336d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3c4da6f54ead49d01d9d691cc081ac9b9955c693
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123247"
---
# <a name="findstring-ssis-expression"></a>FINDSTRING (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  文字式内の文字列のうち、指定された文字列が検出された場所を返します。 返される結果は、1 を基点とする検出場所のインデックスです。 文字列パラメーターは文字式に評価され、検出場所を示すパラメーターは整数に評価される必要があります。 文字列が見つからない場合、戻り値は 0 になります。 文字列の検出回数が、引数によって指定された数より少ない場合の戻り値は 0 です。  
  
## <a name="syntax"></a>構文  
  
```  
  
FINDSTRING(character_expression, searchstring, occurrence)  
```  
  
## <a name="arguments"></a>引数  
 *character_expression*  
 検索対象が含まれる文字列です。  
  
 *searchstring*  
 検索する文字列です。  
  
 *occurrence*  
 何回目に検出した *searchstring* の場所をレポートするかを指定する、符号付きまたは符号なし整数です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_I4  
  
## <a name="remarks"></a>注釈  
 FINDSTRING は DT_WSTR データ型でのみ機能します。  *character_expression* および *searchstring* 引数が DT_STR データ型の文字列リテラルまたはデータ列である場合は、FINDSTRING による演算の実行前に、暗黙的に DT_WSTR データ型にキャストされます。 その他のデータ型は、明示的に DT_WSTR データ型にキャストされる必要があります。 詳しくは、「[Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」および「[Cast &#40;SSIS 式&#41;](../../integration-services/expressions/cast-ssis-expression.md)」をご覧ください。  
  
 FINDSTRING は、 *character_expression* または *searchstring* が null の場合は null を返します。  
  
 1 回目に検出された場所のインデックスを取得するには、 *occurrence* 引数の値に 1 を使用します。2 回目以降の検出場所のインデックスを取得する場合も同様です。  
  
 *occurrence* には、0 より大きい整数値を指定してください。  
  
## <a name="expression-examples"></a>式の例  
 この例では、文字列リテラルを使用します。 値 11 が返されます。  
  
```  
FINDSTRING("New York, NY, NY", "NY", 1)   
```  
  
 この例では、文字列リテラルを使用します。 文字列 "NY" は 2 回しか検出されないため、返される結果は 0 です。  
  
```  
FINDSTRING("New York, NY, NY", "NY", 3)   
```  
  
 この例では、 **Name** 列を使用します。 **Name** 列にある 2 番目の n の場所が返されます。 返される結果は、 **Name** の値によって異なります。 **Name** に Anderson が含まれる場合は、次の関数では 8 が返されます。  
  
```  
FINDSTRING(Name, "n", 2)   
```  
  
 この例では、 **Name** および **Size** 列を使用します。 **Name** 列にある **Size** の値の左端の文字の場所が返されます。 返される結果は、列の値によって異なります。 **Name** の値が Mountain,500Red,42 で **Size** の値が 42 の場合、17 が返されます。  
  
```  
FINDSTRING(Name,Size,1)   
```  
  
## <a name="see-also"></a>関連項目  
 [REPLACE &#40;SSIS &#41;](../../integration-services/expressions/replace-ssis-expression.md)   
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
