---
description: SCOPE ステートメント (MDX)
title: SCOPE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4c9f6738b2d7e0764e750b25f09001b7e9d3864a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483865"
---
# <a name="mdx-scripting---scope"></a>MDX スクリプティング - SCOPE


  指定された多次元式 (MDX) ステートメントのスコープを指定されたサブキューブに限定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
SCOPE(Subcube_Expression)   
   [ MDX_Statement ]  
END SCOPE  
  
Subcube_Expression ::=(Auxiliary_Subcube [, Auxiliary_Subcube,...n])  
  
Auxiliary_Subcube ::=   
        Limited_Set   
    | Root([dimension_name])   
    | Leaves([dimension_name])  
  
Limited_Set ::=   
        single_tuple   
    | member   
    | Common_Grain_Members   
    | hierarchy.members   
    | level.members   
    | {}   
    | Descendants  
            (  
                  Member  
         , [level  
         [  
            , SELF   
             | AFTER   
                          | BEFORE   
                          | SELF_AND_AFTER   
                          | SELF_AND_BEFORE   
                          | SELF_BEFORE_AFTER   
                          | LEAVES  
                  ]  
            )   
[* <limited set>]  
```  
  
## <a name="arguments"></a>引数  
 *Subcube_Expression*  
 有効な MDX サブキューブ式です。  
  
 *MDX_Statement*  
 有効な MDX ステートメントです。  
  
 *Common_Grain_Members*  
 同じ粒度を持つメンバーに評価される有効な MDX ステートメント。  
  
 *single_tuple*  
 1 つの組です。  
  
## <a name="remarks"></a>解説  
 SCOPE ステートメントは、1つまたは複数の MDX ステートメントの実行によって影響を受けるサブキューブを決定します。 MDX ステートメントが SCOPE ステートメント内にある場合を除き、MDX ステートメントの暗黙的なスコープはキューブ全体です。  
  
> [!NOTE]  
>  SCOPE ステートメントは、非表示のメンバーも公開します。  
  
 SCOPE ステートメントは、 **MDX 互換性** の設定に関係なく、"ホール" を公開するサブキューブを作成します。 たとえば、というステートメントでは、 `Scope( Customer.State.members )` 都道府県を含まない国または地域の州を含めることができますが、それ以外の非表示のプレースホルダーメンバーが挿入されます。  
  
 スコープステートメント内で作成された計算されるメンバーおよび名前付きセットは、SCOPE ステートメントの影響を受けません。  
  
## <a name="example"></a>例  
 次の例では、Adventure Works サンプルソリューションの MDX 計算スクリプトから、現在のスコープを会計四半期として2005、sales amount quota メジャーを定義して、 **Parallelperiod** 関数を使用して現在のスコープ内のセルに値を割り当てています。 次に、別の SCOPE ステートメントを使用してスコープを変更した後、 [This (MDX)](../mdx/this-mdx.md) 関数を使用して別の割り当てを実行します。  
  
```  
Scope   
 (   
    [Date].[Fiscal Year].&[2005],  
    [Date].[Fiscal].[Fiscal Quarter].Members,  
    [Measures].[Sales Amount Quota]  
 ) ;     
  
   This = ParallelPeriod                               
          (   
             [Date].[Fiscal].[Fiscal Year], 1,  
             [Date].[Fiscal].CurrentMember   
          ) * 1.35 ;  
  
/*-- Allocate equally to months in FY 2002 -----------------------------*/  
  
  Scope   
  (   
     [Date].[Fiscal Year].&[2002],  
     [Date].[Fiscal].[Month].Members   
  ) ;     
  
    This = [Date].[Fiscal].CurrentMember.Parent / 3 ;     
  
  End Scope ;     
End Scope ;     
```  
  
## <a name="see-also"></a>参照  
 [MDX スクリプト ステートメント &#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
