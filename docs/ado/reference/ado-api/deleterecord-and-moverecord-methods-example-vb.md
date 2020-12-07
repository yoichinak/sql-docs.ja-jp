---
description: DeleteRecord メソッドと MoveRecord メソッドの例 (VB)
title: DeleteRecord メソッドと MoveRecord メソッドの例 (VB) |Microsoft Docs
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
- MoveRecord method [ADO], Visual Basic example
- DeleteRecord method [ADO], Visual Basic example
ms.assetid: c3937d1e-9872-47e5-a22e-b147637f2388
author: rothja
ms.author: jroth
ms.openlocfilehash: 382a4e103d1a51067344788b7fe1fdca9f5e1fd4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974013"
---
# <a name="deleterecord-and-moverecord-methods-example-vb"></a>DeleteRecord メソッドと MoveRecord メソッドの例 (VB)
この例では、Web フォルダーに発行されたテキストファイルの内容をコピー、移動、編集、および削除する方法を示します。 使用されるその他のプロパティとメソッドには、 [Getchildren](../../../ado/reference/ado-api/getchildren-method-ado.md)、 [parenturl](../../../ado/reference/ado-api/parenturl-property-ado.md)、 [Source](../../../ado/reference/ado-api/source-property-ado-record.md)、および [Flush](../../../ado/reference/ado-api/flush-method-ado.md)があります。  
  
```  
'BeginDeleteRecordVB  
  
'Note:  
' IIS must be running for this sample to work. To  
' use this sample you must:  
'  
' 1. create folders named "test" and "test2"  
'    in the root web folder of https://MyServer  
'  
' 2. Create a text file named "test2.txt" in the  
'    "test" folder.  
' 3. Replace "MyServer" with the appropriate web  
'    server name.  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' connection and recordset variables  
    Dim rsDestFolder As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
  
     ' file as record variables  
    Dim rcFile As ADODB.Record  
    Dim rcDestFile As ADODB.Record  
    Dim rcDestFolder As ADODB.Record  
    Dim objStream As Stream  
  
     ' file variables  
    Dim strFile As String  
    Dim strDestFile As String  
    Dim strDestFolder As String  
  
     ' instantiate variables  
    Set rsDestFolder = New ADODB.Recordset  
    Set rcDestFolder = New ADODB.Record  
    Set rcFile = New ADODB.Record  
    Set rcDestFile = New ADODB.Record  
    Set objStream = New ADODB.Stream  
  
     ' open a record on a text file  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "url=https://MyServer/"  
    Cnxn.Open strCnxn  
    strFile = "test/test2.txt"  
    rcFile.Open strFile, Cnxn, adModeReadWrite, adOpenIfExists Or adCreateNonCollection  
    Debug.Print Cnxn  
  
     ' edit the contents of the text file  
    objStream.Open rcFile, , adOpenStreamFromRecord  
  
    Debug.Print "Source: " & strCnxn & rcFile.Source  
    Debug.Print "Original text: " & objStream.ReadText  
  
    objStream.Position = 0  
    objStream.WriteText "Newer Text. "  
    objStream.Position = 0  
  
    Debug.Print "New text: " & objStream.ReadText  
  
     ' reset the stream object  
    objStream.Flush  
    objStream.Close  
    rcFile.Close  
  
     ' reopen record to see new contents of text file  
    rcFile.Open strFile, Cnxn, adModeReadWrite, adOpenIfExists Or adCreateNonCollection  
    objStream.Open rcFile, adModeReadWrite, adOpenStreamFromRecord  
  
    Debug.Print "Source: " & strCnxn & rcFile.Source  
    Debug.Print "Edited text: " & objStream.ReadText  
  
     ' copy the file to another folder  
    strDestFile = "test2/test1.txt"  
    rcFile.CopyRecord "", "https://MyServer/" & strDestFile, "", "", adCopyOverWrite  
  
     ' delete the original file  
    rcFile.DeleteRecord  
  
     ' move the file from the subfolder back to original location  
    strDestFolder = "test2/"  
    rcDestFolder.Open strDestFolder, Cnxn ', adOpenIfExists  'Or adCreateCollection  
    Set rsDestFolder = rcDestFolder.GetChildren  
    rsDestFolder.MoveFirst  
  
     ' position current record at on the correct file  
    Do While Not (rsDestFolder.EOF Or rsDestFolder(0) = "test1.txt")  
        rsDestFolder.MoveNext  
    Loop  
  
     ' open a record on the correct row of the recordset  
    rcDestFile.Open rsDestFolder, Cnxn  
  
     ' do the move  
    rcDestFile.MoveRecord "", "https://MyServer/" & strFile, "", "", adMoveOverWrite  
  
    ' clean up  
    rsDestFolder.Close  
    Cnxn.Close  
    Set rsDestFolder = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rsDestFolder Is Nothing Then  
        If rsDestFolder.State = adStateOpen Then rsDestFolder.Close  
    End If  
    Set rsDestFolder = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndDeleteRecordVB  
```  
  
## <a name="see-also"></a>参照  
 [DeleteRecord メソッド (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)   
 [Flush メソッド (ADO)](../../../ado/reference/ado-api/flush-method-ado.md)   
 [GetChildren メソッド (ADO)](../../../ado/reference/ado-api/getchildren-method-ado.md)   
 [MoveRecord メソッド (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)   
 [ParentURL プロパティ (ADO)](../../../ado/reference/ado-api/parenturl-property-ado.md)   
 [Source プロパティ (ADO Record)](../../../ado/reference/ado-api/source-property-ado-record.md)
