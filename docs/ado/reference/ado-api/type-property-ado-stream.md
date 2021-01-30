---
description: Type プロパティ (ADO Stream)
title: Type プロパティ (ADO Stream) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
author: rothja
ms.author: jroth
ms.openlocfilehash: 61e170cd368771fc75c2c6e552d4465dfe51866c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99166379"
---
# <a name="type-property-ado-stream"></a>Type プロパティ (ADO Stream)
[ストリーム](./stream-object-ado.md)に格納されているデータの型 (バイナリまたはテキスト) を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **ストリーム** オブジェクトに格納されているデータの型を指定する [streamtypeenum](./streamtypeenum.md)値を設定または返します。 既定値は **adTypeText** です。 ただし、バイナリデータが最初に新しい空の **ストリーム** に書き込まれる場合、その **型** は **adtypebinary** に変更されます。  
  
## <a name="remarks"></a>コメント  
 **Type** プロパティは、現在の位置が **ストリーム** の先頭 ([位置](./position-property-ado.md)が 0) であり、他の任意の位置で読み取り専用である場合にのみ、読み取り/書き込みになります。  
  
 **Type** プロパティによって、**ストリーム** の読み取りと書き込みに使用するメソッドが決まります。 テキスト **ストリーム** の場合は、 [ReadText](./readtext-method.md) と [WriteText](./writetext-method.md)を使用します。 バイナリ **ストリーム** の場合は、 [読み取り](./read-method.md) と [書き込み](./write-method.md)を使用します。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [RecordType プロパティ (ADO)](./recordtype-property-ado.md)   
 [Type プロパティ (ADO)](./type-property-ado.md)