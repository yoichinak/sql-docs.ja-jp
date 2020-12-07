---
description: 除算 (MDX)
title: 除算 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0999df34ff817131e890afade89fc5daad85796b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484015"
---
# <a name="divide-mdx"></a>除算 (MDX)


  除算を実行し、0 による除算の別の結果または BLANK() を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>引数  
 *分子*  
 被除数 (割られる数)。  
  
 *分母*  
 除数 (割る数)。  
  
 *alternateresult*  
 (省略可能) 0 による除算でエラーが発生したときに返される値です。 指定しない場合、既定値は BLANK() です。  
  
## <a name="remarks"></a>解説  
 0 による除算の別の結果は定数である必要があります。  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
