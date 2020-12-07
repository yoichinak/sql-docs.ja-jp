---
description: MDX データ操作 - CREATE CELL CALCULATION
title: CREATE CELL CALCULATION ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 94f2a2286b72aac5a8698fad7ba0085f2a6ad8d0
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196999"
---
# <a name="mdx-data-definition---create-cell-calculation"></a>MDX データ操作 - CREATE CELL CALCULATION


  キューブ内の指定された組のセットに対して多次元式 (MDX) 式を評価する計算を作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
[WITH <CELL CALCULATION clause> Calculation_Name  
   [,WITH <CELL CALCULATION clause> Calculation_Name...n]  
CREATE CELL CALCULATION CURRENTCUBE | Cube_Name.Calculation_Name   
  
<CELL CALCULATION clause> ::=  
   FOR Set_Expression AS 'MDX_Expression'   
      [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブ名を提供する有効な文字列です。  
  
 *Calculation_Name*  
 セルの計算名を提供する有効な文字列です。  
  
 *Set_Expression*  
 セットを返す有効な MDX 式です。  
  
 *String*  
 有効な文字列値。  
  
 *MDX_Expression*  
 有効な MDX 式です。  
  
 *Logical_Expression*  
 有効な MDX 論理式です。  
  
 *整数*  
 有効な整数値。  
  
 *Calculation_Name*  
 セル計算プロパティの名前を提供する有効な文字列です。  
  
 *Scalar_Expression*  
 有効な MDX スカラー式です。  
  
## <a name="remarks"></a>注釈  
 クライアントアプリケーションでは、計算されるセルを使用することによって、カスタムロールアップ式や計算されるメンバーの場合と同様に、セルのセット全体ではなく、特定のセルのセットに対してロールアップ値を指定できます。 たとえば、`{[Canada],[Time].[2000]}` によって定義されるセット内のセルに、特定の式によって定義される値を入れる、といった指定が可能です。 このセット内に含まれていないその他のセルは、通常どおりに計算されます。  
  
> [!NOTE]  
>  の Backus-Naur フォーム (BNF) は、 `{*(<comment> | <whitespace> | <newline>)}` `{*}` 下位互換性のためにとして解析されます。  
  
## <a name="see-also"></a>参照  
 [計算されるセルの作成 Session-Scoped](/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-session-scoped-calculated-cells)   
 [MDX&#41;&#40;のセル計算の作成 Query-Scoped ](/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-query-scoped-cell-calculations)   
 [Mdx &#40;MDX でのセル計算の作成&#41;](/analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations)   
 [MDX&#41;&#40;のセルプロパティの使用 ](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties)   
 [MDX&#41;&#40;のコンテンツの FORMAT_STRING ](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents)   
 [MDX&#41;&#40;コンテンツの FORE_COLOR と BACK_COLOR ](/analysis-services/multidimensional-models/mdx/mdx-cell-properties-fore-color-and-back-color-contents)   
 [Mdx&#41;&#40;mdx データ定義ステートメント ](../mdx/mdx-data-definition-statements-mdx.md)  
  
