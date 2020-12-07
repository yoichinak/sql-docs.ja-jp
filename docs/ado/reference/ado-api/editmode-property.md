---
description: EditMode プロパティ
title: EditMode プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
author: rothja
ms.author: jroth
ms.openlocfilehash: b6dd04a089d5a28a7eec3b67ebe1c48fe563ff69
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973833"
---
# <a name="editmode-property"></a>EditMode プロパティ
現在のレコードの編集状態を示します。  
  
## <a name="return-value"></a>戻り値  
 [Editmodeenum](../../../ado/reference/ado-api/editmodeenum.md)値を返します。  
  
## <a name="remarks"></a>解説  
 ADO は、現在のレコードに関連付けられている編集バッファーを保持します。 このプロパティは、このバッファーに変更が加えられたかどうか、または新しいレコードが作成されたかどうかを示します。 現在のレコードの編集状態を確認するには、 **EditMode** プロパティを使用します。 編集プロセスが中断されている場合は、保留中の変更をテストし、 [Update](../../../ado/reference/ado-api/update-method.md) または [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) メソッドを使用する必要があるかどうかを判断できます。  
  
 *即時更新モード*では、**更新**メソッドが正常に呼び出された後に、 **EditMode**プロパティが**adEditNone**にリセットされます。 [削除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)を呼び出すと、データソース内のレコードが正常に削除されない (参照整合性違反があるなど) 場合、[レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)は編集モード (**EditMode**  =  **adEditInProgress**) のままになります。 したがって、現在のレコードから移動する前に、 **CancelUpdate** を呼び出す必要があります (たとえば、 [Move](../../../ado/reference/ado-api/move-method-ado.md)、 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)、 [Close](../../../ado/reference/ado-api/close-method-ado.md) など)。  
  
 *バッチ更新モード*(プロバイダーは、複数の変更をキャッシュし、それらを基になるデータソースに書き込むのは[、UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)メソッドを呼び出す場合のみ)、最初の操作が実行されるときには、**更新**メソッドの呼び出しによって**EditMode**プロパティの値が変更されます。 後続の操作では、異なる操作が実行された場合でも、 **EditMode** プロパティの値は変更されません。 たとえば、最初の操作で新しいレコードを追加し、2番目の操作で既存のレコードを変更する場合、 **EditMode** のプロパティは引き続き **adEditAdd**になります。 **EditMode**プロパティは、 **UpdateBatch**の呼び出しが終わるまで**adEditNone**にリセットされません。 実行された操作を特定するには、 [Filter](../../../ado/reference/ado-api/filter-property.md) プロパティを [adfilterpending](../../../ado/reference/ado-api/filtergroupenum.md) に設定します。これにより、保留中の変更のあるレコードのみが表示され、各レコードの [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) プロパティを調べて、データに加えられた変更を確認できます。  
  
> [!NOTE]
>  **EditMode** は、現在のレコードがある場合にのみ、有効な値を返すことができます。 [BOF または EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)が true の場合、または現在のレコードが削除されている場合、 **EditMode**はエラーを返します。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [CursorType、LockType、および EditMode プロパティの例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType、および EditMode プロパティの例 (VC + +)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew メソッド (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Delete メソッド (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [CancelUpdate メソッド (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update メソッド](../../../ado/reference/ado-api/update-method.md)
