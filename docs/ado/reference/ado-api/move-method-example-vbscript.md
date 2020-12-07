---
description: Move メソッドの例 (VBScript)
title: Move メソッドの例 (VBScript) |Microsoft Docs
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
- Move method, VBScript example
ms.assetid: 29ec4b95-8986-4970-943f-3da3ecb207a2
author: rothja
ms.author: jroth
ms.openlocfilehash: 6a05f873e14f1d722d357288f07d19931139f8bb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990573"
---
# <a name="move-method-example-vbscript"></a>Move メソッドの例 (VBScript)
この例では、 [Move](./move-method-ado.md) メソッドを使用して、ユーザー入力に基づいてレコードポインターを配置します。  
  
 Active Server ページ (ASP) で次の例を使用します。 この完全に機能する例を表示するには、C:\Program た advworks-srv01 Platform SDK\Samples\DataAccess\Rds\RDSTest\advworks.mdb にあるデータソース (SDK と共にインストールされます) があるか、このファイルの実際の場所を反映するようにコード例のパスを編集する必要があります。 これは、Microsoft Access データベースファイルです。  
  
 [ **検索** ] を使用して Adovbs ファイルを検索し、使用する予定のディレクトリに配置します。 次のコードを切り取ってメモ帳または別のテキストエディターに貼り付け、 **Movevbs**として保存します。 結果は任意のブラウザーで表示できます。  
  
 エラー処理作業を確認するには、文字または整数を入力してください。  
  
```  
<!-- BeginMoveVBS -->  
<%@ Language=VBScript %>  
<%' use this meta tag instead of adovbs.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<HTML>  
<HEAD>  
<TITLE>ADO Move Methods</TITLE>  
<STYLE>  
<!--  
BODY {  
   font-family: "MS SANS SERIF",sans-serif;  
    }  
.thead1 {  
   background-color: #008080;   
   font-family: 'Arial Narrow','Arial',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Arial Narrow','Arial',sans-serif;   
   font-size: x-small;  
    }  
-->  
</STYLE>  
</HEAD>  
<BODY>   
<H3>ADO Move Methods</H3>  
<% ' to integrate/test this code replace the   
   ' Data Source value in the Connection string%>  
<%   
    ' connection and recordset variables  
    Dim Cnxn, strCnxn  
    Dim rsCustomers, strSQLCustomers  
  
    ' open connection  
    Set Cnxn = Server.CreateObject("ADODB.Connection")  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
  
    Cnxn.Open strCnxn  
  
     ' create and open Recordset using object refs  
    Set rsCustomers = Server.CreateObject("ADODB.Recordset")  
    strSQLCustomers = "Customers"  
  
    rsCustomers.ActiveConnection = Cnxn  
    rsCustomers.CursorLocation = adUseClient  
    rsCustomers.CursorType = adOpenKeyset  
    rsCustomers.LockType = adLockOptimistic  
    rsCustomers.Source = strSQLCustomers  
    rsCustomers.Open  
  
    'Check number of user moves this session and increment by entry  
    Session("Clicks") = Session("Clicks") + Request.Form("MoveAmount")  
    Clicks = Session("Clicks")  
    ' Move to last known recordset position plus amount passed   
    rsCustomers.Move CInt(Clicks)  
  
    'Error Handling  
    If rsCustomers.EOF Then  
        Session("Clicks") = rsCustomers.RecordCount  
        Response.Write "This is the Last Record"  
        rsCustomers.MoveLast  
    ElseIf rsCustomers.BOF Then  
        Session("Clicks") = 1  
        rsCustomers.MoveFirst  
        Response.Write "This is the First Record"  
    End If  
    %>  
  
    <H3>Current Record Number is <BR>  
    <%   
    If Session("Clicks") = 0 Then Session("Clicks") = 1  
    Response.Write(Session("Clicks") )%> of <%=rsCustomers.RecordCount%></H3>  
    <HR>  
  
    <TABLE COLSPAN=8 CELLPADDING=5 BORDER=0>  
  
    <!-- BEGIN column header row for Customer Table-->  
  
    <TR CLASS=thead1>  
       <TD>Company Name</TD>  
       <TD>Contact Name</TD>  
       <TD>City</TD>  
    </TR>  
        <% 'display%>  
        <TR CLASS=tbody>  
          <TD> <%= rsCustomers("CompanyName")%> </TD>  
          <TD> <%= rsCustomers("ContactName")%></TD>  
          <TD> <%= rsCustomers("City")%> </TD>  
        </TR>   
    </TABLE>  
  
    <HR>  
    <Input Type=Button Name=cmdDown  Value="<  ">  
    <Input Type=Button Name=cmdUp Value=" >">  
    <H5>Click Direction Arrows for Previous or Next Record  
    <BR> <BR>  
  
    <FORM Method = Post Action="MoveVbs.asp" Name=Form>  
    <TABLE>  
        <TR>  
           <TD><Input Type="Button" Name=Move Value="Move Amount "></TD>  
           <TD></TD>  
           <TD><Input Type="Text" Size="4" Name="MoveAmount" Value=0></TD>  
        <TR>  
    </TABLE>  
    Click Move Amount to use Move Method<br>  
    Enter Number of Records to Move + or - </H5>    </FORM>  
</BODY>  
  
<Script Language = "VBScript">  
  
Sub Move_OnClick  
   ' Make sure move value entered is an integer  
   If IsNumeric(Document.Form.MoveAmount.Value)Then  
      Document.Form.MoveAmount.Value = CInt(Document.Form.MoveAmount.Value)  
      Document.Form.Submit  
   Else  
      MsgBox "You Must Enter a Number", ,"ADO-ASP Example"  
      Document.Form.MoveAmount.Value = 0  
   End If  
End Sub  
  
Sub cmdDown_OnClick  
   Document.Form.MoveAmount.Value = -1  
   Document.Form.Submit  
End Sub  
  
Sub cmdUp_OnClick  
   Document.Form.MoveAmount.Value = 1  
   Document.Form.Submit  
End Sub  
</Script>  
  
<%  
    ' clean up  
    If rsCustomers.State = adStateOpen then  
        rsCustomers.Close  
    End If  
    If Cnxn.State = adStateOpen then  
        Cnxn.Close  
    End If  
%>  
</HTML>  
<!-- EndMoveVBS -->  
```  
  
## <a name="see-also"></a>参照  
 [Move メソッド (ADO)](./move-method-ado.md)   
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)