---
description: Flush メソッド (ADO)
title: Flush メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Stream::Flush
- _Stream::raw_Flush
helpviewer_keywords:
- Flush method [ADO]
ms.assetid: 938522b4-f836-4c80-8d27-a598a000f0ee
author: rothja
ms.author: jroth
ms.openlocfilehash: ce390555df75e2fd1d1a9a68257ba5952ee482f0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99167294"
---
# <a name="flush-method-ado"></a>Flush メソッド (ADO)
ADO バッファーに残っている [ストリーム](./stream-object-ado.md) の内容を、 **ストリーム** が関連付けられている基になるオブジェクトに強制的に適用します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>解説  
 このメソッドは、ストリームバッファーの内容を基になるオブジェクトに送信するために使用できます。たとえば、 **ストリーム** オブジェクトのソースである URL によって表されるノードやファイルなどです。 **ストリーム** のコンテンツに対して行われたすべての変更が書き込まれたことを確認する場合は、このメソッドを呼び出す必要があります。 ただし、ado では、通常は **Flush** を呼び出す必要がありません。これは、ado がバックグラウンドでできるだけバッファーをフラッシュするためです。 **ストリーム** の内容に対する変更は自動的に行われ、**フラッシュ** が呼び出されるまではキャッシュされません。  
  
 [Close](./close-method-ado.md)メソッドを使用して **ストリーム** を閉じると、**ストリーム** の内容が自動的にフラッシュされます。**閉じる** 直前に **Flush** を明示的に呼び出す必要はありません。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)