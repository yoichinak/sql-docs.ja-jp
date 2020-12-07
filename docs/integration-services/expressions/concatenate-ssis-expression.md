---
description: + (連結) (SSIS 式)
title: + (連結) (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- concatenation [Integration Services]
- + (concatenate operator)
- concatenate operator (+)
ms.assetid: 0fed6334-7a4f-42dc-a611-191fcaa0e443
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8ea4ea990ab0bfc07c7861c0e79f90bca124de22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457249"
---
# <a name="-concatenate-ssis-expression"></a>+ (連結) (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  2 つの式を連結して 1 つの式にします。  
  
## <a name="syntax"></a>構文  
  
```  
  
character_expression1 + character_expression2  
  
```  
  
## <a name="arguments"></a>引数  
 *expression1、expression2*  
 データ型が DT_STR、DT_WSTR、DT_TEXT、DT_NTEXT、または DT_IMAGE である、任意の有効な式です。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>解説  
 この式では、DT_STR データ型および DT_WSTR データ型のいずれか一方、または両方を使用できます。  
  
 DT_STR データ型と DT_WSTR データ型を連結すると、DT_WSTR データ型の結果が返されます。 文字列の長さは、元の文字列の長さを文字数で表した値の合計です。  
  
 文字列データ型 DT_STR および DT_WSTR、または Binary Large Object Block (BLOB) データ型 DT_TEXT、DT_NTEXT、および DT_IMAGE のデータのみが連結できます。 その他のデータ型は、これらのデータ型のいずれかに明示的に変換してから連結する必要があります。 データ型間の有効なキャストについて詳しくは、「[Cast &#40;SSIS 式&#41;](../../integration-services/expressions/cast-ssis-expression.md)」をご覧ください。  
  
 両方の式のデータ型は同じであるか、または一方の式をもう一方の式のデータ型に暗黙的に変換できる必要があります。 たとえば、文字列 "Order date is" と列 **OrderDate** を連結する場合、 **OrderDate** の値は暗黙的に文字列データ型に変換されます。 2 つの数値を連結するには、両方の数値を文字列データ型に明示的にキャストする必要があります。  
  
 BLOB データ型を連結する場合、DT_TEXT、DT_NTEXT、または DT_IMAGE のいずれか 1 つのみを連結できます。  
  
 要素のいずれかが NULL の場合、結果は NULL になります。  
  
 文字列リテラルは引用符で囲まれている必要があります。  
  
## <a name="expression-examples"></a>式の例  
 この例では、 **FirstName** 列と **LastName** 列の値を連結し、値の間にスペースを挿入します。  
  
```  
FirstName + ' ' + LastName  
```  
  
 この例では、変数 **ZIPCode** と変数 **ZIPCode+4**を連結します。 どちらの変数も文字列データ型です。 **ZIPCode+4** は、変数名にプラス記号 (+) が含まれているため、角かっこで囲む必要があります。  
  
```  
@ZIPCcode + "-" + @[ZipCode+4]  
```  
  
## <a name="see-also"></a>関連項目  
 [演算子の優先順位と結合規則](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [演算子 &#40;SSIS 式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
