---
description: LineSeparator プロパティ (ADO)
title: LineSeparator プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::LineSeparator
helpviewer_keywords:
- LineSeparator property [ADO]
ms.assetid: 0b20fbb8-6b83-48ec-b442-f96c8a4bafbb
author: rothja
ms.author: jroth
ms.openlocfilehash: 7bd1e14d5c7ebc84ea4736da08296eca0e02ea38
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990723"
---
# <a name="lineseparator-property-ado"></a>LineSeparator プロパティ (ADO)
テキスト [ストリーム](./stream-object-ado.md) オブジェクトの行区切り記号として使用されるバイナリ文字を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **ストリーム**で使用される行区切り文字を示す[LineSeparatorsEnum](./lineseparatorsenum.md)値を設定または返します。 既定値は **Adcrlf**です。  
  
## <a name="remarks"></a>解説  
 **Lineseparator** は、テキスト **ストリーム**の内容を読み取るときに、行を解釈するために使用されます。 [SkipLine](./skipline-method.md)メソッドでは、行をスキップできます。  
  
 **Lineseparator** は、テキスト **ストリーム** オブジェクトでのみ使用されます ([型](./type-property-ado-stream.md) は **adTypeText**)。 **Type**が**adtypebinary**の場合、このプロパティは無視されます。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)