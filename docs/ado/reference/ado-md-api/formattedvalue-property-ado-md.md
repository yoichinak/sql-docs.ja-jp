---
description: FormattedValue プロパティ (ADO MD)
title: FormattedValue プロパティ (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Cell::FormattedValue
- FormattedValue
helpviewer_keywords:
- FormattedValue property [ADO MD]
ms.assetid: 5c06451e-06ec-4da6-9a87-2d043469248a
author: rothja
ms.author: jroth
ms.openlocfilehash: aba336cff29c02f1468ed1763d005990cc465adb
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100054757"
---
# <a name="formattedvalue-property-ado-md"></a>FormattedValue プロパティ (ADO MD)
[セル](./cell-object-ado-md.md)値の書式設定された表示を示します。  
  
## <a name="return-values"></a>戻り値  
 は **文字列** を返し、読み取り専用です。  
  
## <a name="remarks"></a>解説  
 [Cell](./cell-object-ado-md.md)オブジェクトの [value](./value-property-ado-md.md)プロパティの書式設定された表示値を取得するには、 **FormattedValue** プロパティを使用します。 たとえば、セルの値が1056.87 で、この値がドルの金額を表している場合、 **FormattedValue** は $1056.87 になります。  
  
## <a name="applies-to"></a>適用対象  
 [Cell オブジェクト (ADO MD)](./cell-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [セルセットの例 (VB)](./cellset-example-vb.md)   
 [Value プロパティ (ADO MD)](./value-property-ado-md.md)