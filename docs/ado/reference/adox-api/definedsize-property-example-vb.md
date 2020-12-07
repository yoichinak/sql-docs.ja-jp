---
description: DefinedSize プロパティの例 (VB)
title: "\"持つサイズ\" プロパティの例 (VB) |Microsoft Docs"
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
- DefinedSize property [ADOX], Visual Basic example
ms.assetid: 4dda2239-7ab5-4729-9c63-eb530803f7d9
author: rothja
ms.author: jroth
ms.openlocfilehash: e5c3010ce4e320ef0fd8a8bb1fbe09a5ebafad6b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984653"
---
# <a name="definedsize-property-example-vb"></a>DefinedSize プロパティの例 (VB)
この例では、[列](./column-object-adox.md)の "値の[サイズ](./definedsize-property-adox.md)" プロパティを示します。 コードによって、 *Northwind*データベースの**Employees**テーブルの FirstName 列のサイズが再定義されます。 次に、 **Employees**テーブルに基づいて[レコードセット](../ado-api/recordset-object-ado.md)の FirstName[フィールド](../ado-api/field-object.md)の値が変更されます。 既定では、"定義された **サイズ** " プロパティを再定義した後、[FirstName] フィールドに空白が埋め込まれていることに注意してください。  
  
```  
' BeginDefinedSizeVB  
Public Sub Main()  
    On Error GoTo DefinedSizeXError  
  
    Dim rstEmployees As ADODB.Recordset  
    Dim catNorthwind As New ADOX.Catalog  
    Dim colFirstName As ADOX.Column  
    Dim colNewFirstName As New ADOX.Column  
    Dim aryFirstName() As String  
    Dim i As Integer  
    Dim strCnn As String  
  
    strCnn = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
             "Data Source='Northwind.mdb';"  
  
    ' Open a Recordset for the Employees table.  
    Set rstEmployees = New ADODB.Recordset  
    rstEmployees.Open "Employees", strCnn, adOpenKeyset, , adCmdTable  
    ReDim aryFirstName(rstEmployees.RecordCount)  
  
    ' Open a Catalog for the Northwind database,  
    ' using same connection as rstEmployees  
    Set catNorthwind.ActiveConnection = rstEmployees.ActiveConnection  
  
    ' Loop through the recordset displaying the contents  
    ' of the FirstName field, the field's defined size,  
    ' and its actual size.  
    ' Also store FirstName values in aryFirstName array.  
    rstEmployees.MoveFirst  
    Debug.Print " "  
    Debug.Print "Original Defined Size and Actual Size"  
    i = 0  
    Do Until rstEmployees.EOF  
        Debug.Print "Employee name: " & rstEmployees!FirstName & _  
            " " & rstEmployees!LastName  
        Debug.Print "    FirstName Defined size: " _  
            & rstEmployees!FirstName.DefinedSize  
        Debug.Print "    FirstName Actual size: " & _  
            rstEmployees!FirstName.ActualSize  
            If Not rstEmployees!FirstName = Null Then  
                aryFirstName(i) = rstEmployees!FirstName  
            End If  
        rstEmployees.MoveNext  
        i = i + 1  
    Loop  
    rstEmployees.Close  
  
    ' Redefine the DefinedSize of FirstName in the catalog  
    Set colFirstName = catNorthwind.Tables("Employees").Columns("FirstName")  
    colNewFirstName.Name = colFirstName.Name  
    colNewFirstName.Type = colFirstName.Type  
    colNewFirstName.DefinedSize = colFirstName.DefinedSize + 1  
  
    ' Append new FirstName column to catalog  
    catNorthwind.Tables("Employees").Columns.Delete colFirstName.Name  
    catNorthwind.Tables("Employees").Columns.Append colNewFirstName  
  
    ' Open Employee table in Recordset for updating  
    rstEmployees.Open "Employees", catNorthwind.ActiveConnection, _  
        adOpenKeyset, adLockOptimistic, adCmdTable  
  
    ' Loop through the recordset displaying the contents  
    ' of the FirstName field, the field's defined size,  
    ' and its actual size.  
    ' Also restore FirstName values from aryFirstName.  
    rstEmployees.MoveFirst  
    Debug.Print " "  
    Debug.Print "New Defined Size and Actual Size"  
    i = 0  
    Do Until rstEmployees.EOF  
        rstEmployees!FirstName = aryFirstName(i)  
        Debug.Print "Employee name: " & rstEmployees!FirstName & _  
            " " & rstEmployees!LastName  
        Debug.Print "    FirstName Defined size: " _  
            & rstEmployees!FirstName.DefinedSize  
        Debug.Print "    FirstName Actual size: " & _  
            rstEmployees!FirstName.ActualSize  
        rstEmployees.MoveNext  
        i = i + 1  
    Loop  
    rstEmployees.Close  
  
    ' Restore original FirstName column to catalog  
    catNorthwind.Tables("Employees").Columns.Delete colNewFirstName.Name  
    catNorthwind.Tables("Employees").Columns.Append colFirstName  
  
    ' Restore original FirstName values to Employees table  
    rstEmployees.Open "Employees", catNorthwind.ActiveConnection, _  
        adOpenKeyset, adLockOptimistic, adCmdTable  
  
    rstEmployees.MoveFirst  
    i = 0  
    Do Until rstEmployees.EOF  
        rstEmployees!FirstName = aryFirstName(i)  
        rstEmployees.MoveNext  
        i = i + 1  
    Loop  
    rstEmployees.Close  
  
    'Clean up  
    Set catNorthwind = Nothing  
    Set colNewFirstName = Nothing  
    Set colFirstName = Nothing  
    Set rstEmployees = Nothing  
    Exit Sub  
  
DefinedSizeXError:  
    Set catNorthwind = Nothing  
    Set colNewFirstName = Nothing  
    Set colFirstName = Nothing  
  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndDefinedSizeVB  
```  
  
## <a name="see-also"></a>参照  
 [Column オブジェクト (ADOX)](./column-object-adox.md)   
 [DefinedSize プロパティ (ADOX)](./definedsize-property-adox.md)