---
description: Read メソッド
title: Read メソッド |Microsoft Docs
ms.prod: sql
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
author: rothja
ms.author: jroth
ms.openlocfilehash: 030627c58eb33d064b50c4e9347a06330f01cf9a
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100040792"
---
# <a name="read-method"></a>Read メソッド
バイナリ [ストリーム](./stream-object-ado.md) オブジェクトから、指定されたバイト数を読み取ります。  
  
## <a name="syntax"></a>構文  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *NumBytes*  
 任意。 ファイルから読み取るバイト数、または既定の [Streamreadenum](./streamreadenum.md)値 **adreadall** を指定する **Long** 値です。  
  
## <a name="return-value"></a>戻り値  
 **Read** メソッドは、指定されたバイト数またはストリーム全体を **ストリーム** オブジェクトから読み取り、結果のデータを **バリアント** として返します。  
  
## <a name="remarks"></a>解説  
 *Numbytes* が **ストリーム** の残りのバイト数よりも大きい場合は、残っているバイトだけが返されます。 読み取られたデータは、 *Numbytes* によって指定された長さと一致するように埋め込まれていません。 読み取るバイトが残っていない場合は、null 値を持つバリアントが返されます。 **Read** を使用して後方に読み取ることはできません。  
  
> [!NOTE]
>  *Numbytes* は常にバイトを計測します。 テキスト **ストリーム** オブジェクト ([型](./type-property-ado-stream.md) は **adTypeText**) の場合は、 [ReadText](./readtext-method.md)を使用します。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [ReadText メソッド](./readtext-method.md)