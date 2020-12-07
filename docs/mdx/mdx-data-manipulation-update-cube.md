---
description: MDX データ操作 - UPDATE CUBE
title: UPDATE CUBE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e4ee6d69057745486ed72f00721f9ab38833ca2e
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196977"
---
# <a name="mdx-data-manipulation---update-cube"></a>MDX データ操作 - UPDATE CUBE


  UPDATE CUBE ステートメントは、SUM 集計によって親に対して集計を行うキューブ内の任意のセルにデータを書き戻すために使用します。 詳細と例については、このブログの投稿「 [Analysis Services を使用した書き戻しアプリケーションの構築 (ブログ)](/archive/blogs/data_otaku/building-a-writeback-application-with-analysis-services)」の「割り当てについて」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
UPDATE [ CUBE ] Cube_Name   
   SET   
            <update clause>   
           [, <update clause> ...n ]  
  
<update clause> ::=   
      Tuple_Expression[.VALUE]= New_Value  
      [   
        USE_EQUAL_ALLOCATION   
        | USE_EQUAL_INCREMENT   
        | USE_WEIGHTED_ALLOCATION [ BY Weight_Expression]   
        | USE_WEIGHTED_INCREMENT [ BY Weight_Expression]  
      ]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブの名前を指定する有効な文字列です。  
  
 *Tuple_Expression*  
 組を返す有効な多次元式 (MDX) 式です。  
  
 *New_Value*  
 有効な数値式です。  
  
 *Weight_Expression*  
 0 ～ 1 の範囲の 10 進値を返す有効な多次元式 (MDX) 数値式です。  
  
## <a name="remarks"></a>注釈  
 キューブ内の指定されたリーフ セルまたは非リーフ セルの値を更新できます。指定された非リーフ セルの値を、それに依存するすべてのリーフ セルに割り当てることもできます。 組式で指定されるセルは、多次元空間内の任意の有効なセルにすることができます (つまり、セルはリーフセルである必要はありません)。 ただし、セルは [Sum](../mdx/sum-mdx.md) 集計関数を使用して集計する必要があり、セルの識別に使用される組には計算されるメンバーを含めないでください。  
  
 **UPDATE CUBE**ステートメントは、指定された合計にロールアップされるリーフセルと非リーフセルに対して、一連の個別のセルの書き戻し操作を自動的に生成するサブルーチンと考えると役に立つ場合があります。  
  
 次に、割り当ての方法の説明を示します。  
  
 **USE_EQUAL_ALLOCATION:** 更新されたセルに貢献するすべてのリーフセルには、次の式に基づいて等しい値が割り当てられます。  
  
```  
<leaf cell value> =   
<New Value> / Count(leaf cells that are contained in <tuple>)  
```  
  
 **USE_EQUAL_INCREMENT:** 更新されたセルに貢献するすべてのリーフセルは、次の式に従って変更されます。  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value > - <existing value>) /  
Count(leaf cells contained in <tuple>)  
```  
  
 **USE_WEIGHTED_ALLOCATION:** 更新されたセルに貢献するすべてのリーフセルには、次の式に基づく等しい値が割り当てられます。  
  
```  
<leaf cell value> = < New Value> * Weight_Expression  
```  
  
 **USE_WEIGHTED_INCREMENT:** 更新されたセルに貢献するすべてのリーフセルは、次の式に従って変更されます。  
  
```  
<leaf cell value> = <leaf cell value> +   
(<New Value> - <existing value>)  * Weight_Expression  
```  
  
 重み式が指定されていない場合、 **UPDATE CUBE** ステートメントは暗黙的に次の式を使用します。  
  
```  
Weight_Expression = <leaf cell value> / <existing value>  
```  
  
 重み式は、0 ~ 1 の10進値として表す必要があります。 この値には、割り当て対象となるリーフ セルに割り当てる値の比率を指定します。 クライアント アプリケーションのプログラマは、式の割り当て値とロールアップ集計値が等しくなるように式を作成する必要があります。  
  
> [!CAUTION]  
>  クライアントアプリケーションは、正しくないロールアップ値やデータの不整合などの予期しない結果を回避するために、すべてのディメンションの割り当てを同時に検討する必要があります。  
  
 各 **更新キューブ** の割り当ては、トランザクションのためにアトミックであると見なす必要があります。 つまり、数式のエラーやセキュリティ違反など、何かの理由でいずれかの割り当て操作が失敗すると、UPDATE CUBE 操作全体が失敗します。 個々の割り当て操作の計算が処理される前に、データのスナップショットが作成され、計算結果が正しいかどうかの確認が行われます。  
  
> [!CAUTION]  
>  USE_WEIGHTED_ALLOCATION メソッドは、整数を含むメジャーで使用する場合、増分丸めの変更によって発生する不正確な結果を返すことができます。  
  
> [!IMPORTANT]  
>  更新されるセルが重ならない場合は、 **Update Isolation Level** 接続文字列プロパティを使用して、UPDATE CUBE のパフォーマンスを向上させることができます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>   
 [Mdx&#41;&#40;MDX データ操作ステートメント ](../mdx/mdx-data-manipulation-statements-mdx.md)  
  
