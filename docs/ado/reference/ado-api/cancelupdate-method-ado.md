---
description: CancelUpdate メソッド (ADO)
title: CancelUpdate メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CancelUpdate
helpviewer_keywords:
- CancelUpdate method [ADO]
ms.assetid: eaa856cc-c786-462e-890c-c896261b1741
author: rothja
ms.author: jroth
ms.openlocfilehash: 2355d2a0b2ff0bbe14eb9b7d2a9a373164a4f5e5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975563"
---
# <a name="cancelupdate-method-ado"></a>CancelUpdate メソッド (ADO)
[Update](./update-method.md)メソッドを呼び出す前に、[レコードセット](./recordset-object-ado.md)オブジェクトの現在または新しい行、または[レコード](./record-object-ado.md)オブジェクトの[Fields](./fields-collection-ado.md)コレクションに対して行われたすべての変更をキャンセルします。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.CancelUpdaterecord.Fields.CancelUpdate  
```  
  
## <a name="remarks"></a>解説  
  
## <a name="recordset"></a>レコードセット  
 **CancelUpdate**メソッドを使用して、現在の行に対して行われた変更を取り消すか、新しく追加した行を破棄します。 **Update**メソッドを呼び出した後、現在の行または新しい行への変更を取り消すことはできません。ただし、変更がトランザクションの一部である場合は、 [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)メソッドを使用してロールバックするか、バッチ更新の一部にする必要があります。 バッチ更新の場合は、 **CancelUpdate**または[CancelBatch](./cancelbatch-method-ado.md)メソッドを使用して**更新**を取り消すことができます。  
  
 **CancelUpdate**メソッドを呼び出すときに新しい行を追加する場合、現在の行は、 [AddNew](./addnew-method-ado.md)呼び出しの前の現在の行になります。  
  
 編集モードで、移動、 [NextRecordset](./nextrecordset-method-ado.md)、または[閉じる](./close-method-ado.md)メソッドを使用して、現在のレコードから移動する場合は、 **CancelUpdate**を使用して保留[中の変更](./move-method-ado.md)を取り消すことができます。 更新をデータソースに正常に送信できない場合は、この操作が必要になることがあります。 たとえば、参照整合性違反によって失敗した削除を試みた場合、[削除](./delete-method-ado-recordset.md)の呼び出し後に、**レコードセット**は編集モードのままになります。  
  
## <a name="record"></a>Record  
 **CancelUpdate**メソッドでは、[フィールド](./field-object.md)オブジェクトの保留中の挿入または削除がキャンセルされ、既存のフィールドの保留中の更新が取り消され、元の値に復元されます。 **Fields**コレクション内のすべてのフィールドの[Status](./status-property-ado-recordset.md)プロパティは、 **adFieldOK**に設定されています。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Fields コレクション (ADO)](./fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [Update および CancelUpdate メソッドの例 (VB)](./update-and-cancelupdate-methods-example-vb.md)   
 [Update および CancelUpdate メソッドの例 (VC + +)](./update-and-cancelupdate-methods-example-vc.md)   
 [AddNew メソッド (ADO)](./addnew-method-ado.md)   
 [Cancel メソッド (ADO)](./cancel-method-ado.md)   
 [Cancel メソッド (RDS)](../rds-api/cancel-method-rds.md)   
 [CancelBatch メソッド (ADO)](./cancelbatch-method-ado.md)   
 [CancelUpdate メソッド (RDS)](../rds-api/cancelupdate-method-rds.md)   
 [EditMode プロパティ](./editmode-property.md)   
 [Update メソッド](./update-method.md)