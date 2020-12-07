---
description: MDX データ操作 - ALTER CUBE
title: ALTER CUBE ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 052d533e503f5b82f506ec119684acbbfe7cdd5f
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192352"
---
# <a name="mdx-data-definition---alter-cube"></a>MDX データ操作 - ALTER CUBE


  指定されたキューブの構造を変更します。通常、ディメンションの書き戻しをサポートするために使用されます。 アプリケーションでの書き戻しの使用の詳細については、このブログの投稿「 [Analysis Services を使用した書き戻しアプリケーションの構築 (ブログ)](/archive/blogs/data_otaku/building-a-writeback-application-with-analysis-services) 」を参照してください。  
  
 同時実行ディメンションの書き戻しによってデッドロックが発生する可能性があることに注意してください。2番目の書き戻しによって保持されている共有ロックが原因で、最初の書き戻しがコミットからブロックされます。 このような状況では、エラーは生成されません。また、どのような操作も実行されません。 最終的には、タイムアウトと変更の両方がロールバックされます。  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER CUBE  
      Cube_Name | CURRENTCUBE  
      <alter clause>   
            [ < alter clause> ...n]  
  
< alter clause> ::=   
   <create dimension member clause>   
  | <remove dimension member clause>  
  | <move dimension member clause>   
    | <update clause>   
    | <create cell calculation clause>  
  
<create dimension member clause> ::=  
CREATE DIMENSION MEMBER [ParentName.]MemberName  
    , [[KEY = Key_Value]   
    | [Property_Name = Property_Value[, ...n]]  
  
<dropping clause>::=  
DROP   
      DIMENSION MEMBER Member_Name   
            Member_Name ...n ]   
      [WITH DESCENDANTS]  
      | [ SESSION ] [ CALCULATED ] MEMBER Member_Name   
                  [ ,Member_Name,...n ]   
    | SET Set_Name  
                  [ ,Set_Name,...n ]   
    | [ SESSION ] CELL CALCULATION CellCalc_Name  
                  [ ,CellCalc_Name,...n ]   
    | ACTION Action_Name  
  
<move dimension member clause> ::=  
MOVE DIMENSION MEMBER MemberName  
        [, SKIPPED_LEVELS = Unsigned_Integer]   
      [WITH DESCENDANTS]  
    UNDER ParentName      
  
<update clause> ::=  
UPDATE   
    CUSTOM ROLLUP FOR MEMBER MemberName  
      [,MemberName, ...n] AS MDX_Expression  
   | DIMENSION Dimension_Name | Hierarchy_Name  
      , DEFAULT_MEMBER = MDX_Expression  
   | DIMENSION MEMBER MemberName AS  
   [MDX_Expression]  
   [Property_Name = Property_Value[, ...n]]  
  
<create cell calculation clause>::=  
CELL CALCULATION Calculation_Name   
   FOR Set_Expression AS MDX_Expression   
            [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="creating-a-dimension-member"></a>ディメンションメンバーの作成  
 基になるディメンションテーブルに新しい行が追加されます。  
  
### <a name="arguments"></a>引数  
 *ParentName*  
 ディメンションメンバーがルートで作成されている場合を除き、新しいディメンションメンバーの親の名前を提供する有効な文字列式です。  
  
 *MemberName*  
 メンバー名を提供する有効な文字列式です。  
  
 *Key_Value*  
 新しいディメンションメンバーのキー値を定義する有効なスカラー式です。  
  
 *Property_Name*  
 メンバー プロパティを表す有効な多次元式 (MDX) 識別子です。  
  
 *Property_Value*  
 計算されるメンバー プロパティの値を定義する有効な多次元式 (MDX) スカラー式です。  
  
## <a name="dropping-a-dimension-member"></a>ディメンションメンバーの削除  
 書き込み許可ディメンションからディメンションメンバーを削除すると、基になるディメンションテーブルからメンバーとそれに対応する行が削除されます。  
  
### <a name="arguments"></a>引数  
 *Cube_Name*  
 キューブ名を指定する有効な文字列式です。  
  
 *Member_Name*  
 メンバー名またはメンバーキーを指定する有効な文字列式です。  
  
### <a name="remarks"></a>注釈  
 WITH DESCENDANTS 句を使用しなかった場合、削除したメンバーの子は、削除したメンバーの親の子になります。 WITH 子孫句が使用されている場合は、ディメンションテーブル内のすべての子孫とその行も削除されます。  
  
> [!NOTE]  
>  計算されるメンバー、名前付きセット、アクション、およびセルの計算の削除については、「 [DROP MEMBER ステートメント &#40;mdx&#41;](../mdx/mdx-data-definition-drop-member.md)」、「Drop [SET ステートメント &#40;mdx&#41;](../mdx/mdx-data-definition-drop-set.md)」、「 [drop ACTION ステートメント &#40;mdx&#41;](../mdx/mdx-data-definition-drop-action.md)」、および「drop [cell CALCULATION ステートメント &#40;mdx&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md)」を参照してください。  
  
## <a name="updating-the-default-dimension-member"></a>既定のディメンション メンバーの更新  
 この句は、キューブの既定のメンバーを更新し、MDX 計算スクリプトで既定のメンバーを定義するために使用されます。 データベース ディメンション、キューブ ディメンション、またはユーザー ログインの既定のメンバーを指定できます。 既定のメンバーは、セッション中に変更することもできます。  
  
### <a name="arguments"></a>引数  
 *Dimension_Name*  
 ディメンションの名前を提供する有効な文字列です。  
  
 *MDX_Expression*  
 1つのメンバーを返す有効な MDX 式です。  
  
### <a name="remarks"></a>注釈  
 指定された MDX 式は、静的または動的にすることができます。  
  
## <a name="moving-a-dimension-member"></a>ディメンション メンバーの移動  
 基になるディメンション テーブルの行が変更されます。  
  
### <a name="arguments"></a>引数  
 *ParentName*  
 移動するディメンションメンバーの新しい親の名前を指定する有効な文字列式です。  
  
 *MemberName*  
 メンバー名を提供する有効な文字列式です。  
  
 Unsigned_*整数*  
 スキップするレベル数を指定する有効な数値です。  
  
 WITH 子孫句が指定されている場合、ツリー全体が移動されます。 WITH DESCENDANTS を指定しなかった場合、移動した親の子は、移動したメンバーの親の子になります。 移動の効果は、単に基になるディメンションテーブルの親キー列の値を更新することです。  
  
## <a name="updating-a-dimension-member"></a>ディメンションメンバーの更新  
 UPDATE DIMENSION MEMBER 句を使用すると、メンバーのプロパティだけでなく、メンバーに関連付けられているカスタムメンバー式を変更することもできます。  
  
### <a name="arguments"></a>引数  
 *MemberName*  
 メンバー名を提供する有効な文字列式です。  
  
 *MDX_Expression*  
 1つのメンバーを返す有効な MDX 式です。  
  
 *Property_Value*  
 計算されるメンバープロパティの値を定義する有効な MDX スカラー式です。  
  
## <a name="creating-a-cell-calculation"></a>セル計算の作成  
 ALTER CUBE ステートメントを使用してセル計算を作成する方法の詳細については、「 [DROP CELL Calculation ステートメント &#40;MDX&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Mdx&#41;&#40;mdx データ定義ステートメント ](../mdx/mdx-data-definition-statements-mdx.md)  
  
