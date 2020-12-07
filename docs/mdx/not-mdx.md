---
description: NOT (MDX)
title: NOT (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6c0cfa43896457397f2e2e08bac0b3de1d61e73f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471784"
---
# <a name="not-mdx"></a>NOT (MDX)


  数値式の論理否定を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
NOT Expression1  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Expression1*  
 数値を返す有効な多次元式 (MDX) 式です。  
  
## <a name="return-value"></a>戻り値  
 引数が**true**に評価された場合に**False**を返すブール値です。それ以外の場合は**true**です。  
  
## <a name="remarks"></a>解説  
 **Not**演算子は、演算子が論理否定を実行する前に、式をブール値 (0、0、 **false**、それ以外の場合は**true**) として扱います。 次の表は、 **not** 演算子が論理否定を実行する方法を示しています。  
  
|*Expression1*|戻り値|  
|-------------------|------------------|  
|**true**|**false**|  
|**false**|**true**|  
  
## <a name="see-also"></a>参照  
 [Mdx 演算子リファレンス &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
