---
description: CustomData (MDX)
title: CustomData (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ed7bfe2841caf9bd5b2c6e6caf102323db6d62ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88413168"
---
# <a name="customdata-mdx"></a>CustomData (MDX)


  **CustomData**接続文字列プロパティの値を返します (定義されている場合)。それ以外の場合は**null**。  
  
## <a name="syntax"></a>構文  
  
```  
  
CustomData()  
```  
  
## <a name="return-value"></a>戻り値  
 **CustomData**関数は、 **CustomData**接続文字列プロパティを取得し、多次元式 (mdx) 関数およびステートメント (Mdx) や[CALL ステートメント (mdx](../mdx/mdx-data-manipulation-call.md) [) などの](../mdx/username-mdx.md)ステートメントで使用される構成設定を渡すことができます。 たとえば、この関数を動的セキュリティ式で使用すると、 **CustomData** 接続文字列プロパティの文字列値に対して許可または拒否されたセットメンバーを選択できます。  
  
## <a name="example"></a>例  
 次のクエリでは、計算されるメジャーで **CustomData** 関数によって返される値が表示されます。  
  
```  
WITH MEMBER [Measures].CUSTOMDATADEMO AS CUSTOMDATA()  
SELECT [Measures].CUSTOMDATADEMO ON 0  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
