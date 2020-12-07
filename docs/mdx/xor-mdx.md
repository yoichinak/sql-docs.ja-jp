---
description: XOR (MDX)
title: XOR (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b74d4ec3d92469dc0372218bfe66375c0844384e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421876"
---
# <a name="xor-mdx"></a>XOR (MDX)


  2つの数値式に対して論理的な除外を実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Expression1 XOR Expression2  
  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Expression1*  
 数値を返す有効な多次元式 (MDX) 式です。  
  
 *Expression2*  
 数値を返す有効な MDX 式です。  
  
## <a name="return-value"></a>戻り値  
 1つの引数だけが**true**と評価される場合に**True**を返すブール値です。それ以外の場合は**false**。  
  
## <a name="remarks"></a>解説  
 **XOR**演算子は、両方のパラメーターをブール値として処理した後 (0 は**false**、それ以外の場合は**true**)、演算子が論理的な除外を実行します。 次の表は、 **XOR** 演算子が論理的な除外を実行する方法を示しています。  
  
|*Expression1*|*Expression2*|戻り値|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**false**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="see-also"></a>参照  
 [Mdx 演算子リファレンス &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
