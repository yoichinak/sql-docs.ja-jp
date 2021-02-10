---
description: Size プロパティ (ADO Stream)
title: Size プロパティ (ADO Stream) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
author: rothja
ms.author: jroth
ms.openlocfilehash: eefb2271372a6746c2df9c3f052760bb35d7f8ea
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100040592"
---
# <a name="size-property-ado-stream"></a>Size プロパティ (ADO Stream)
ストリームのサイズをバイト数で示します。  
  
## <a name="return-values"></a>戻り値  
 ストリームのサイズをバイト数で指定する **Long 型** の値を返します。 既定値はストリームのサイズです。ストリームのサイズが不明な場合は-1 です。  
  
## <a name="remarks"></a>解説  
 **Size** は、開いている [ストリーム](./stream-object-ado.md) オブジェクトでのみ使用できます。  
  
> [!NOTE]
>  **ストリーム** オブジェクトには任意の数のビットを格納でき、システムリソースによってのみ制限されます。 **ストリーム** に **Long 型** の値で表すことができるビットよりも多くのビットが含まれている場合、**サイズ** が切り捨てられるため、**ストリーム** の長さを正確に表すことはできません。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Size プロパティ (ADO Parameter)](./size-property-ado-parameter.md)