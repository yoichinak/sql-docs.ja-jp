---
description: OriginalValue プロパティと UnderlyingValue プロパティの例 (VB)
title: OriginalValue プロパティと UnderlyingValue プロパティの例 (VB) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- UnderlyingValue property [ADO], Visual Basic example
- OriginalValue property [ADO]
ms.assetid: 1750804b-d7ef-47d6-8d73-1f51fa1cbe4a
author: rothja
ms.author: jroth
ms.openlocfilehash: d77e8e0856830d76e9d431ffeb3ae9687a1f1e8d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99170661"
---
# <a name="originalvalue-and-underlyingvalue-properties-example-vb"></a>OriginalValue プロパティと UnderlyingValue プロパティの例 (VB)
この例では、レコードの基になるデータがレコード[セット](./recordset-object-ado.md)のバッチ更新中に変更された場合にメッセージを表示することによって、 [Originalvalue](./originalvalue-property-ado.md)プロパティと[UnderlyingValue](./underlyingvalue-property.md)プロパティを示します。  
  
```  
'BeginOriginalValueVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstTitles As ADODB.Recordset  
    Dim fldType As ADODB.Field  
    Dim strCnxn As String  
    Dim strSQLTitles As String  
  
    ' Open connection.  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset for batch update  
    ' using object refs to set properties  
    Set rstTitles = New ADODB.Recordset  
    Set rstTitles.ActiveConnection = Cnxn  
    rstTitles.CursorType = adOpenKeyset  
    rstTitles.LockType = adLockBatchOptimistic  
    strSQLTitles = "titles"  
    rstTitles.Open strSQLTitles  
  
    ' Set field object variable for Type field  
    Set fldType = rstTitles!Type  
  
    ' Change the type of psychology titles  
    Do Until rstTitles.EOF  
        If Trim(fldType) = "psychology" Then  
            fldType = "self_help"  
        End If  
        rstTitles.MoveNext  
    Loop  
  
    ' Similate a change by another user by updating  
    ' data using a command string  
    Cnxn.Execute "UPDATE Titles SET type = 'sociology' " & _  
       "WHERE type = 'psychology'"  
  
    'Check for changes  
    rstTitles.MoveFirst  
    Do Until rstTitles.EOF  
        If fldType.OriginalValue <> fldType.UnderlyingValue Then  
            MsgBox "Data has changed!" & vbCr & vbCr & _  
                "  Title ID: " & rstTitles!title_id & vbCr & _  
                "  Current value: " & fldType & vbCr & _  
                "  Original value: " & _  
                fldType.OriginalValue & vbCr & _  
                "  Underlying value: " & _  
                fldType.UnderlyingValue & vbCr  
        End If  
    rstTitles.MoveNext  
    Loop  
  
    ' Cancel the update because this is a demonstration  
    rstTitles.CancelBatch  
  
    ' Restore original values  
    Cnxn.Execute "UPDATE Titles SET type = 'psychology' " & _  
        "WHERE type = 'sociology'"  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then rstTitles.Close  
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
'EndOriginalValueVB  
```  
  
## <a name="see-also"></a>参照  
 [OriginalValue プロパティ (ADO)](./originalvalue-property-ado.md)   
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)   
 [UnderlyingValue プロパティ](./underlyingvalue-property.md)