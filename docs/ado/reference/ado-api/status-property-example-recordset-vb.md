---
description: Status プロパティの例 (Recordset) (VB)
title: Status プロパティの例 (レコードセット) (VB) |Microsoft Docs
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
- Status property [ADO Recordset], Visual Basic example
ms.assetid: e37b4d46-380d-4615-b4bb-e1a7b0851771
author: rothja
ms.author: jroth
ms.openlocfilehash: 0c8e417b86578500529820905beb3b16b0dc3a0f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988702"
---
# <a name="status-property-example-recordset-vb"></a>Status プロパティの例 (Recordset) (VB)
この例では、 [Status](./status-property-ado-recordset.md) プロパティを使用して、バッチ更新が行われる前にバッチ操作で変更されたレコードを表示します。  
  
```  
'BeginStatusRecordsetVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    ' connection and recordset variables  
    Dim rstTitles As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLTitles As String  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
     ' open recordset for batch update  
    Set rstTitles = New ADODB.Recordset  
    strSQLTitles = "Titles"  
    rstTitles.Open strSQLTitles, Cnxn, adOpenKeyset, adLockBatchOptimistic, adCmdTable  
  
    ' change the type of psychology titles  
    Do Until rstTitles.EOF  
        If Trim(rstTitles!Type) = "psychology" Then rstTitles!Type = "self_help"  
        rstTitles.MoveNext  
    Loop  
  
    ' display Title ID and status  
    rstTitles.MoveFirst  
    Do Until rstTitles.EOF  
        If rstTitles.Status = adRecModified Then  
            Debug.Print rstTitles!title_id & " - Modified"  
        Else  
            Debug.Print rstTitles!title_id  
        End If  
    rstTitles.MoveNext  
    Loop  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then  
            ' Cancel the update because this is a demonstration  
            rstTitles.CancelBatch  
            rstTitles.Close  
        End If  
    End If  
    Set rstTitles = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndStatusRecordsetVB  
```  
  
## <a name="see-also"></a>参照  
 [Status プロパティ (ADO Recordset)](./status-property-ado-recordset.md)