---
description: Find メソッド (ADO)
title: Find メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Find
- Recordset15::Find
helpviewer_keywords:
- Find method [ADO]
ms.assetid: 55c9810a-d8ca-46c2-a9dc-80e7ee7aa188
author: rothja
ms.author: jroth
ms.openlocfilehash: 18b4dc88dfedbb5a9a06968ebb5b02300439ed1b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88972953"
---
# <a name="find-method-ado"></a>Find メソッド (ADO)
[レコードセット](./recordset-object-ado.md)内で、指定した条件を満たす行を検索します。 必要に応じて、開始行からの検索、開始行、およびオフセットの方向を指定することもできます。 条件が満たされた場合は、見つかったレコードに現在の行の位置が設定されます。それ以外の場合、位置は **レコードセット**の末尾 (または先頭) に設定されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Find (Criteria, SkipRows, SearchDirection, Start)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *条件*  
 検索で使用する列名、比較演算子、および値を指定するステートメントを含む **文字列** 値です。  
  
 *SkipRows*  
 省略可能。 現在の行または*開始*ブックマークからの行オフセットを指定する**Long**値。既定値は0です。 既定では、検索は現在の行で開始されます。  
  
 *SearchDirection*  
 省略可能。 検索を現在の行で開始するか、検索の方向で次に使用可能な行で開始するかを指定する [Searchdirection 列挙](./searchdirectionenum.md) 値。 値が**Adsearchforward**の場合、**レコードセット**の末尾で失敗した検索は停止します。 値が**Adsearchbackward**の場合、**レコードセット**の先頭で失敗した検索は停止します。  
  
 *Start*  
 省略可能。 検索の開始位置として機能する **Variant** ブックマーク。  
  
## <a name="remarks"></a>解説  
 *条件*には、単一列の名前のみを指定できます。 このメソッドは、複数列の検索をサポートしていません。  
  
 *条件*としての比較演算子には、" **>** " (より大きい)、"* * \<**" (less than), "=" (equal), "> =" (以上)、"<=" (以下)、"<>" (不等号)、"like" (パターンマッチング) などがあります。  
  
 *条件*の値には、文字列、浮動小数点数、または日付を指定できます。 文字列値は、単一引用符または "#" (シャープ記号) マーク (たとえば、"state = ' WA '" または "state = #WA #") で区切られます。 日付の値は、"#" (シャープ記号) マークで区切られます (たとえば、"start_date > #7/22/97 #")。 これらの値には、タイムスタンプを示す時間、分、秒を含めることができますが、ミリ秒を含めることはできません。または、エラーが発生します。  
  
 比較演算子が "like" の場合、文字列値にアスタリスク (*) を含めることで、任意の文字または部分文字列の1回以上の出現箇所を見つけることができます。 たとえば、"m のような状態 \* " は Maine とマサチューセッツに一致します。 また、先頭と末尾のアスタリスクを使用して、値内に含まれる部分文字列を検索することもできます。 たとえば、"州 like ' \* as \* '" はアラスカ、アーカンソー、およびマサチューセッツに一致します。  
  
 上に示すように、アスタリスクは、条件文字列の末尾、または条件文字列の先頭と末尾の両方で使用できます。 先頭のワイルドカードとしてアスタリスク (' * str ') を使用することはできません。また、埋め込みワイルドカード (r) として使用することもできません \* 。 これにより、エラーが発生します。  
  
> [!NOTE]
>  **検索**を呼び出す前に現在の行の位置が設定されていない場合、エラーが発生します。 [**検索**] を呼び出す前に、 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)などの行の位置を設定するメソッドを呼び出す必要があります。  
  
> [!NOTE]
>  レコードセットの **find** メソッドを呼び出し、レコードセットの現在位置が最後のレコードまたはファイルの末尾 (EOF) である場合、何も見つかりません。 **MoveFirst**メソッドを呼び出して、現在の位置/カーソルをレコードセットの先頭に設定する必要があります。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Find メソッドの例 (VB)](./find-method-example-vb.md)   
 [Index プロパティ](./index-property.md)   
 [Optimize プロパティ-動的 (ADO)](./optimize-property-dynamic-ado.md)   
 [Seek メソッド](./seek-method.md)