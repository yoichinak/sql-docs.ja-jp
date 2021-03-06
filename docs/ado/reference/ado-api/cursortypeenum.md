---
description: CursorTypeEnum
title: カーソルの Typeenum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- CursorTypeEnum
helpviewer_keywords:
- CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
author: rothja
ms.author: jroth
ms.openlocfilehash: 9ce49416e2cb298e4829022b7da0840a5e2c516a
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100025868"
---
# <a name="cursortypeenum"></a>CursorTypeEnum
[レコードセット](./recordset-object-ado.md)オブジェクトで使用されるカーソルの種類を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|動的カーソルを使用します。 他のユーザーによる追加、変更、および削除が表示され、プロバイダーがサポートしていない場合は、ブックマークを除くすべての種類の **移動が許可され** ます。|  
|**adOpenForwardOnly**|0|既定値。 順方向専用カーソルを使用します。 レコードをスクロールするだけでスクロールできる点を除いて、静的カーソルと同じです。 これにより、 **レコードセット** のパススルーを1回だけ行う必要がある場合に、パフォーマンスが向上します。|  
|**adOpenKeyset**|1|キーセットカーソルを使用します。 動的カーソルと同様に、他のユーザーが追加したレコードは表示されませんが、他のユーザーが削除したレコードにはレコード **セット** からアクセスできません。 他のユーザーによるデータの変更は引き続き表示されます。|  
|**adOpenStatic**|3|静的カーソルを使用します。これは、データの検索やレポートの生成に使用できる一連のレコードの静的なコピーです。 他のユーザーによる追加、変更、または削除は表示されません。|  
|**adOpenUnspecified**|-1|カーソルの種類を指定しません。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums CursorType|  
|AdoEnums. CursorType. FORWARDONLY|  
|AdoEnums CursorType|  
|AdoEnums CursorType|  
|AdoEnums. CursorType|  
  
## <a name="applies-to"></a>適用対象  
 [CursorType プロパティ (ADO)](./cursortype-property-ado.md)