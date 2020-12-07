---
description: MDX データ操作 - DROP MEMBER
title: DROP MEMBER ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f71232997c24a1bdca9a1294a804e8b30660d704
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483855"
---
# <a name="mdx-data-definition---drop-member"></a>MDX データ操作 - DROP MEMBER


  計算されるメンバーを削除します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DROP MEMBER   
   CURRENTCUBE | Cube_Name  
      .Member_Name   
               [,CURRENTCUBE | Cube_Name.Member_Name ...n]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブ名を提供する有効な文字列式です。  
  
 *Member_Identifier*  
 メンバー名またはメンバーキーを提供する有効な文字列式です。  
  
## <a name="see-also"></a>参照  
 [CREATE MEMBER ステートメント &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [Mdx&#41;&#40;mdx データ定義ステートメント ](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
