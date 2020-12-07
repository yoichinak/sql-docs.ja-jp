---
description: ReadText メソッド
title: ReadText メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_ReadText
- _Stream::ReadText
helpviewer_keywords:
- ReadText method [ADO]
ms.assetid: be5a409e-cf87-4859-9ea5-713401755a77
author: rothja
ms.author: jroth
ms.openlocfilehash: d2e55657dc0bf2e5cd508897196138e842e23b8e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989873"
---
# <a name="readtext-method"></a>ReadText メソッド
テキスト [ストリーム](./stream-object-ado.md) オブジェクトから指定された数の文字を読み取ります。  
  
## <a name="syntax"></a>構文  
  
```  
  
String = Stream.ReadText ( NumChars)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *NumChars*  
 省略可能。 ファイルから読み取る文字数、または[Streamreadenum](./streamreadenum.md)値を指定する**Long**値。 既定値は **Adreadall**です。  
  
## <a name="return-value"></a>戻り値  
 **ReadText**メソッドは、指定された文字数、行全体、またはストリーム全体を**ストリーム**オブジェクトから読み取り、結果の文字列を返します。  
  
## <a name="remarks"></a>解説  
 *Numchar*がストリームに残された文字数よりも多い場合は、残りの文字だけが返されます。 読み取られた文字列は、 *Numchar*で指定された長さと一致するように埋め込まれていません。 読み取る文字が残っていない場合は、値が null であるバリアントが返されます。 **ReadText** を後方読み取りに使用することはできません。  
  
> [!NOTE]
>  **ReadText**メソッドはテキストストリームと共に使用されます ([型](./type-property-ado-stream.md)は**adTypeText**)。 バイナリストリーム (**Type** は **adtypebinary**) の場合は、 [Read](./read-method.md)を使用します。  
  
 ADO (ActiveX Data Object) ストリームオブジェクトの **ReadText** メソッドによって返される大量の XML データを生成するクエリは、実行に時間がかかることがあります。これが ASP ページから呼び出された COM + コンポーネントで実行された場合、ユーザーのセッションがタイムアウトすることがあります。ADO は、ストリームオブジェクトデータを UTF-8 エンコードから Unicode に変換します。大量のデータを一度に変換するために頻繁に使用されるメモリの再割り当てには、かなりの時間がかかります。 解決するには、ADO command オブジェクトの **ReadText** メソッドを繰り返し呼び出し、より少ない文字数を指定します。 テストでは、128K (131072) に相当する値が最適であることが示されています。 この値が減少すると応答時間が短縮されます。 詳細については、サポート技術情報の記事280067「」を参照してください。 "PRB: ADO stream オブジェクトの ReadText メソッドを使用して SQL Server 2000 から非常に大きな XML ドキュメントを取得するには、Microsoft サポート技術情報の「」を参照してください https://support.microsoft.com 。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Read メソッド](./read-method.md)