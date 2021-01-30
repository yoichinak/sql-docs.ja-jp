---
description: SkipLine メソッド
title: SkipLine メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Stream::raw_SkipLine
- _Stream::SkipLine
helpviewer_keywords:
- Skipline method [ADO]
ms.assetid: 0abc00fe-ee09-4c8e-b1f2-48ee9c5f3329
author: rothja
ms.author: jroth
ms.openlocfilehash: 826e90b65131453bb50cc70e3efbc3ad8796c89f
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99166533"
---
# <a name="skipline-method"></a>SkipLine メソッド
テキスト [ストリーム](./stream-object-ado.md)を読み取るときに、1行全体をスキップします。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.SkipLine  
```  
  
## <a name="remarks"></a>解説  
 次の行区切り記号までのすべての文字がスキップされます。 既定では、 [Lineseparator](./lineseparator-property-ado.md) は **adcrlf** です。 以前の [eos](./eos-property.md)をスキップしようとすると、現在の位置は **eos** のままになります。  
  
 **SkipLine** メソッドは、テキストストリームと共に使用されます ([型](./type-property-ado-stream.md)は **adTypeText**)。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)