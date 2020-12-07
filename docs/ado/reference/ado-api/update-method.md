---
description: Update メソッド
title: Update メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
author: rothja
ms.author: jroth
ms.openlocfilehash: bb673de86d48143a8869460eeab3377f3c0ec0d2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988103"
---
# <a name="update-method"></a>Update メソッド
レコード[セット](./recordset-object-ado.md)オブジェクトの現在の行、または[レコード](./record-object-ado.md)オブジェクトの[Fields](./fields-collection-ado.md)コレクションに対して行ったすべての変更を保存します。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>パラメーター  
 *フィールド*  
 省略可能。 1つの名前、または変更するフィールドの名前または序数を表す**バリアント**配列を**表すバリアント配列**。  
  
 *値*  
 省略可能。 単一の値を表す **バリアント** 、または新しいレコードのフィールドの値を表す **バリアント** 配列。  
  
## <a name="remarks"></a>解説  
  
## <a name="recordset"></a>レコードセット  
 [AddNew](./addnew-method-ado.md)メソッドを呼び出した後、または既存のレコードのフィールド値を変更した後に、**レコードセット**オブジェクトの現在のレコードに対して行った変更を保存するには、 **Update**メソッドを使用します。 **レコードセット**オブジェクトは更新をサポートしている必要があります。  
  
 フィールドの値を設定するには、次のいずれかの操作を行います。  
  
-   [フィールド](./field-object.md)オブジェクトの[Value](./value-property-ado.md)プロパティに値を割り当て、 **Update**メソッドを呼び出します。  
  
-   **Update**呼び出しを使用して、フィールド名と値を引数として渡します。  
  
-   **更新**呼び出しを使用して、フィールド名の配列と値の配列を渡します。  
  
 フィールドと値の配列を使用する場合、両方の配列に同じ数の要素を指定する必要があります。 また、フィールド名の順序は、フィールド値の順序と一致している必要があります。 フィールドと値の数と順序が一致しない場合は、エラーが発生します。  
  
 **レコードセット**オブジェクトでバッチ更新がサポートされている場合は、 [UpdateBatch](./updatebatch-method.md)メソッドを呼び出すまで、1つ以上のレコードに対して複数の変更をローカルにキャッシュできます。 現在のレコードを編集している場合、または **UpdateBatch** メソッドを呼び出したときに新しいレコードを追加している場合、ADO は **Update** メソッドを自動的に呼び出して、保留中の変更を現在のレコードに保存してから、バッチされた変更をプロバイダーに送信します。  
  
 **更新**メソッドを呼び出す前に追加または編集しているレコードから移動すると、ADO は自動的に**update**を呼び出して変更を保存します。 現在のレコードに対して行われた変更を取り消す場合や、新しく追加したレコードを破棄する場合は、 [CancelUpdate](./cancelupdate-method-ado.md) メソッドを呼び出す必要があります。  
  
 **Update**メソッドを呼び出した後、現在のレコードは最新のままです。  
  
## <a name="record"></a>Record  
 **Update**メソッドは、**レコード**オブジェクトの[fields](./fields-collection-ado.md)コレクション内のフィールドの追加、削除、および更新を終了します。  
  
 たとえば、 **Delete** メソッドを使用して削除されたフィールドは、直ちに削除対象としてマークされますが、コレクション内に残ります。 これらのフィールドをプロバイダーのコレクションから実際に削除するには、 **Update** メソッドを呼び出す必要があります。  
  
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
 [CancelUpdate メソッド (ADO)](./cancelupdate-method-ado.md)   
 [EditMode プロパティ](./editmode-property.md)   
 [UpdateBatch メソッド](./updatebatch-method.md)