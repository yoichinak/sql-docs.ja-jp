---
description: Type プロパティの例 (Field) (VB)
title: Type プロパティの例 (Field) (VB) |Microsoft Docs
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
- Type property [field] [ADO], Visual Basic example
ms.assetid: accb72f5-a3bd-4a7e-92b6-6da0783b4b75
author: rothja
ms.author: jroth
ms.openlocfilehash: b6dcd959172ade73a7c960e91997c5a1cb1e2dc5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988273"
---
# <a name="type-property-example-field-vb"></a>Type プロパティの例 (Field) (VB)
この例では、 ***Employees***テーブル内のすべての[Field](./field-object.md)オブジェクトの[type](./type-property-ado.md)プロパティの値に対応する定数の名前を表示することによって、 [type](./type-property-ado.md)プロパティを示します。 このプロシージャを実行するには、FieldType 関数が必要です。  
  
```  
'BeginTypeFieldVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstEmployees As ADODB.Recordset  
    Dim fld As ADODB.Field  
    Dim strCnxn As String  
    Dim strSQLEmployee As String  
    Dim FieldType As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Open recordset with data from Employees table  
    Set rstEmployees = New ADODB.Recordset  
    strSQLEmployee = "employee"  
    rstEmployees.Open strSQLEmployee, Cnxn, , , adCmdTable  
    'rstEmployees.Open strSQLEmployee, Cnxn, adOpenStatic, adLockReadOnly, adCmdTable  
     ' the above two lines of code are identical  
  
    Debug.Print "Fields in Employees Table:" & vbCr  
  
    ' Enumerate Fields collection of Employees table  
    For Each fld In rstEmployees.Fields  
        ' translate field-type code to text  
        Select Case fld.Type  
            Case adChar  
               FieldType = "adChar"  
            Case adVarChar  
               FieldType = "adVarChar"  
            Case adSmallInt  
               FieldType = "adSmallInt"  
            Case adUnsignedTinyInt  
               FieldType = "adUnsignedTinyInt"  
            Case adDBTimeStamp  
               FieldType = "adDBTimeStamp"  
        End Select  
        ' show results  
        Debug.Print "  Name: " & fld.Name & vbCr & _  
          "  Type: " & FieldType & vbCr  
    Next fld  
  
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
  
    Set fld = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndTypeFieldVB  
  
Attribute VB_Name = "TypeField"  
```  
  
## <a name="see-also"></a>参照  
 [Field オブジェクト](./field-object.md)   
 [Type プロパティ (ADO)](./type-property-ado.md)