---
description: StayInSync プロパティ
title: StayInSync Property |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::StayInSync
- Recordset20::put_StayInSync
- Recordset20::PutStayInSync
- Recordset20::get_StayInSync
- Recordset20::GetStayInSync
helpviewer_keywords:
- StayInSync property
ms.assetid: 502d69b5-dc9a-455d-b115-a03bd39a552b
author: rothja
ms.author: jroth
ms.openlocfilehash: 9677a776273e83ad31fecde3a7ea436138d3784e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988623"
---
# <a name="stayinsync-property"></a>StayInSync プロパティ
親の行位置が変更されたときに、基になる子レコード (つまり、*チャプター*) への参照が変更されるかどうかを階層[レコードセット](./recordset-object-ado.md)オブジェクトで示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **ブール**値を設定または返します。 既定値は **True** です。 **True**の場合、親の**Recordset**オブジェクトが行の位置を変更すると、チャプターが更新されます。**False**の場合、親の**Recordset**オブジェクトが行の位置を変更した場合でも、チャプターは前の章のデータを参照し続けます。  
  
## <a name="remarks"></a>解説  
 このプロパティは、 [OLE DB 用の Microsoft データ整形サービス](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)によってサポートされるレコードセットなどの階層的なレコードセットに適用されます。子**レコード**セットを取得する前に、親**レコード**セットに設定する必要があります。 このプロパティは、階層的なレコードセットの移動を簡略化します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [StayInSync プロパティの例 (VB)](./stayinsync-property-example-vb.md)   
 [OLE DB 用の Microsoft データ整形サービス (ADO サービスプロバイダー)](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)