---
description: Execute、Requery、および Clear メソッドの例 (VBScript)
title: Execute、Requery、および Clear メソッドの例 (VBScript) |Microsoft Docs
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
- Execute method [ADO], VBScript example
- Clear method [ADO], VBScript example
- Requery method [ADO], VBScript example
ms.assetid: 3a7bbf07-2fca-4892-95f4-eec93f2d5e91
author: rothja
ms.author: jroth
ms.openlocfilehash: 3a584d2c0c0187425cc5796fa8c7a0070f358b31
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973414"
---
# <a name="execute-requery-and-clear-methods-example-vbscript"></a>Execute、Requery、および Clear メソッドの例 (VBScript)
この例では、[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトと[接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトの両方から実行する場合の**Execute**メソッドを示します。 また、 [Requery](../../../ado/reference/ado-api/requery-method.md) メソッドを使用して [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)内の現在のデータを取得し、 [clear](../../../ado/reference/ado-api/clear-method-ado.md) メソッドを使用して [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) コレクションの内容をクリアします。 この手順を実行するには、ExecuteCommand および PrintOutput プロシージャが必要です。  
  
 Active Server ページ (ASP) で次の例を使用します。 この完全に機能する例を表示するには、C:\Program Raplatform SDK\Samples\DataAccess\Rds\RDSTest\advworks.mdb にあるデータソースた advworks-srv01 (SDK サンプルと共にインストールされます) があるか、このファイルの実際の場所を反映するようにコード例のパスを編集する必要があります。 これは、Microsoft Access データベースファイルです。  
  
 [ **検索** ] を使用して Adovbs ファイルを検索し、使用する予定のディレクトリに配置します。 次のコードを切り取ってメモ帳などのテキストエディターに貼り付け、 **ExecuteVBS**として保存します。 結果は任意のクライアントブラウザーで表示できます。  
  
```  
<!-- BeginExecuteVBS -->  
<%@ Language=VBScript %>  
<% ' use this meta tag instead of ADOVBS.inc%>  
<!-- METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4"  -->  
<HTML>  
<HEAD>  
<META name="VI60_DefaultClientScript"  content=VBScript>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<title>ADO Execute Method</title>  
<STYLE>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</STYLE>  
</HEAD>  
  
<BODY>  
<H3>ADO Execute Method</H3>  
<HR>  
<H4>Recordset Retrieved Using Connection Object</H4>  
<!--- Recordsets retrieved using Execute method of Connection and Command Objects-->  
<%   
     ' connection, command and recordset variables  
    Dim Cnxn, strCnxn  
    Dim rsCustomers, strSQLCustomers  
    Dim Cmd   
    Dim rsProducts, strSQLProducts  
  
    ' create and open connection  
    Set Cnxn = Server.CreateObject("ADODB.Connection")   
    strCnxn="Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    Cnxn.Open  strCnxn  
    ' create and open recordset  
    Set rsCustomers = Server.CreateObject("ADODB.Recordset")  
    strSQLCustomers = "Customers"  
    rsCustomers.Open strSQLCustomers, Cnxn, adOpenKeyset, adLockOptimistic, adCmdTable  
  
    '1st Recordset using Connection - Execute  
    Set rsCustomers = Cnxn.Execute(strSQLCustomers)   
  
    Set Cmd = Server.CreateObject("ADODB.Command")  
    Cmd.ActiveConnection = Cnxn  
    strSQLProducts = "SELECT * From Products"  
    Cmd.CommandText = strSQLProducts  
  
    '2nd Recordset Cmd - execute   
    Set rsProducts = Cmd.Execute  
    %>  
    <TABLE COLSPAN=8 CELLPADDING=5 BORDER=0 ALIGN=CENTER>  
    <!-- BEGIN column header row for Customer Table-->  
    <TR CLASS=thead>  
      <TH>Company Name</TH>  
      <TH>Contact Name</TH>  
      <TH>City</TH>  
    </TR>  
  
    <!--Display ADO Data from Customer Table-->  
    <%   
    Do While Not rsCustomers.EOF %>  
      <TR CLASS=tbody>  
        <TD>   
        <%= rsCustomers("CompanyName")%>   
        </TD>  
        <TD>  
        <%= rsCustomers("ContactName") %>   
        </TD>  
        <TD>   
        <%= rsCustomers("City")%>   
        </TD>  
      </TR>   
      <%   
    rsCustomers.MoveNext   
    Loop   
    %>  
</TABLE>  
  
<HR>  
<H4>Recordset Retrieved Using Command Object</H4>  
  
<TABLE CELLPADDING=5 BORDER=0 ALIGN=CENTER WIDTH="80%">  
  
<!-- BEGIN column header row for Product List Table-->  
<TR CLASS=thead2>  
  <TH>Product Name</TH>  
  <TH>Unit Price</TH>  
</TR>  
  
<!-- Display ADO Data Product List-->  
<% Do Until rsProducts.EOF %>  
  <TR CLASS=tbody>  
    <TD>  
    <%= rsProducts("ProductName")%>    
    </TD>  
    <TD>   
    <%= rsProducts("UnitPrice")%>   
    </TD>  
<%   
    rsProducts.MoveNext   
    Loop  
  
    ' clean up  
    If rsCustomers.State = adStateOpen then  
        rsCustomers.Close  
    End If  
    If rsProducts.State = adStateOpen then  
        rsProducts.Close  
    End If  
    If Cnxn.State = adStateOpen then  
        Cnxn.Close  
    End If  
    Set Cmd = Nothing  
    Set rsCustomers = Nothing  
    Set rsProducts = Nothing  
    Set Cnxn = Nothing  
%>  
</TABLE>  
  
</BODY>  
</HTML>  
<!-- EndExecuteVBS -->  
```  
  
## <a name="see-also"></a>参照  
 [Clear メソッド (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Command オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Error オブジェクト](../../../ado/reference/ado-api/error-object.md)   
 [Errors コレクション (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Execute メソッド (ADO コマンド)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute メソッド (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Requery メソッド](../../../ado/reference/ado-api/requery-method.md)
