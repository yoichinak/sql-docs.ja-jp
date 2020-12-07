---
description: 演算子 (MDX 構文)
title: 演算子 (MDX 構文) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b9ad1f77a8e023d55a34e64d6c40ad956b0dac92
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193492"
---
# <a name="operators-mdx-syntax"></a>演算子 (MDX 構文)


  多次元式 (MDX) では、演算子を使用して以下の操作を実行できます。  
  
-   永続的または一時的にデータを変更します。  
  
-   指定された条件を満たす値またはオブジェクトを検索します。  
  
-   値または式の間に決定を実装します。  
  
-   トランザクションの開始やコミット、または特定のステートメントの実行の前に行う特定の条件に対する試験  
  
 MDX では、以下の表に示す演算子がサポートされます。  
  
|演算の種類|使用|  
|---------------------------------------|---------|  
|変数に値を割り当てるか、または結果セット列を別名に関連付けます。|[代入演算子](../mdx/assignment-operators.md)|  
|加算、減算、乗算、除算。|[算術演算子](../mdx/arithmetic-operators.md)|  
|AND、OR、NOT、XOR などの条件の真偽をテストします。|[ビット処理演算子 &、^、&#124;](../mdx/bitwise-operators.md)|  
|値を他の値または式と比較します。|[比較演算子](../mdx/comparison-operators.md)|  
|2 つの文字列を永続的または一時的に 1 つの文字列に結合します。|[連結演算子](../mdx/concatenation-operators.md)|  
|2つのセット式を1つのセットに永続的または一時的に結合します。|[集合演算子](../mdx/set-operators.md)|  
|1つのオペランドに対して演算を実行します。|[単項演算子](../mdx/unary-operators.md)|  
  
> [!NOTE]  
>  クエリ内では、特定の種類の演算子と共に使用するキューブのデータを読み取ることができるユーザーは演算を実行できます。 ただし、データを正常に変更するには、適切なアクセス許可が必要です。  
  
 複数の演算子を使用する場合は、MDX によって演算子が評価される順序が重要です。 同様に重要な点として、演算子を評価する前に、あるデータ型を別のデータ型に変換しておかなければならない場合もあります。  
  
## <a name="evaluating-complex-expressions"></a>複合式の評価  
 演算子を使用して式を作成すると、複数の小さい式を組み合わせることができます。 これらの複雑な式では、によって使用される演算子の優先順位の定義に基づいて、MDX によって演算子が評価され [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ます。 MDX は、優先順位の高い演算子を、優先順位の低い演算子より先に実行します。  
  
### <a name="understanding-operator-precedence"></a>演算子の優先順位について  
 次の一覧では、演算子の優先順位が高いものから順に表示されています。 同じ行に示されている演算子は優先順位が同じです。かっこによる強制的な優先がない限り、左から右の順に評価されます。  
  
-   IS  
  
-   AS  
  
-   DISTINCT  
  
-   :  
  
-   ^  
  
-   /, *  
  
-   +、-  
  
-   既存  
  
-   <>、>=、=、 \<=, > 、<  
  
-   NOT  
  
-   AND  
  
-   XOR  
  
-   OR  
  
 Mdx の演算子の詳細については、「mdx [演算子リファレンス &#40;mdx&#41;](../mdx/mdx-operator-reference-mdx.md)」を参照してください。  
  
### <a name="determining-results"></a>結果の確認  
 単純な式を結合して複雑な式を作成する場合、演算子に関する規則とデータ型の優先順位に関する規則の組み合わせによって、結果の値のデータ型が決まります。  
  
 結果が文字または Unicode 値の場合、演算子のルールと照合順序の優先順位に関するルールを組み合わせて、結果の照合順序を決定します。 照合順序の詳細については、「 [Analysis Services&#41;&#40;言語と照合順序 ](/analysis-services/languages-and-collations-analysis-services)」を参照してください。  
  
 また、単純式の有効桁数、小数点以下桁数、および長さに基づいて、結果の有効桁数、小数点以下桁数、および長さを決定するルールもあります。  
  
## <a name="converting-data-types"></a>データ型の変換  
 MDX では、あるオブジェクトが別のデータ型を必要とする式の中で使用されている場合、そのオブジェクトを別のデータ型へ暗黙的に変換します。 各オブジェクトは、次の表に示す規則に従って変換されます。  
  
|元の型|必要な型|変換|  
|-------------------|-----------------|----------------|  
|Level|オン|\<level>. メンバー|  
|Hierarchy|メンバー|\<hierarchy>. defaultmember|  
|メンバー|タプル|(\<Member>)|  
|タプル|メンバー|\<tuple>。 item (0)|  
|タプル|スカラー|\<tuple>. 値|  
  
## <a name="see-also"></a>参照  
 [Mdx 演算子リファレンス &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [MDX 構文の要素 &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
