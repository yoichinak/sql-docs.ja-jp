---
description: 空の値の操作
title: 空の値を使用する |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f497ba1ccf84ac642144340af4d5597d773dcadb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421896"
---
# <a name="working-with-empty-values"></a>空の値の操作


  空の値は、特定のメンバー、組、またはセルが空であることを示します。 空のセル値は、指定されたセルのデータが基になるファクト テーブルに見つからないこと、あるいは指定されたセルの組の表すメンバーの組み合わせをキューブに適用できないことのいずれかを示します。  
  
> [!NOTE]  
>  空の値は0の値とは異なりますが、通常、空の値はゼロとして扱われます。  
  
 次のクエリでは、空の値と 0 の動作を示しています。  
  
```  
WITH  
//A calculated Product Category that always returns 0  
MEMBER [Product].[Category].[All Products].ReturnZero AS 0  
//Will return true for any null value  
MEMBER MEASURES.ISEMPTYDemo AS ISEMPTY([Measures].[Internet Tax Amount])  
//Will true for any null or zero value  
//To be clear: the expression 0=null always returns true in MDX  
MEMBER MEASURES.IsZero AS [Measures].[Internet Tax Amount]=0  
SELECT  
{[Measures].[Internet Tax Amount],MEASURES.ISEMPTYDemo,MEASURES.IsZero}  
ON COLUMNS,  
[Product].[Category].[Category].ALLMEMBERS  
ON ROWS  
FROM [Adventure Works]  
WHERE([Date].[Calendar].[Calendar Year].&[2001])  
```  
  
 次の情報は、空の値に適用されます。  
  
-   [IsEmpty](../mdx/isempty-mdx.md)関数は、関数で指定された組によって識別されるセルが空の場合にのみ**TRUE**を返します。 それ以外の場合、関数は **FALSE**を返します。  
  
    > [!NOTE]  
    >  **IsEmpty**関数は、メンバー式が null 値を返すかどうかを判断できません。 Null メンバーが式から返されるかどうかを判断するに [は、is](../mdx/is-mdx.md)演算子を使用します。  
  
-   空のセル値が数値演算子 (+、-、*、/) のいずれかのオペランドである場合、もう一方のオペランドが空でない値であるなら、空のセル値は 0 として扱われます。 両方のオペランドが空の場合、数値演算子は空のセル値を返します。  
  
-   空のセル値が文字列連結演算子 (+) のオペランドである場合、もう一方のオペランドが空でない値の場合、空のセル値は空の文字列として扱われます。 オペランドが両方とも空なら、文字列連結演算子は空のセル値を返します。  
  
-   空のセル値がいずれかの比較演算子 (=) のオペランドである場合。 <>、>=、 \<=, > 、<) の場合、他のオペランドのデータ型が数値と文字列のどちらであるかによって、空のセル値は0または空の文字列として扱われます。 オペランドが両方とも空なら、どちらも 0 として扱われます。  
  
-   数値を照合する場合、空のセル値は0と同じ場所に照合されます。 空のセル値と 0 との照合の場合、空のセル値の照合順序は、0 の前になります。  
  
-   文字列の値を照合する場合、空のセル値の照合順序は、空の文字列と同じ位置になります。 空のセル値と空の文字列の間には、空の文字列の前に空の照合順序があります。  
  
## <a name="dealing-with-empty-values-in-mdx-statements-and-cubes"></a>MDX ステートメントおよびキューブにおける空の値の処理  
 多次元式 (MDX) ステートメントでは、空の値を検索し、有効な (空ではない) データを含むセルに対して特定の計算を実行できます。 計算時に空の値を除去することが必要な場合があります。平均値などの計算では、空のセル値が含まれていると正確な結果を得ることができません。  
  
 基になるファクトテーブルデータに空の値が格納されている場合、既定では、キューブが処理されるときにゼロに変換されます。 メジャーに対して **Null 処理** オプションを使用すると、null ファクトを0に変換するか、空の値に変換するか、または処理中にエラーをスローするかを制御できます。 空のセル値がクエリ結果に表示されないようにするには、空の値を除去するか他の値に置き換えるクエリ、計算されるメンバー、または MDX スクリプト ステートメントを作成する必要があります。  
  
 空の行または列をクエリから削除するには、軸セットの定義の前に空でないステートメントを使用します。 たとえば、次のクエリでは、製品カテゴリ Bikes のみが返されます。これは、2001年に販売された唯一のカテゴリであるためです。  
  
 `SELECT`  
  
 `{[Measures].[Internet Tax Amount]}`  
  
 `ON COLUMNS,`  
  
 `//Comment out the following line to display all the empty rows for other Categories`  
  
 `NON EMPTY`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Date].[Calendar].[Calendar Year].&[2001])`  
  
 セットから空の組を削除するには、NonEmpty 関数を使用する方法がより一般的です。 次のクエリでは、2つの計算されるメジャーを示しています。1つは製品カテゴリの数をカウントし、2番目はメジャー [Internet Tax Amount] と2001暦年の値を持つ製品カテゴリの数を示します。  
  
 `WITH`  
  
 `MEMBER MEASURES.CategoryCount AS`  
  
 `COUNT([Product].[Category].[Category].MEMBERS)`  
  
 `MEMBER MEASURES.NonEmptyCategoryCountFor2001 AS`  
  
 `COUNT(`  
  
 `NONEMPTY(`  
  
 `[Product].[Category].[Category].MEMBERS`  
  
 `,([Date].[Calendar].[Calendar Year].&[2001], [Measures].[Internet Tax Amount])`  
  
 `))`  
  
 `SELECT`  
  
 `{MEASURES.CategoryCount,MEASURES.NonEmptyCategoryCountFor2001 }`  
  
 `ON COLUMNS`  
  
 `FROM [Adventure Works]`  
  
 詳細については、「空でない [&#40;MDX&#41;](../mdx/nonempty-mdx.md)」を参照してください。  
  
## <a name="empty-values-and-comparison-operators"></a>空の値と比較演算子  
 データに空の値がある場合、論理演算子と比較演算子は、TRUE または FALSE ではなく、空の3番目の結果を返す可能性があります。 このような 3 値論理が必要な場合、多くのアプリケーション エラーの原因になります。 これらの表は、空の値の比較を導入した場合の効果を示しています。  
  
 次の表は、2つのブール型オペランドに AND 演算子を適用した結果を示しています。  
  
|AND|true|EMPTY|false|  
|---------|----------|-----------|-----------|  
|**TRUE**|true|false|false|  
|**指定**|false|EMPTY|false|  
|**FALSE**|false|false|false|  
  
 次の表は、OR 演算子を2つのブール値オペランドに適用した結果を示しています。  
  
|OR|true|false|  
|--------|----------|-----------|  
|**TRUE**|true|true|  
|**指定**|true|true|  
|**FALSE**|true|false|  
  
 次の表は、NOT 演算子によってブール演算子の結果が否定または反転される方法を示しています。  
  
|NOT 演算子が適用されるブール式|評価結果|  
|-------------------------------------------------------------|------------------|  
|true|false|  
|EMPTY|EMPTY|  
|false|true|  
  
## <a name="see-also"></a>参照  
 [Mdx 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [Mdx 演算子リファレンス &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [MDX &#40;式&#41;](../mdx/expressions-mdx.md)  
  
  
