---
description: Status プロパティの例 (Field) (VB)
title: Status プロパティの例 (Field) (VB) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
author: rothja
ms.author: jroth
ms.openlocfilehash: 23a6ebaa724e06ce4a8283b95e3d7a982c8deef1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988697"
---
# <a name="status-property-example-field-vb"></a>Status プロパティの例 (Field) (VB)
次の例では、 [インターネット発行プロバイダー](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を使用して、読み取り/書き込みフォルダーからドキュメントを開きます。 [レコード](./record-object-ado.md)の[Field](./field-object.md)オブジェクトの[Status](./status-property-ado-field.md)プロパティは、最初に**adfieldpendinginsert**に設定され、次に**adFieldOk**に更新されます。  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=https://MyServer/"  
   Cnxn.Open strCnxn  
  
   Set File = New ADODB.Record  
   strFile = "Folder/FileName"  
   ' Open a read/write document  
   File.Source = strFile  
   File.ActiveConnection = Cnxn  
   File.Mode = adModeReadWrite  
   File.Open  
  
   Debug.Print "Append a couple of fields"  
  
   File.Fields.Append "chektest:fld1", adWChar, 42, adFldUpdatable, "fld1"  
   File.Fields.Append "chektest:fld2", adWChar, 42, adFldUpdatable, "fld2"  
  
   Debug.Print "status for the fields"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert  
  
    'turn off error-handling to verify field status  
   On Error Resume Next  
  
   File.Fields.Update  
  
   Debug.Print "Update succeeds"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert + adFieldUnavailable  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert + adFieldUnavailable  
  
    ' resume default error-handling  
   On Error GoTo 0  
  
     ' clean up  
    File.Close  
    Cnxn.Close  
    Set File = Nothing  
    Set Cnxn = Nothing  
  
End Sub  
'EndStatusFieldVB  
```  
  
 次の例では、ドキュメントから開かれた**レコード**から既知の**フィールド**を削除します。 **Status**プロパティは、まず**adFieldOK**、次に**adfieldpendingunknown**に設定されます。  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 次のコードは、読み取り専用のドキュメントで開かれている**レコード**から**フィールド**を削除します。 **状態** は **adfieldpendingdelete**に設定されます。 [更新](./update-method.md)時には、削除は失敗し、**状態**は**Adfieldpendingdelete**プラス**adfieldpermissiondenied**になります。 [CancelUpdate](./cancelupdate-method-ado.md) は、保留中の **状態** の設定をクリアします。  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>参照  
 [Field オブジェクト](./field-object.md)   
 [Record オブジェクト (ADO)](./record-object-ado.md)   
 [Status プロパティ (ADO Field)](./status-property-ado-field.md)