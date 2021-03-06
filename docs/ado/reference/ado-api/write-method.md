---
description: Write メソッド
title: Write メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Stream::raw_Write
- _Stream::Write
helpviewer_keywords:
- Write method [ADO]
ms.assetid: 02982e6a-ac5f-4af2-b82e-ce12534b84b2
author: rothja
ms.author: jroth
ms.openlocfilehash: 312eba9678843932103875acd2a170a2e98f148c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100056047"
---
# <a name="write-method"></a>Write メソッド
バイナリデータを [ストリーム](./stream-object-ado.md) オブジェクトに書き込みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.Write Buffer  
```  
  
#### <a name="parameters"></a>パラメーター  
 *バッファー*  
 書き込むバイト配列を格納している **Variant** 。  
  
## <a name="remarks"></a>解説  
 指定されたバイトは、各バイト間にスペースを入れずに **ストリーム** オブジェクトに書き込まれます。  
  
 現在の [位置](./position-property-ado.md) は、書き込まれたデータに続くバイトに設定されます。 **Write** メソッドは、ストリーム内の残りのデータを切り捨てません。 これらのバイトを切り捨てる場合は、 [SetEOS](./seteos-method.md)を呼び出します。  
  
 現在の [EOS](./eos-property.md)位置を超えて書き込む場合、**ストリーム** の [サイズ](./size-property-ado-stream.md)は新しいバイト数を含むように増加し、 **EOS** は **ストリーム** の新しい最後のバイトに移動します。  
  
> [!NOTE]
>  **Write** メソッドはバイナリストリームで使用されます ([Type](./type-property-ado-stream.md)は **adtypebinary** です)。 テキストストリーム (**型** は **adTypeText**) の場合は、 [WriteText](./writetext-method.md)を使用します。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [WriteText メソッド](./writetext-method.md)