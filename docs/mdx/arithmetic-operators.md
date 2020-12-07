---
description: 算術演算子
title: 算術演算子 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 995e7ce1cb6a3c5d06db1042c00f945ec01e1be6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494995"
---
# <a name="arithmetic-operators"></a>算術演算子


  多次元式 (MDX) では、加算、減算、乗算、除算などの算術演算に算術演算子を使用できます。  
  
 MDX では、以下の表に示す算術演算子がサポートされます。  
  
|演算子|説明|  
|--------------|-----------------|  
|[+ (加算)](../mdx/add-mdx.md)|2 つの値を加算します。|  
|[/ (除算)](../mdx/divide-mdx-operator-reference.md)|1つの数値を別の数値で除算します。|  
|[* (乗算)](../mdx/multiply-mdx.md)|2 つの値を乗算します。|  
|[- (減算)](../mdx/subtract-mdx.md)|2 つの値の間で減算をします。|  
|^ (Power)|1つの数値を別の数値で累乗します。|  
  
> [!NOTE]  
>  MDX には、数値の平方根を取得する関数は含まれていません。 数値の平方根を取得するには、^ 演算子を使用してその数値を 0.5 で累乗してください。  
  
## <a name="order-of-precedence"></a>優先順位  
 MDX 式内での算術演算子の優先順位は、以下の規則によって決まります。  
  
-   式に複数の算術演算子がある場合、MDX は最初に乗算と除算を実行し、次に減算と加算を実行します。  
  
-   式のすべての算術演算子の優先順位が同じである場合、実行の順序は左から右になります。  
  
-   かっこの中の式は、他のどの操作よりも優先されます。  
  
## <a name="see-also"></a>参照  
 [Mdx 演算子リファレンス &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [MDX 構文 &#40;の演算子&#41;](../mdx/operators-mdx-syntax.md)  
  
  
