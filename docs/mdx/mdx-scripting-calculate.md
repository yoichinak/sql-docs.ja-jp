---
description: CALCULATE ステートメント (MDX)
title: CALCULATE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ff995f08ffef27abca65db10ff2cd38f2dd01e95
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196966"
---
# <a name="mdx-scripting---calculate"></a>MDX スクリプティング - CALCULATE


  キューブの各セルに集計値を格納します。  
  
## <a name="syntax"></a>構文  
  
```  
  
CALCULATE  
```  
  
## <a name="arguments"></a>引数  
 なし  
  
## <a name="remarks"></a>解説  
 を使用してキューブを作成すると、CALCULATE ステートメントがキューブの MDX スクリプトの最初のステートメントとして自動的に含まれ [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ます。 CALCULATE ステートメントは、キューブの各セルに対して、粒度の低いセルから集計を行うよう指定します。 セルの集計後、式を使用して粒度の低いセルに値を設定すると、粒度の高いセルの集計値に反映されます。 通常はこの集計をそのまま使用しますが、CALCULATE ステートメントを削除することも、先に他のステートメントを実行することもできます。  
  
 CALCULATE ステートメントは、MDX スクリプト内の入れ子になったサブキューブに含めることはできません。 入れ子になったサブキューブは、SCOPE ステートメントを使用して定義されます。 SCOPE ステートメントの詳細については、「 [Scope ステートメント &#40;MDX&#41;](../mdx/mdx-scripting-scope.md)」を参照してください。  
  
> [!NOTE]  
>  計算されるメンバーは集計されません。  
  
## <a name="see-also"></a>参照  
 [Mdx&#41;&#40;MDX スクリプトステートメント ](../mdx/mdx-scripting-statements-mdx.md)   
 [MDX スクリプティングの基礎 &#40;Analysis Services&#41;](/analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services)   
 [割り当てとその他のスクリプト コマンドの定義](/analysis-services/multidimensional-models/define-assignments-and-other-script-commands)  
  
