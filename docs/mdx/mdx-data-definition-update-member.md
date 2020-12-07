---
description: MDX データ操作 - UPDATE MEMBER
title: UPDATE MEMBER ステートメント (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 3b1333a8784ea5427dec3ed7223a3c7c1a09120d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387066"
---
# <a name="mdx-data-definition---update-member"></a>MDX データ操作 - UPDATE MEMBER


  既存の計算されるメンバーを更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
UPDATE MEMBER Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>引数  
 *Cube_Name*  
 メンバーを含むキューブの名前を指定する有効な文字列です。  
  
 *Member_Name*  
 既存のメンバーの名前を指定する有効な文字列です。  
  
 *MDX_Expression*  
 メンバーを更新する有効な多次元式 (MDX) 式です。  
  
 *Property_Name*  
 計算されるメンバーのプロパティの名前を指定する有効な文字列です。  
  
 *Property_Value*  
 計算されるメンバーのプロパティ値を指定する有効なスカラー式です。  
  
## <a name="remarks"></a>解説  
 UPDATE MEMBER ステートメントは、他の計算に対して、このメンバーの相対的な優先順位を維持したまま、既存の計算されるメンバーを更新します。 したがって、SOLVEORDER を変更するために UPDATE MEMBER ステートメントを使用することはできません。  
  
 キューブの MDX スクリプトでは、UPDATE MEMBER ステートメントを指定できません。  
  
 現在接続されているキューブ以外のキューブを指定すると、エラーが発生します。 したがって、現在のキューブを示すには、キューブ名の代わりに CURRENTCUBE を使用する必要があります。  
  
 OLE DB によって定義されるメンバープロパティの詳細については、OLE DB のドキュメントを参照してください。  
  
## <a name="standard-properties"></a>標準のプロパティ  
 各メンバーには、一連の既定のプロパティがあります。 これらの既定のプロパティを次の表に示します。  
  
|プロパティの識別子|説明|  
|-------------------------|-------------|  
|FORMAT_STRING|クライアントアプリケーションがセル値を表示するために使用できる Office スタイルの書式指定文字列。|  
|表示|計算されるメンバーがスキーマ行セットに表示されるかどうかを示す値です。 表示される計算されるメンバーは、 [Add演算メンバー](../mdx/addcalculatedmembers-mdx.md) 関数を使用してセットに追加できます。 0以外の値は、計算されるメンバーが表示されることを示します。 このプロパティの既定値が *表示*されます。<br /><br /> 一般に、表示されない計算されるメンバーは、より複雑な計算されるメンバーの中間手順として使用されます。 これらの計算されるメンバーは、メジャーなど、他の種類のメンバーによって参照することもできます。|  
|NON_EMPTY_BEHAVIOR|空のセルを解決する場合の計算されるメンバーの動作を決定するために MDX が使用するメジャーまたはセットです。|  
|キャプション|メンバーを表示するためにクライアントアプリケーションが使用するキャプションを指定する文字列値。|  
|DISPLAY_FOLDER|クライアントアプリケーションによってメンバーが表示される、表示フォルダーのパスを指定する文字列値。 フォルダー レベルの区切り記号は、クライアント アプリケーションによって定義されます。 によって提供されるツールとクライアントの場合、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] レベル区切り記号として円記号 () を使用し \\ ます。 定義されたメンバーで複数の表示フォルダーを指定するには、セミコロン (;) を使用してフォルダーを区切ります。|  
|ASSOCIATED_MEASURE_GROUP|このメンバーが関連付けられているメジャー グループの名前です。|  
  
## <a name="see-also"></a>参照  
 [DROP MEMBER ステートメント &#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [CREATE MEMBER ステートメント &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [Mdx&#41;&#40;mdx データ定義ステートメント ](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
