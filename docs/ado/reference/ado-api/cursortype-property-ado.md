---
description: CursorType プロパティ (ADO)
title: CursorType プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CursorType
helpviewer_keywords:
- CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
author: rothja
ms.author: jroth
ms.openlocfilehash: 5401b5b5b9e91b6b851f70d2d3a7e19f5e5d7a82
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974323"
---
# <a name="cursortype-property-ado"></a>CursorType プロパティ (ADO)
[レコードセット](./recordset-object-ado.md)オブジェクトで使用されるカーソルの種類を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 [カーソル Typeenum](./cursortypeenum.md)値を設定または返します。 既定値は **adOpenForwardOnly**です。  
  
## <a name="remarks"></a>解説  
 **CursorType**プロパティを使用して、**レコードセット**オブジェクトを開くときに使用するカーソルの種類を指定します。  
  
 [カーソル位置](./cursorlocation-property-ado.md)プロパティが**adUseClient**に設定されている場合は、 **adopenstatic**の設定のみがサポートされます。 サポートされていない値が設定されている場合、エラーは発生しません。サポートされている最も近い **CursorType** が代わりに使用されます。  
  
 要求されたカーソルの種類がプロバイダーでサポートされていない場合は、別の種類のカーソルが返されることがあります。 **CursorType**プロパティは、 [Recordset](./recordset-object-ado.md)オブジェクトが開いているときに使用される実際のカーソルの種類に合わせて変更されます。 返されたカーソルの特定の機能を確認するには、 [Supports](./supports-method.md) メソッドを使用します。 **レコードセット**を閉じると、 **CursorType**プロパティが元の設定に戻ります。  
  
 次の表は、各カーソルの種類に必要なプロバイダーの機能 (で識別されます **) を示し** ています。  
  
|この CursorType のレコードセットの場合|サポートメソッドは、これらのすべての定数に対して True を返す必要があります。|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|なし|  
|**adOpenKeyset**|**Adbookmark**、 **adHoldRecords**、 **adMovePrevious**、 **adbookmark**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**Adbookmark**、 **adHoldRecords**、 **adMovePrevious**、 **adbookmark**|  
  
> [!NOTE]
>  では、動的カーソルと順方向専用カーソルに対して **サポート**(**adupdatebatch**) が true である場合がありますが、バッチ更新の場合は、キーセットまたは静的カーソルのいずれかを使用する必要があります。 [LockType](./locktype-property-ado.md)プロパティを**Adlockbatchoptimistic**に設定し、Cursor **location**プロパティを**adUseClient**に設定して、バッチの更新に必要な OLE DB のカーソルサービスを有効にします。  
  
 **CursorType**プロパティは、**レコードセット**が閉じられている場合は読み取り/書き込み、開いている場合は読み取り専用になります。  
  
> [!NOTE]
>  **リモートデータサービスの使用状況** クライアント側の **レコードセット** オブジェクトで使用する場合、 **CursorType** プロパティは **adopenstatic**にのみ設定できます。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [CursorType、LockType、および EditMode プロパティの例 (VB)](./cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType、および EditMode プロパティの例 (VC + +)](./cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports メソッド](./supports-method.md)