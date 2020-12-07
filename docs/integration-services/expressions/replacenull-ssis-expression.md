---
description: REPLACENULL (SSIS 式)
title: REPLACENULL (SSIS 式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 70db7832-b5a0-4db5-a8ad-42ad8630d8e8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f90bf0dfc2eba97d8a0c1b8b2e9bd7cdf8a0e565
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477464"
---
# <a name="replacenull-ssis-expression"></a>REPLACENULL (SSIS 式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  1 番目の式パラメーターの値が NULL の場合、2 番目の式パラメーターの値を返します。NULL でない場合は、1 番目の式の値を返します。  
  
## <a name="syntax"></a>構文  
  
```vb  
REPLACENULL(expression 1,expression 2)  
```  
  
## <a name="arguments"></a>引数  
 *expression 1*  
 この式の結果が NULL かどうかを調べます。  
  
 *expression 2*  
 1 番目の式が NULL と評価される場合、この式の結果が返されます。  
  
## <a name="result-types"></a>戻り値の型  
 DT_WSTR  
  
## <a name="remarks"></a>解説  
  
-   *expression 2* の長さは 0 にできます。  
  
-   いずれかの引数が NULL の場合、REPLACENULL は NULL を返します。  
  
-   BLOB 列 (DT_TEXT、DT_NTEXT、DT_IMAGE) は、いずれのパラメーターとしてもサポートされていません。  
  
-   2 つの式は、戻り値の型が同じであるものと想定されています。 同じでない場合は、2 番目の式が 1 番目の式の戻り値の型にキャストされ、データ型に互換性がない場合はエラーが発生する可能性があります。  
  
## <a name="expression-examples"></a>式の例  
 次の例では、データベース列の NULL 値を、文字列 (1900-01-01) に置き換えます。 この関数は、特に、NULL 値を他のなんらかの値に置き換える必要のある一般的な派生列パターンで使用されます。  
  
```  
REPLACENULL(MyColumn, "1900-01-01")  
```  
  
> [!NOTE]
>  次の例では、 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]/ [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]で行われていた方法を示します。  
  
```  
(DT_DBTIMESTAMP) (ISNULL(MyColumn) ? "1900-01-01" : MyColumn)   
```  
  
  
