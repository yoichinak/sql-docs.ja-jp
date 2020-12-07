---
description: Error (MDX)
title: エラー (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f95ee71586f5571d91221fe8889198a44a1252b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494925"
---
# <a name="error-mdx"></a>Error (MDX)


  指定されたエラーメッセージを提供して、オプションでエラーを生成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Error( [ Error_Text ] )  
```  
  
## <a name="arguments"></a>引数  
 *Error_Text*  
 返すエラー メッセージを格納した有効な文字列式です。  
  
## <a name="examples"></a>例  
 次のクエリは、計算されるメジャー内で **Error** 関数を使用する方法を示しています。  
  
 `WITH MEMBER MEASURES.ERRORDEMO AS ERROR("THIS IS AN ERROR")`  
  
 `SELECT`  
  
 `MEASURES.ERRORDEMO ON 0`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
