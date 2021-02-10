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
ms.openlocfilehash: 3c1b23ef249e2dd543772e1e414d347cc2377860
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100051433"
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