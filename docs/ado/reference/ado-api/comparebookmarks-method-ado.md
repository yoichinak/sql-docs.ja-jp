---
description: CompareBookmarks メソッド (ADO)
title: CompareBookmarks メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
author: rothja
ms.author: jroth
ms.openlocfilehash: 785f2b61e4a6197a287ce9f97b27fef5cb8742b1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975053"
---
# <a name="comparebookmarks-method-ado"></a>CompareBookmarks メソッド (ADO)
2つのブックマークを比較し、それらの相対値を示す値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>戻り値  
 各ブックマークによって表される2つのレコードの相対行の位置を示す [Compareenum](./compareenum.md) 値を返します。  
  
#### <a name="parameters"></a>パラメーター  
 *Bookmark1*  
 最初の行のブックマーク。  
  
 *Bookmark2*  
 2番目の行のブックマーク。  
  
## <a name="remarks"></a>解説  
 ブックマークは、同じ [レコードセット](./recordset-object-ado.md) オブジェクト、または **レコードセット** オブジェクトとその [複製](./clone-method-ado.md)に適用する必要があります。 同じソースまたはコマンドから作成されたものであっても、異なる **レコードセット** オブジェクトのブックマークを確実に比較することはできません。 また、基になるプロバイダーで比較がサポートされていない **レコードセット** オブジェクトのブックマークを比較することもできません。  
  
 ブックマークは、 **レコードセット** オブジェクト内の行を一意に識別します。 ブックマークを取得するには、現在の行の [bookmark](./bookmark-property-ado.md) プロパティを使用します。  
  
 ブックマークのデータ型は各プロバイダーに固有であるため、ADO はそれを **バリアント**として公開します。 たとえば、SQL Server のブックマークの種類は DBTYPE_R8 (**Double**) です。 この型は、 **Double**型のサブタイプの**バリアント**として ADO によって公開されます。  
  
 ブックマークを比較するとき、ADO はどのような型の強制型変換も試行しません。 値は、比較が発生したプロバイダーに渡されるだけです。 **Comparebookmarks**メソッドに渡されるブックマークが異なる型の変数に格納されている場合、次のような型の不一致エラーが発生する可能性があります。 "引数の型が間違っているか、許容範囲外であるか、競合しています。"  
  
 無効または形式が正しくないブックマークは、エラーを発生させます。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [CompareBookmarks メソッドの例 (VB)](./comparebookmarks-method-example-vb.md)   
 [CompareBookmarks メソッドの例 (VC + +)](./comparebookmarks-method-example-vc.md)   
 [Bookmark プロパティ (ADO)](./bookmark-property-ado.md)