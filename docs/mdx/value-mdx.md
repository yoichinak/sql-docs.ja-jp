---
description: Value (MDX)
title: 値 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 52224625f5e2e6fc70ca9a76f750ed374108c52c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196730"
---
# <a name="value-mdx"></a>Value (MDX)


  クエリのコンテキストで、属性階層の現在のメンバーと交差する、Measures ディメンションの現在のメンバーの値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression[.Value]   
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーを 1 つ返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>注釈  
 **Value**関数は、指定されたメンバーの値を文字列として返します。 **Value**引数は省略可能です。これは、メンバーの値がメンバーの既定のプロパティであり、他の値が指定されていない場合にメンバーに対して返される値であるためです。 メンバーのプロパティの詳細については、「 [mdx&#41;&#40;の固有メンバープロパティ ](/analysis-services/multidimensional-models/mdx/mdx-member-properties-intrinsic-member-properties) 」および「 [Mdx&#41;&#40;ユーザー定義メンバープロパティ ](/analysis-services/multidimensional-models/mdx/mdx-member-properties-user-defined-member-properties)」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、明示的にメンバーの名前を返すだけでなく、メンバーの値も返します。  
  
```  
WITH MEMBER [Date].[Calendar].NumericValue as [Date].[Calendar].[July 1, 2001].Value  
MEMBER [Date].[Calendar].MemberName AS [Date].[Calendar].[July 1, 2001].Name  
  
SELECT {[Date].[Calendar].NumericValue, [Date].[Calendar].MemberName} ON 0  
from [Adventure Works]  
```  
  
 次の例では、軸上のメンバーに対して返される既定値として、メンバーの値を返します。  
  
```  
SELECT {[Date].[Calendar].[July 1, 2001]} ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MemberValue &#40;MDX&#41;](../mdx/membervalue-mdx.md)   
 [MDX&#41;&#40;プロパティ ](../mdx/properties-mdx.md)   
 [MDX&#41;&#40;名前 ](../mdx/name-mdx.md)   
 [UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
