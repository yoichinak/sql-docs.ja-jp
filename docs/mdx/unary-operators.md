---
description: 単項演算子
title: 単項演算子 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 391b39dd92011ce43b146d740b232d0c4fca6669
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193482"
---
# <a name="unary-operators"></a>単項演算子


  多次元式 (MDX) において、単項演算子は単一のオペランドに対する操作を実行します (たとえば、数値式の負または正の値を返します)。  
  
 MDX では、以下の表に示す単項演算子がサポートされます。  
  
|演算子|説明|  
|--------------|-----------------|  
|[- (負号)](../mdx/negative-mdx.md)|数値式の負の値を返します。|  
|[+ (正号)](../mdx/positive-mdx.md)|数値式の正の値を返します。|  
  
 次の例は、単項演算子を使用してメジャーの負の値を返す方法を示しています。  
  
```  
WITH   
   MEMBER [Measures].[NegDiscountAmount] AS  
   -[Measures].[Discount Amount]  
SELECT   
   {[Measures].[Discount Amount],[Measures].[NegDiscountAmount]} on COLUMNS,  
   NON EMPTY [Product].[Product].MEMBERS  ON Rows  
FROM [Adventure Works]  
WHERE [Product].[Category].[Bikes]  
```  
  
 さらに、MDX では、特別な単項演算子を使用して、 [Rollupchildren](../mdx/rollupchildren-mdx.md) 関数によって実行される集計操作を決定します。 これらの特別な単項演算子の詳細については、「 [ディメンションへのカスタム集計の追加](/analysis-services/multidimensional-models/bi-wizard-add-a-custom-aggregation-to-a-dimension)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [MDX 構文 &#40;の演算子&#41;](../mdx/operators-mdx-syntax.md)  
  
