---
description: WriteText メソッド
title: WriteText メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
author: rothja
ms.author: jroth
ms.openlocfilehash: d38d493fb57e8147f882056d07514ba9f405ecf9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987723"
---
# <a name="writetext-method"></a>WriteText メソッド
指定したテキスト文字列を [ストリーム](./stream-object-ado.md) オブジェクトに書き込みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>パラメーター  
 *データ*  
 書き込む文字のテキストを含む **文字列** 値。  
  
 *Options*  
 省略可能。 指定した文字列の末尾に行区切り記号を書き込む必要があるかどうかを指定する [Streamwriteenum](./streamwriteenum.md) 値。  
  
## <a name="remarks"></a>解説  
 指定された文字列は、 **ストリーム** オブジェクトに書き込まれます。文字列の間にスペースや文字は含まれません。  
  
 現在の [位置](./position-property-ado.md) は、書き込まれたデータに続く文字に設定されます。 **WriteText**メソッドは、ストリーム内の残りのデータを切り捨てません。 これらの文字を切り捨てたい場合は、 [SetEOS](./seteos-method.md)を呼び出します。  
  
 現在の[EOS](./eos-property.md)位置を超えて書き込むと、**ストリーム**の[サイズ](./size-property-ado-stream.md)が新しい文字を含むように拡大され、 **EOS**は**ストリーム**の新しい最後のバイトに移動します。  
  
> [!NOTE]
>  **WriteText**メソッドはテキストストリームと共に使用されます ([型](./type-property-ado-stream.md)は**adTypeText**)。 バイナリストリーム (**Type** は **adtypebinary**) の場合は、 [Write](./write-method.md)を使用します。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Write メソッド](./write-method.md)