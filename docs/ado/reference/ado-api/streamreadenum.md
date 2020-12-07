---
description: StreamReadEnum
title: StreamReadEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamReadEnum
helpviewer_keywords:
- StreamReadEnum enumeration [ADO]
ms.assetid: cfa1b416-003a-436f-a21b-bd2397e54db3
author: rothja
ms.author: jroth
ms.openlocfilehash: d9f685a80d822950a159ddb3fbc9f148489a723e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988473"
---
# <a name="streamreadenum"></a>StreamReadEnum
ストリーム全体または次の行を [ストリーム](./stream-object-ado.md) オブジェクトから読み取るかどうかを指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adReadAll**|-1|既定値。 ストリームから、現在の位置から [EOS](./eos-property.md) マーカーまでのすべてのバイトを読み取ります。 これは、バイナリストリームを持つ唯一の有効な **Streamreadenum** 値です ([Type](./type-property-ado-stream.md) は **adtypebinary**です)。|  
|**adReadLine**|-2|( [Lineseparator](./lineseparator-property-ado.md) プロパティによって指定された) ストリームから次の行を読み取ります。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 これらの定数には、対応する ADO/WFC がありません。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Read メソッド](./read-method.md)  
    :::column-end:::
    :::column:::
        [ReadText メソッド](./readtext-method.md)  
    :::column-end:::
:::row-end:::