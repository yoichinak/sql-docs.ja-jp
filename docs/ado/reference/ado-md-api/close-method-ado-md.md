---
description: Close メソッド (ADO MD)
title: Close メソッド (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f4f0c1613b1ca0e33a4f325dbe3e326d56f76e6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987113"
---
# <a name="close-method-ado-md"></a>Close メソッド (ADO MD)
開いているセルセットを閉じます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>解説  
 **Close**メソッドを使用して[セルセット](./cellset-object-ado-md.md)オブジェクトを閉じると、関連する[セル](./cell-object-ado-md.md)、[軸](./axis-object-ado-md.md)、[位置](./position-object-ado-md.md)、または[メンバー](./member-object-ado-md.md)オブジェクトのデータを含む、関連付けられたデータが解放されます。 **セルセット**を閉じると、メモリからは削除されません。プロパティの設定を変更し、後でもう一度開くことができます。 メモリからオブジェクトを完全に削除するには、オブジェクト変数を **Nothing**に設定します。  
  
 後で [Open](./open-method-ado-md.md) メソッドを呼び出して、同じまたは別のソース文字列を使用して **セルセット** を再び開くことができます。 **Cellset**オブジェクトが閉じられている間に、プロパティを取得したり、基になるデータまたはメタデータを参照するメソッドを呼び出したりすると、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [CellSet オブジェクト (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [Axis オブジェクト (ADO MD)](./axis-object-ado-md.md)   
 [Cell オブジェクト (ADO MD)](./cell-object-ado-md.md)   
 [Member オブジェクト (ADO MD)](./member-object-ado-md.md)   
 [Open メソッド (ADO MD)](./open-method-ado-md.md)   
 [Position オブジェクト (ADO MD)](./position-object-ado-md.md)   
 [State プロパティ (ADO MD)](./state-property-ado-md.md)