---
description: ABS (SSIS 式)
title: ABS (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- ABS function
- absolute positive value
ms.assetid: 156747f6-e016-44cf-9a9f-ae8e4a1b4f17
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cc19d31e89795ab2af731deac610656e61f61062
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88391338"
---
# <a name="abs-ssis-expression"></a>ABS (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  数値式の正の絶対値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
ABS(numeric_expression)  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 符号付きまたは符号なしの数値式です。  
  
## <a name="result-types"></a>戻り値の型  
 関数に送信された数値式のデータ型です。  
  
## <a name="remarks"></a>注釈  
 引数が NULL の場合、ABS は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 次の例では、正の数および負の数に ABS 関数を適用します。 どちらも 1.23 を返します。  
  
```  
ABS(-1.23)  
ABS(1.23)  
```  
  
 この例では、変数 **HighTemperature** および **LowTempature**の値を減算する式に対して ABS 関数を適用します。  
  
```  
ABS(@HighTemperature - @LowTemperature)  
```  
  
## <a name="see-also"></a>参照  
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
