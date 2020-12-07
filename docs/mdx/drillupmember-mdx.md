---
description: ドリルスルーメンバー (MDX)
title: ドリルスルーメンバー (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 9db34a9117bf7405511b86e8e989d2e002cb12d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494945"
---
# <a name="drillupmember-mdx"></a>ドリルスルーメンバー (MDX)


  2番目に指定されたセットのメンバーの子孫ではない、指定されたセット内のメンバーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DrillupMember(Set_Expression1, Set_Expression2)   
```  
  
## <a name="arguments"></a>引数  
 *Set_Expression1*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
 *Set_Expression2*  
 セットを返す有効な多次元式 (MDX) 式です。  
  
## <a name="remarks"></a>解説  
 **ドリルダウンメンバー**関数は、最初のセットで指定されたメンバーに基づいて、2番目のセットのメンバーの子孫であるメンバーのセットを返します。 1 番目のセットの次元は任意ですが、2 番目には 1 次元のセットを指定する必要があります。 順序は、最初のセットの元のメンバーの間で保持されます。 関数は、2番目のセット内のメンバーの直接の子孫である最初のセット内のメンバーのみを含めることによって、セットを構築します。 最初のセット内のメンバーの直接の先祖が2番目のセットに存在しない場合は、この関数によって返されるセットに1番目のセットのメンバーが含まれます。 2番目のセット内の先祖メンバーの前にある最初のセットの子孫も含まれます。  
  
 1番目のセットには、メンバーではなく組を含めることができます。 組のドリルダウンは OLE DB の拡張機能であり、メンバーではなく組のセットを返します。  
  
> [!IMPORTANT]  
>  メンバーのドリルアップは、直後に子または子孫が続く場合のみ行われます。 セット内のメンバーの順序は、関数のドリルダウンとドリルアップの両方のファミリにとって重要 \* \* です。 最初のセットのメンバーを適切に並べ替えるには、 **Hierarchize** 関数を使用することを検討してください。  
  
## <a name="example"></a>例  
 次の 3 つの例は、2 番目のセットを除いて同一です。 最初の例では、2 番目のセットは United States です。 その結果、コロラドは結果セットから除外されます。 これは米国の子孫です。  
  
```  
SELECT DrillUpMember (   
  { [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[United States]}   
 ) ON 0   
FROM [Adventure Works]  
```  
  
 例2は、メンバーの順序の重要性を示しています。 ドリルダウン **メンバー** は、最初のセットの子孫が直後にあるメンバーにドリルアップするだけなので、カナダメンバーをドリルアップしません。 カナダは、米国とコロラドでその子孫から分離されています。 カナダがアルバータ州の真上にあるようにメンバーの順序を変更すると、アルバータとニューブランズウィックの両方が行セットから除外されます。  
  
```  
SELECT DrillUpMember (   
 {  [Geography].[Geography].[Country].[Canada]   
   ,[Geography].[Geography].[Country].[United States]   
   ,[Geography].[Geography].[State-Province].[Colorado]   
   ,[Geography].[Geography].[State-Province].[Alberta]   
   ,[Geography].[Geography].[State-Province].[Brunswick]    
 }   
 , {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
```  
  
 例3では、 **Hierarchize** を使用してメンバーの順序の効果を軽減し、カナダのメンバーにドリルアップする方法を示しています。  
  
```  
SELECT DrillUpMember (   
 Hierarchize   
  (   
   { [Geography].[Geography].[Country].[Canada]   
    ,[Geography].[Geography].[Country].[United States]   
    ,[Geography].[Geography].[State-Province].[Colorado]   
    ,[Geography].[Geography].[State-Province].[Alberta]   
    ,[Geography].[Geography].[State-Province].[Brunswick]    
   }   
  ), {[Geography].[Geography].[Country].[Canada]}   
 )   
ON 0   
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>参照  
 [MDX 関数リファレンス &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
