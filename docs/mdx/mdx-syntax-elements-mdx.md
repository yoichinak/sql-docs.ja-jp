---
description: MDX 構文の要素 (MDX)
title: MDX 構文の要素 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 27755806802e5238329b4a9ecb49e6a9f6ad5ce2
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196942"
---
# <a name="mdx-syntax-elements-mdx"></a>MDX 構文の要素 (MDX)


  多次元式 (MDX) には、以下に示すような、ほとんどのステートメントで使用される要素、およびほとんどのステートメントに影響を与える要素があります。  
  
|用語|定義|  
|----------|----------------|  
|[識別子](../mdx/identifiers-mdx.md)|識別子は、キューブ、ディメンション、メンバー、メジャーなどのオブジェクトの名前です。|  
|**Data Types (データ型)**|セル、メンバープロパティ、およびセルプロパティに含まれるデータの種類を定義します。 MDX は OLE VARIANT データ型だけをサポートします。 VARIANT データ型の強制型変換、変換、および操作の詳細については、プラットフォーム SDK ドキュメントの「VARIANT と VARIANTARG」を参照してください。|  
|[MDX &#40;式&#41;](../mdx/expressions-mdx.md)|式は、Analysis Services が単一の (スカラー) 値またはオブジェクトに解決できる構文の単位です。 式には、単一値、セット式などを返す関数も含まれます。|  
|[オペレーター](../mdx/operators-mdx-syntax.md)|演算子は、1つまたは複数の単純な MDX 式を使用して、より複雑な MDX 式を作成する構文要素です。|  
|[関数](../mdx/functions-mdx-syntax.md)|関数とは、0 個以上の入力値を受け入れてスカラー値またはオブジェクトを返す構文要素です。 例としては、複数の値を追加するための [Sum](../mdx/sum-mdx.md) 関数、ディメンションまたはレベルからメンバーのセットを返す [メンバー](../mdx/members-set-mdx.md) 関数などがあります。|  
|[コメント](../mdx/comments-mdx-syntax.md)|コメントは、ステートメントの目的を説明するために MDX ステートメントまたはスクリプトに挿入されるテキストです。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] コメントは実行されません。|  
|[予約済みキーワード](../mdx/reserved-keywords-mdx-syntax.md)|予約済みキーワードは、MDX を使用するために予約されている単語であり、MDX ステートメントで使用されるオブジェクト名には使用できません。|  
|[メンバー、組、セット](/analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx)|メンバー、組、およびセットは多次元データの主要概念であり、MDX クエリを作成する前に理解しておく必要があります。|  
  
## <a name="see-also"></a>参照  
 [多次元式 &#40;MDX&#41; リファレンス](../mdx/multidimensional-expressions-mdx-reference.md)  
  
