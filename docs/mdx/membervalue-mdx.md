---
description: MemberValue (MDX)
title: MemberValue (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aaa7592c5f2d3413a63fbc0867bb8857e5d87d73
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483795"
---
# <a name="membervalue-mdx"></a>MemberValue (MDX)


  メンバーの値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Member_Expression.MemberValue  
```  
  
## <a name="arguments"></a>引数  
 *Member_Expression*  
 メンバーに評価される有効な多次元式 (MDX) 式です。  
  
## <a name="return-value"></a>戻り値  
 返されるメンバーの値には、次の情報が含まれています。この情報は、戻り値に表示される順序で示されています。  
  
-   値のバインド (定義されている場合)。  
  
-   名前のバインドが存在しない場合、またはキーとキャプションが同じ列にバインドされている場合は、元のデータ型のキー。  
  
-   メンバーのキャプション。  
  
## <a name="example"></a>例  
 次の例では、Adventure Works キューブ内の Date ディメンションの最初の日付の値のバインド、メンバー キー、およびキャプションを返します。  
  
```  
WITH MEMBER Measures.ValueColumn as [Date].[Calendar].[July 1, 2001].MemberValue  
MEMBER Measures.KeyColumn as [Date].[Calendar].[July 1, 2001].Member_Key  
MEMBER Measures.NameColumn as [Date].[Calendar].[July 1, 2001].Member_Name  
  
SELECT {Measures.ValueColumn, Measures.KeyColumn, Measures.NameColumn}  ON 0  
from [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
