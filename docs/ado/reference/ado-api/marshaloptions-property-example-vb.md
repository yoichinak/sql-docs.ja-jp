---
description: MarshalOptions プロパティの例 (VB)
title: MarshalOptions プロパティの例 (VB) |Microsoft Docs
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
- MarshalOptions property [ADO], Visual Basic example
ms.assetid: ae576b2c-65aa-4838-872a-85e618806dc8
author: rothja
ms.author: jroth
ms.openlocfilehash: 08ac6a07341c37e412a6bc030e37e04a8ff8e787
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990663"
---
# <a name="marshaloptions-property-example-vb"></a>MarshalOptions プロパティの例 (VB)
この例では、 [Marshaloptions](./marshaloptions-property-ado.md) プロパティを使用して、サーバーに送信される行を指定します。すべての行または変更された行のみが返されます。  
  
```  
'BeginMarshalOptionsVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim rstEmployees As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLEmployees As String  
  
    Dim strOldFirst As String  
    Dim strOldLast As String  
    Dim strMessage As String  
    Dim strMarshalAll As String  
    Dim strMarshalModified As String  
  
    ' Open connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open strCnxn  
  
    ' open recordset with names from Employees table  
    ' and set some properties through object refs  
    Set rstEmployees = New ADODB.Recordset  
    rstEmployees.CursorType = adOpenKeyset  
    rstEmployees.LockType = adLockOptimistic  
    rstEmployees.CursorLocation = adUseClient  
  
    strSQLEmployees = "SELECT fname, lname FROM Employee ORDER BY lname"  
  
    rstEmployees.Open strSQLEmployees, Cnxn, , , adCmdText  
     ' empty properties have been set above  
  
     ' Store original data  
    strOldFirst = rstEmployees!fname  
    strOldLast = rstEmployees!lname  
  
    ' Change data in edit buffer  
    rstEmployees!fname = "Linda"  
    rstEmployees!lname = "Kobara"  
  
    ' Show contents of buffer and get user input  
    strMessage = "Edit in progress:" & vbCr & _  
        " Original data = " & strOldFirst & " " & _  
        strOldLast & vbCr & " Data in buffer = " & _  
        rstEmployees!fname & " " & rstEmployees!lname & vbCr & vbCr & _  
        "Use Update to replace the original data with " & _  
        "the buffered data in the Recordset?"  
    strMarshalAll = "Would you like to send all the rows " & _  
        "in the recordset back to the server?"  
    strMarshalModified = "Would you like to send only " & _  
        "modified rows back to the server?"  
  
    If MsgBox(strMessage, vbYesNo) = vbYes Then  
        If MsgBox(strMarshalAll, vbYesNo) = vbYes Then  
            rstEmployees.MarshalOptions = adMarshalAll  
            rstEmployees.Update  
        ElseIf MsgBox(strMarshalModified, vbYesNo) = vbYes Then  
            rstEmployees.MarshalOptions = adMarshalModifiedOnly  
            rstEmployees.Update  
        End If  
    End If  
  
    ' sShow the resulting data  
    MsgBox "Data in recordset = " & rstEmployees!fname & " " & _  
        rstEmployees!lname  
  
    ' restore original data because this is a demonstration  
    If Not (strOldFirst = rstEmployees!fname And _  
            strOldLast = rstEmployees!lname) Then  
        rstEmployees!fname = strOldFirst  
        rstEmployees!lname = strOldLast  
        rstEmployees.Update  
    End If  
  
    ' clean up  
    rstEmployees.Close  
    Cnxn.Close  
    Set rstEmployees = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndMarshalOptionsVB  
```  
  
## <a name="see-also"></a>参照  
 [MarshalOptions プロパティ (ADO)](./marshaloptions-property-ado.md)   
 [MarshalOptionsEnum](./marshaloptionsenum.md)