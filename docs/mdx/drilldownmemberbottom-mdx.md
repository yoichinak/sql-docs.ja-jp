---
description: DrilldownMemberBottom (MDX)
title: ドリルダウン Memberbottom (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: eb308c3fbdbcf9f13398a7d44c885069c1665db1
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193984"
---
# <a name="drilldownmemberbottom-mdx"></a>DrilldownMemberBottom (MDX)


  2番目に指定したセット内に存在する、指定したセットのメンバーをドリルダウンします。結果セットは、指定した数のメンバーに制限されます。 または、この関数では、最初の組階層または必要に応じて指定した階層を使用して、組のセットをドリルダウンすることもできます。  
  
## <a name="syntax"></a>構文  
  
```  
  
DrillDownMemberBottom(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expresion>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Count*  
 返す組の数を指定する有効な数値式です。  
  
 *Numeric_Expression*  
 有効な数値式です。通常は、数値を返すセル座標の多次元式 (MDX) 式です。  
  
 *Hierarchy*  
 階層を返す有効な多次元式 (MDX) 式です。  
  
 *繰り返し*  
 セットの再帰的な比較を示すキーワードです。  
  
 *Include_Calc_Members*  
 計算されるメンバーがドリルダウン結果に含まれるようにするキーワード。  
  
## <a name="remarks"></a>注釈  
 数値式を指定する **と、子** メンバーのセットに対して評価された数値式の値に従って、1番目のセット内の各メンバーの子を昇順で並べ替えます。 数値式が指定されていない場合、関数は、クエリコンテキストによって決定される子メンバーのセットによって表されるセルの値に基づいて、最初のセット内の各メンバーの子を昇順で並べ替えます。 この動作は、並べ替えを行わずに、一連のメンバーを自然な順序で返す、下端のカウントおよび末尾 (MDX) 関数に似ています。  
  
 並べ替えの後、 **ドリルダウン Memberbottom** 関数は、親メンバーと子メンバーの *数を含む* セットを返します。これには、最小値が設定され、両方のセットに含まれています。  
  
 **RECURSIVE**が指定されている場合、関数は、前に説明したように最初のセットを並べ替えてから、階層に編成されている最初のセットのメンバーを2番目のセットに対して再帰的に比較します。 この関数は、最初のセットのメンバーのうち、2 番目のセット内にも存在する各メンバーの子を、最小のものから指定されている数だけ取得します。  
  
 1番目のセットには、メンバーではなく組を含めることができます。 組のドリルダウンは OLE DB の拡張機能であり、メンバーではなく組のセットを返します。  
  
 **ドリルダウン Memberbottom**関数は、[ドリルダウンメンバー](../mdx/drilldownmember-mdx.md)関数と似ていますが、2番目のセットにも含まれている最初のセット内の各メンバーのすべての子を含めるのではなく、**ドリルダウン memberbottom**関数は各メンバーの最下位の子メンバーの数を返します。  
  
 XMLA プロパティ MdpropMdxDrillFunctions に対してクエリを実行すると、ドリル機能に対してサーバーが提供するサポートのレベルを確認できます。詳細については、「 [サポートされる Xmla プロパティ &#40;xmla&#41;](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 」を参照してください。  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
