---
description: MoveFirst、MoveLast、MoveNext、および MovePrevious メソッドの例 (VBScript)
title: レコードセットのレコードポインターの移動の例 (VBScript) |Microsoft Docs
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
- MoveLast method [ADO], VBScript example
- MoveNext method [ADO], VBScript example
- MovePrevious method [ADO], VBScript example
- MoveFirst method [ADO], VBScript example
ms.assetid: 911aa1dd-2786-4f34-992c-bb2fbdabcbdf
author: rothja
ms.author: jroth
ms.openlocfilehash: 7d6d1fdb55ca18fcbb06fb3cbb9e32f603af4d26
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990533"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript"></a>MoveFirst、MoveLast、MoveNext、および MovePrevious メソッドの例 (VBScript)
この例では、 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveLast](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveNext](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、および [MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md) メソッドを使用して、指定されたコマンドに基づいてレコード [セット](./recordset-object-ado.md) のレコードポインターを移動します。  
  
 次のコードを切り取ってメモ帳などのテキストエディターに貼り付け、 **Movefirstvbs. asp**として保存します。 結果は任意のブラウザーで表示できます。  
  
```  
<!-- BeginMoveFirstVBS -->  
<%@ Language=VBScript %>  
<%' use this meta tag instead of adovbs.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<HTML>  
<HEAD>  
<TITLE>ADO MoveNext, MovePrevious, MoveLast, MoveFirst Methods</TITLE>  
  
<SCRIPT LANGUAGE="VBScript">  
<!--  
   Sub cmdDown_OnClick  
      'Set Values in Form Input Boxes and Submit Form  
      Document.form.MoveAction.Value = "MovePrev"  
      Document.Form.Submit  
   End Sub  
  
   Sub cmdUp_OnClick  
      Document.form.MoveAction.Value = "MoveNext"  
      Document.Form.Submit  
   End Sub  
  
   Sub cmdFirst_OnClick  
      Document.form.MoveAction.Value = "MoveFirst"  
      Document.Form.Submit  
   End Sub  
  
   Sub cmdLast_OnClick  
      Document.form.MoveAction.Value = "MoveLast"  
      Document.Form.Submit  
   End Sub  
//-->  
</SCRIPT>  
</HEAD>  
  
<body bgcolor="white">   
<h1 align="center">ADO MoveNext, MovePrevious <br> MoveLast & MoveFirst Methods</h1>  
<% ' to integrate/test this code replace the   
   ' Data Source value in the Connection string%>  
<%   
   ' connection and recordset variables  
   Dim Cnxn, strCnxn  
   Dim rsEmployees, strSQLEmployees  
  
   ' open connection  
    Set Cnxn = Server.CreateObject("ADODB.Connection")  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    Cnxn.Open strCnxn  
  
    ' create and open Recordset using object refs  
   Set rsEmployees = Server.CreateObject("ADODB.Recordset")  
   strSQLEmployees = "Employees"  
  
   rsEmployees.ActiveConnection = Cnxn  
   rsEmployees.CursorLocation = adUseClient  
   rsEmployees.CursorType = adOpenKeyset  
   rsEmployees.LockType = adLockOptimistic  
   rsEmployees.Source = strSQLEmployees  
   rsEmployees.Open  
  
   rsEmployees.MoveFirst  
  
   If Not IsEmpty(Request.Form("MoveAction")) Then  
      strAction = Request.Form("MoveAction")  
      varPosition  = Request.Form("Position")  
  
      rsEmployees.AbsolutePosition = varPosition  
  
      Select Case strAction  
  
        Case "MoveNext"  
  
         rsEmployees.MoveNext  
         If rsEmployees.EOF Then  
            rsEmployees.MoveLast  
            strMessage = "Can't move beyond the last record."  
         End If  
  
        Case "MovePrev"  
  
         rsEmployees.MovePrevious  
         If rsEmployees.BOF Then  
            rsEmployees.MoveFirst  
            strMessage = "Can't move beyond the first record."  
         End If  
  
        Case "MoveLast"  
  
         rsEmployees.MoveLast  
  
        Case "MoveFirst"  
  
         rsEmployees.MoveFirst  
  
      End Select  
   End If  
  
%>  
  
<!-- Display Current Record Number and Recordset Size -->  
<h2>Record Number <%=rsEmployees.AbsolutePosition%> of <%=rsEmployees.RecordCount%></H2>  
<hr>  
<table cellpadding=5 border=0>  
<!-- BEGIN column header row for Customer Table-->  
<tr>  
   <th>Name</th>  
   <th>Hire Date</th>  
</tr>  
  
<!--Display ADO Data from Customer Table-->  
<tr>  
  <td><%= rsEmployees("LastName") & ", " %>   
      <%= rsEmployees("FirstName") & " " %></td>  
  <td><%= rsEmployees("HireDate")%></td>  
</tr>   
<tr>  
  <td colspan=2><%=strMessage%></td>  
</tr>  
</table>  
  
<hr>  
  
<form Name="Form" Method="Post" Action="MoveFirstVbs.asp">  
<Input Type=Button Name=cmdDown Value="<">  
<Input Type=Button Name=cmdUp Value=">">  
<BR>  
<H3>Click Direction Arrows to Use MovePrevious or MoveNext</H3>  
<Input Type=Button Name=cmdFirst Value="First Record">  
<Input Type=Button Name=cmdLast Value="Last Record">  
  
<!-- Use Hidden Form Fields to record values to send to Server -->  
  
<input Type="Hidden" Size="4" Name="MoveAction" Value="Move">  
<input Type="Hidden" Size="4" Name="Position" Value="<%= rsEmployees.AbsolutePosition%>">  
</form>  
  
<HR>  
</BODY>  
  
<%  
    ' clean up  
    If rsEmployees.State = adStateOpen then  
        rsEmployees.Close  
    End If  
    If Cnxn.State = adStateOpen then  
        Cnxn.Close  
    End If  
%>  
</HTML>  
<!-- EndMoveFirstVBS -->  
```  
  
## <a name="see-also"></a>参照  
 [MoveFirst、MoveLast、MoveNext、および MovePrevious メソッド (ADO)](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)