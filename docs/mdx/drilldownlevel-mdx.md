---
description: ドリルダウンレベル (MDX)
title: ドリルダウンレベル (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3bd1f2214820a1795ae8d279c88a0d86c2ca5843
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194014"
---
# <a name="drilldownlevel-mdx"></a>ドリルダウンレベル (MDX)


  セットで表される最低レベルより 1 つ下のレベルに、セットのメンバーをドリルダウンします。  
  
 ドリルダウンするレベルの指定は省略可能ですが、レベルを設定した場合は、 **レベル式** または **インデックスレベル**を使用できます。 これらの引数は相互に排他的です。 最後に、計算されるメンバーがクエリに存在する場合は、引数を指定して行セットに含めることができます。  
  
## <a name="syntax"></a>構文  
  
```  
DrilldownLevel(Set_Expression [,[Level_Expression] ,[Index]] [,INCLUDE_CALC_MEMBERS])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Level_Expression*  
 (省略可能)。 ドリルダウンするレベルを明示的に識別する MDX 式。 レベル式を指定する場合は、以下の index 引数をスキップします。  
  
 *Index*  
 (省略可能)。 セット内でドリルダウンする階層番号を指定する有効な数値式です。 Level_Expression の代わりにインデックスレベルを使用して、ドリルダウンするレベルを明示的に指定することができます。  
  
 *Include_Calc_Members*  
 (省略可能)。 計算されるメンバーがドリルダウン レベルに存在する場合にそれらを含めるかどうかを示すフラグです。  
  
## <a name="remarks"></a>注釈  
 **ドリルダウンレベル**関数は、指定されたセットに含まれるメンバーに基づいて、階層の順序で子メンバーのセットを返します。 順序は、指定されたセット内の元のメンバーの間で保持されます。ただし、関数の結果セットに含まれるすべての子メンバーは、その親メンバーの直下に含まれます。  
  
 複数レベルの階層データ構造を指定した場合は、ドリルダウンするレベルを明示的に選択できます。 レベルを指定するには、相互に排他的な2つの方法があります。 1つ目の方法は、レベルを返す MDX 式を使用して **level_expression** 引数を設定することです。別の方法として、数値でレベルを指定する数値式を使用して、 **インデックス** 引数を指定することもできます。  
  
 レベル式が指定されている場合、関数は、指定されたレベルにあるメンバーの子だけを取得することによって、階層の順序でセットを構築します。 レベル式が指定されていて、そのレベルにメンバーがない場合、レベル式は無視されます。  
  
 インデックス値が指定された場合、この関数は、インデックス (0 を基点とするインデックス) を基準にして、指定されたセット内で参照されている階層の最低レベルより 1 つ上のレベルにあるメンバーの子メンバーだけを取得し、階層の順序でセットを構築します。  
  
 レベル式もインデックス値も指定されていない場合、関数は、指定されたセット内で参照されている最初のディメンションの最下位レベルにあるメンバーの子だけを取得することによって、階層の順序でセットを構築します。  
  
 XMLA プロパティ MdpropMdxDrillFunctions に対してクエリを実行すると、ドリル機能に対してサーバーが提供するサポートのレベルを確認できます。詳細については、「 [サポートされる Xmla プロパティ &#40;xmla&#41;](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 」を参照してください。  
  
## <a name="examples"></a>例  
 SSMS の MDX クエリウィンドウでは、Adventure Works キューブを使用して、次の例を試すことができます。  
  
 **例 1-最小構文を示します。**  
  
 最初の例は、 **ドリルダウンレベル**の最小構文を示しています。 唯一必要な引数は、セット式です。 このクエリを実行すると、親 [All Categories] と次のレベルのメンバー ([アクセサリ]、[Bikes] など) が取得されることに注意してください。 この例は単純ですが、次のレベルにドリルダウンする、 **ドリルダウンレベル** 関数の基本的な目的を示しています。  
  
```  
SELECT DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]}}) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 例 2-明示的なインデックスレベルを使用した代替構文  
  
 この例では、インデックスレベルが数値式で指定されている代替構文を示します。 この場合、インデックスレベルは0です。 0から始まるインデックスの場合、これは最も低いレベルです。  
  
```  
SELECT  
DRILLDOWNLEVEL({[Product].[Product Categories]} * {[Sales Territory].[Sales Territory]},,0) ON COLUMNS  
FROM [Adventure Works]  
```  
  
 前のクエリと同じ結果セットが返されることに注意してください。 一般に、特定のレベルからドリルダウンする場合を除き、インデックス レベルを設定する必要はありません。 前のクエリを再実行し、インデックス値を1に設定してから、2を実行します。 インデックス値が1に設定されている場合は、階層の2番目のレベルからドリルダウンが開始されます。 インデックス値が2に設定されている場合、ドリルダウンは、この例の最上位レベルである3番目のレベルから開始します。 数値式を大きくするほど、インデックス レベルは高くなります。  
  
 **例 3-レベル式のデモ**  
  
 次の例では、レベル式を使用する方法を示します。 階層構造を表すセットが指定されている場合、レベル式を使用すると、階層内のレベルを選択してドリルダウンを開始できます。  
  
 この例では、ドリルダウンのレベルは **、ドリルダウンレベル関数の** 2 番目の引数として [City] から始まります。 このクエリを実行すると、ワシントン州およびオレゴン州の [City] レベルからドリルダウンされます。 **ドリル**ダウンレベル関数の結果セットには、次のレベル下にあるメンバーも含まれています。 [郵便番号]。  
  
```  
SELECT [Measures].[Internet Sales Amount] ON COLUMNS,  
   NON EMPTY (  
   DRILLDOWNLEVEL(  
       {[Customer].[Customer Geography].[Country].[United States],  
           DESCENDANTS(  
             { [Customer].[Customer Geography].[State-Province].[Washington],    
               [Customer].[Customer Geography].[State-Province].[Oregon]},   
               [Customer].[Customer Geography].[City]) } ,  
[Customer].[Customer Geography].[City] ) )  ON ROWS  
FROM [Adventure Works]  
```  
  
 **例 4-計算されるメンバーを含む**  
  
 最後の例は、 **include_calculated_members** フラグを追加したときに、結果セットの末尾に表示される計算されるメンバーを示しています。 フラグが4番目のパラメーターとして指定されていることに注意してください。  
  
 計算されるメンバーが、計算されないメンバーと同じレベルに存在するため、この例は正常に実行されます。 計算されるメンバー [West Coast] は、[米国] のメンバーと、[米国] の1レベル下にあるすべてのメンバーで構成されます。  
  
```  
WITH MEMBER   
[Customer].[Customer Geography].[Country].&[United States].[West Coast] AS  
[Customer].[Customer Geography].[State-Province].&[OR]&[US] +  
[Customer].[Customer Geography].[State-Province].&[WA]&[US] +  
[Customer].[Customer Geography].[State-Province].&[CA]&[US]  
SELECT [Measures].[Internet Order Count] ON 0,  
DRILLDOWNLEVEL([Customer].[Customer Geography].[Country].&[United States],,,INCLUDE_CALC_MEMBERS) on 1  
FROM [Adventure Works]  
```  
  
 このフラグだけを削除してクエリを再実行すると、計算されるメンバー [West Coast] が除かれた、同じ結果が返されます。  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
