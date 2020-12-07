---
description: MeasureGroupMeasures (MDX)
title: MeasureGroupMeasures (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3adb11cd39e5a85e498f9b04ac714385d944c48a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483835"
---
# <a name="measuregroupmeasures-mdx"></a>MeasureGroupMeasures (MDX)


  指定されたメジャーグループに属するメジャーのセットを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
MEASUREGROUPMEASURES(MeasureGroupName)  
```  
  
## <a name="arguments"></a>引数  
 *MeasureGroupName*  
 メジャーのセットの取得元となるメジャー グループの名前が格納されている有効な文字列式です。  
  
## <a name="remarks"></a>解説  
 指定する文字列は、メジャー グループの名前と正確に一致する必要があります。 スペースを含むメジャー グループ名を角かっこで囲む必要はありません。  
  
## <a name="example"></a>例  
 次の例では、Adventure Works キューブの Internet Sales メジャーグループに含まれるすべてのメジャーを返します。  
  
```  
SELECT MeasureGroupMeasures('Internet Sales') ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
