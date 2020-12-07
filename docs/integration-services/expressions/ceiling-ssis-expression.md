---
description: CEILING (SSIS 式)
title: CEILING (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- smallest integer great than or equal to expression
- CEILING function [SSIS]
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 533cef6354c3dcea15146809a1f2466f342e60c9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457284"
---
# <a name="ceiling-ssis-expression"></a>CEILING (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  数値式以上で最小の整数値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CEILING(numeric_expression)  
```  
  
## <a name="arguments"></a>引数  
 *numeric_expression*  
 有効な数値式です。  
  
## <a name="result-types"></a>戻り値の型  
 関数に送信された数値式のデータ型です。  
  
## <a name="remarks"></a>注釈  
 引数が NULL の場合、CEILING は NULL を返します。  
  
## <a name="expression-examples"></a>式の例  
 この例では、正の値、負の値、および 0 に CEILING 関数を適用します。  
  
```  
CEILING(123.74)  
```  
  
 124.00 を返します。  
  
```  
CEILING(-124.27)  
```  
  
 -124.00 を返します  
  
```  
CEILING(0.00)  
```  
  
 0.00 を返します。  
  
## <a name="see-also"></a>関連項目  
 [FLOOR &#40;SSIS 式&#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [関数 (SSIS 式)](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
