---
description: SetEOS メソッド
title: SetEOS メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b9685f0ca0b5e9bdd1b484c7d424308619307d9
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99170278"
---
# <a name="seteos-method"></a>SetEOS メソッド
ストリームの末尾である位置を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>解説  
 **SetEOS** は、現在 [位置](./position-property-ado.md)をストリームの末尾にすることによって、 [EOS](./eos-property.md)プロパティの値を更新します。 現在の位置の後に続くバイトまたは文字は切り捨てられます。  
  
 [Write](./write-method.md)、 [WriteText](./writetext-method.md)、および [CopyTo](./copyto-method-ado.md)では、既存の **ストリーム** オブジェクトの余分な値は切り捨てられないため、新しいストリームの末尾の位置を **SetEOS** で設定することにより、これらのバイトまたは文字を切り捨てることができます。  
  
> [!CAUTION]
>  **Eos** を実際のストリームの末尾の前の位置に設定すると、新しい **eos** 位置以降のすべてのデータが失われます。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)