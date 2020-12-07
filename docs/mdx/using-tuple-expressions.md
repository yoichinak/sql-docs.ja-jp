---
description: 組式の使用
title: タプル式を使用する |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0dfba7ed88a27c7cdcc56ff29861d593cca33e91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494845"
---
# <a name="using-tuple-expressions"></a>組式の使用


  組は、キューブ内に含まれるすべてのディメンションの1つのメンバーで構成されます。 したがって、タプルはキューブ内の1つのセルを一意に識別します。  
  
> [!NOTE]  
>  有効でない 1 つ以上のメンバーを参照する組は、空の組と呼ばれます。  
  
 組識別子の完全な式は、かっこで囲まれた1つ以上の明示的に指定されたメンバーで構成されます。  
  
 (*Member_expression* [、*Member_expression* ...])  
  
 タプルは完全修飾することも、暗黙的なメンバーを含めることもできます。また、1つのメンバーを含めることもできます。  
  
## <a name="tuples-and-implicit-members"></a>組と暗黙的なメンバー  
 キューブ内に含まれるすべてのディメンションの1つのメンバーを明示的に指定する組は、完全修飾タプルと呼ばれます。 ただし、すべての組が完全に修飾されている必要はありません。  
  
 タプル内で明示的に参照されていないディメンションは、暗黙的に参照されます。 暗黙的に参照されたディメンションのメンバーは、ディメンションの構造とその中で定義されている属性リレーションシップによって異なります。 暗黙的に参照される階層と同じディメンション上の階層への明示的な参照が存在し、明示的に参照されている階層と暗黙的に参照される階層の間に直接または間接リレーションシップが定義されている場合、タプルは、明示的に参照されている階層のメンバーと共に存在する、暗黙的に参照される階層 たとえば、City 属性および Country 属性を持つ Customer ディメンションがキューブに含まれており、これら 2 つの属性間でリレーションシップが定義され、City に 1 つの Country が含まれ、Country に複数の City を含めることができるようになっている場合、明示的に City 'London' を組に含めると、Country 'United Kingdom' が暗黙的に参照されます。 ただし、属性リレーションシップが定義されておらず、リレーションシップの方向が逆になっている場合 (たとえば、City に Country とのリレーションシップがあっても、ある人が住んでいる Country がわかるだけで、住んでいる City を特定できない場合) や 2 つの属性間で直接的なリレーションシップが定義されていない場合 (たとえば、Customer から City へのリレーションシップと Customer から Country へのリレーションシップが定義されていても、City と Country 間のリレーションシップが定義されていない場合) は、次の規則が適用されます。  
  
-   暗黙的に参照される階層に既定のメンバーがある場合は、既定のメンバーが組に追加されます。  
  
-   暗黙的に参照される階層に既定のメンバーがない場合は、既定の階層の **(All)** メンバーが使用されます。  
  
-   暗黙的に参照される階層に既定のメンバーがない場合は、階層の最上位レベルの最初のメンバーが使用されます。  
  
## <a name="one-member-tuples"></a>1つのメンバーの組  
 組式に1つのメンバーが含まれている場合、MDX は、式を評価するためにメンバーを1つのメンバーのタプルに変換します。 つまり、組式の代わりにメンバー式 `[Measures].[TestMeasure]` を使用することは、組式 `( [Measures].[TestMeasure] ).` と機能的に等価です。  
  
## <a name="see-also"></a>参照  
 [MDX &#40;式&#41;](../mdx/expressions-mdx.md)   
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
