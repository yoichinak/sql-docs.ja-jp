---
description: DrilldownMember (MDX)
title: ドリルダウンメンバー (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0dfc26c52cbd478979cbbaad4a69e66bc58138a5
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194024"
---
# <a name="drilldownmember-mdx"></a>DrilldownMember (MDX)


  2 番目に指定されたセット内に存在する、指定されたセットのメンバーをドリル ダウンします。  
  
 または、最初の組階層または必要に応じて指定した階層を使用して、関数が組のセットをドリル ダウンします。  
  
## <a name="syntax"></a>構文  
  
```  
  
DrillDownMember(<Set_Expression1>, <Set_Expression2> [,[<Target_Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]])  
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Target_Hierarchy*  
 階層を返す有効な多次元式 (MDX) 式です。  
  
 *繰り返し*  
 セットの再帰的な比較を示すキーワードです。  
  
 *Include_Calc_Members*  
 計算されるメンバーがドリルダウン結果に含まれるようにするキーワード。  
  
## <a name="remarks"></a>注釈  
 この関数は、階層によって順序付けられた子メンバーのセットを返します。このセットには、最初のセットで指定されたメンバーのうち、2 番目のセット内にも存在するメンバーが格納されます。 最初のセットに親メンバーと 1 つ以上の子が含まれている場合、親メンバーはドリル ダウンされません。 1 番目のセットの次元は任意ですが、2 番目には 1 次元のセットを指定する必要があります。 順序は、最初のセットの元のメンバーの間で保持されます。ただし、関数の結果セットに含まれるすべての子メンバーは、その親メンバーの直下に含まれます。 関数は、2番目のセットにも存在する1番目のセット内の各メンバーの子を取得することによって、結果セットを構築します。 **RECURSIVE**が指定されている場合、関数は、結果セットのメンバーを2番目のセットに対して再帰的に比較し、結果セットのメンバーが2番目のセットに存在しないようになるまで、2番目のセットにも存在します。  
  
 XMLA プロパティ **MdpropMdxDrillFunctions** に対してクエリを実行すると、ドリル機能に対してサーバーが提供するサポートのレベルを確認できます。詳細については、「 [サポートされる Xmla プロパティ &#40;xmla&#41;](/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) 」を参照してください。  
  
 1番目のセットには、メンバーではなく組を含めることができます。 組のドリルダウンは OLE DB の拡張機能であり、メンバーではなく組のセットを返します。  
  
> [!IMPORTANT]  
>  メンバーは、直後にその子の1つが続く場合、にドリルダウンされません。 セット内のメンバーの順序は、ドリルダウン * 関数とドリルアップファミリ関数の両方にとって重要 \* です。  
  
## <a name="examples"></a>例  
 次の例では、最初のセットのメンバーであり 2 番目のセットにも存在する、Australia へのドリル ダウンを行っています。  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   )  
   ON 0  
   FROM [Adventure Works]  
```  
  
 次の例では、最初のセットのメンバーであり 2 番目のセットにも存在する、Australia へのドリル ダウンを行っています。 RECURSIVE 引数があるので、結果セットのメンバー (State-Province レベルのメンバー) を 2 番目のセットと再帰的に比較し、結果セット内にあり 2 番目のセット内にも存在する各メンバーの子 (City レベルのメンバー) を取得するという操作が、結果セットのメンバーが 2 番目のセット内で検出されなくなるまで続けて行われます。  
  
```  
SELECT DrilldownMember   
   ( [Geography].[Geography].Children,  
      {[Geography].[Geography].[Country].[Australia],  
        [Geography].[Geography].[State-Province].[New South Wales]}  
   ,RECURSIVE)  
   ON 0  
   FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
