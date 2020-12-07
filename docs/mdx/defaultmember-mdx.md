---
description: DefaultMember (MDX)
title: DefaultMember (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7363d650073b301eba6b29d509590e22dee5661a
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196026"
---
# <a name="defaultmember-mdx"></a>DefaultMember (MDX)


  階層の既定のメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Hierarchy_Expression.DefaultMember  
```  
  
## <a name="arguments"></a>引数  
 *Hierarchy_Expression*  
 階層を返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>注釈  
 属性がクエリに含まれていない場合は、属性上の既定のメンバーが式の評価に使用されます。  
  
## <a name="example"></a>例  
 次の例では、 **DefaultMember** 関数を **Name** 関数と共に使用して、Adventure Works キューブの換算先通貨ディメンションの既定のメンバーを返します。 この例では、 **米ドル**が返されます。 **Name**関数は、メジャーの既定のプロパティではなく、**値**であるメジャーの名前を返すために使用されます。  
  
```  
WITH MEMBER Measures.x AS   
   [Destination Currency].[Destination Currency].DefaultMember.Name  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [Mdx 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [既定のメンバーの定義](/analysis-services/multidimensional-models/attribute-properties-define-a-default-member)  
  
