---
description: MarshalOptions プロパティ (ADO)
title: MarshalOptions プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
author: rothja
ms.author: jroth
ms.openlocfilehash: 2d825a56123965fa95605e913354f6ea34db04ea
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99170882"
---
# <a name="marshaloptions-property-ado"></a>MarshalOptions プロパティ (ADO)
サーバーにマーシャリングされるレコード [セット](./recordset-object-ado.md) のレコードを示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 [Marshaloptionsenum](./marshaloptionsenum.md)値を設定または返します。 既定値は **Admarshalall** です。  
  
## <a name="remarks"></a>コメント  
 クライアント側の [レコードセット](./recordset-object-ado.md)を使用すると、クライアントで変更されたレコードが、スレッドまたはプロセスの境界を越えてパッケージ化および送信するプロセスであるマーシャリングと呼ばれる手法によって、中間層または Web サーバーに書き戻されます。 変更したリモートデータを中間層または Web サーバーに戻すためにマーシャリングする場合、 **Marshaloptions** プロパティを設定するとパフォーマンスが向上します。  
  
> [!NOTE]
>  **リモートデータサービスの使用状況** このプロパティは、クライアント側の **レコードセット** でのみ使用されます。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [MarshalOptions プロパティの例 (VB)](./marshaloptions-property-example-vb.md)   
 [MarshalOptions プロパティの例 (VC++)](./marshaloptions-property-example-vc.md)