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
ms.openlocfilehash: c4df6f318afaed7bbbc7a3302be2b1c6a15a5c1d
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100033959"
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