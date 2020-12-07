---
description: 比較演算子
title: 比較演算子 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 2f1dcb77c15e540a740ac9956dc4c547c5ca61c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387670"
---
# <a name="comparison-operators"></a>比較演算子


  比較演算子は、スカラー データと共に使用します。 比較演算子は、任意の多次元式 (MDX) 式で使用できます。  
  
 条件を確認するために、mdx のステートメントや関数 (MDX [IIf](../mdx/iif-mdx.md) 関数など) で比較演算子を使用することもできます。 ただし、条件を満たしているかどうかを調べるために比較演算子を使用する場合は、その条件に基づいてデータの変更を試みる前に、適切な権限を持っていることを確認してください。 実際のデータへのアクセス権を持ち、そのデータにクエリを実行するすべてのユーザーは、追加のクエリで比較演算子を使用できます。 しかし、このようにアクセスできることは、それらのユーザーがデータを変更するための適切な権限を持っている、あるいは持つ必要があるという意味ではありません。 また、データの整合性を維持するためにも、データに対してクエリを実行してデータを変更できるユーザーの数は制限してください。  
  
 比較演算子は、ブールデータ型に評価され、テストされた条件の結果に基づいて TRUE または FALSE を返します。  
  
 MDX では、次の表に示す比較演算子がサポートされています。  
  
|演算子|説明|  
|--------------|-----------------|  
|[= (等しい)](../mdx/equal-to-mdx.md)|Null 以外の引数については、左の引数が右の引数と等しい場合に TRUE を返します。それ以外の場合は FALSE。<br /><br /> いずれかまたは両方の引数が null 値に評価される場合、比較が行われない限り、演算子は null 値を返し `0=null` ます。この場合、ブール値は TRUE を含みます。|  
|[<>  (等しくない)](../mdx/not-equal-to-mdx.md)|Null 以外の引数については、左の引数が右の引数と等しくない場合に TRUE を返します。それ以外の場合は FALSE。<br /><br /> いずれかまたは両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[> (より大きい)](../mdx/greater-than-mdx.md)|Null 以外の引数については、左の引数の値が右の引数の値よりも大きい場合に TRUE を返します。それ以外の場合は FALSE。<br /><br /> いずれかまたは両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[>= (以上)](../mdx/greater-than-or-equal-to-mdx.md)|NULL 以外の引数について、左の引数の値が右の引数の値以上である場合に TRUE を返します。そうでない場合は、FALSE を返します。<br /><br /> いずれかまたは両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[< (より小さい)](../mdx/less-than-mdx.md)|Null 以外の引数については、左の引数の値が右の引数の値より小さい場合に TRUE を返します。それ以外の場合は FALSE。<br /><br /> いずれかまたは両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
|[<= (以下)](../mdx/less-than-or-equal-to-mdx.md)|NULL 以外の引数について、左の引数の値が右の引数の値以下である場合に TRUE を返します。そうでない場合は、FALSE を返します。<br /><br /> いずれかまたは両方の引数が null 値に評価される場合、演算子は null 値を返します。|  
  
## <a name="see-also"></a>参照  
 [Mdx 演算子リファレンス &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [MDX 構文 &#40;の演算子&#41;](../mdx/operators-mdx-syntax.md)  
  
  
