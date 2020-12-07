---
description: ストリームと永続性
title: ストリームと永続化 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
author: rothja
ms.author: jroth
ms.openlocfilehash: 60e006733fd8ef5bd958328420ab43c1cbabc50e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979423"
---
# <a name="streams-and-persistence"></a>ストリームと永続性
[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトの[Save](../../../ado/reference/ado-api/save-method.md)メソッド*では、***レコードセット**がファイルに保存されるか、保存されます。 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッドでは、そのファイルから**レコードセット**が復元されます。  
  
 ADO 2.7 以降では、 **Save** メソッドと **Open** メソッドを使用して、 **レコードセット** を [Stream](../../../ado/reference/ado-api/stream-object-ado.md) オブジェクトにも永続化できます。 この機能は、リモートデータサービス (RDS) および Active Server ページ (ASP) を使用する場合に特に便利です。  
  
 ASP ページで永続化を単独で使用する方法の詳細については、現在の ASP ドキュメントを参照してください。  
  
 **ストリーム**オブジェクトと永続化を使用する方法を示すいくつかのシナリオを次に示します。  
  
## <a name="scenario-1"></a>シナリオ 1  
 このシナリオでは、単に **レコードセット** をファイルに保存し、次に **ストリーム**に保存します。 次に、永続化されたストリームを別の **レコードセット**に開きます。  
  
```  
Dim rs1 As ADODB.Recordset  
Dim rs2 As ADODB.Recordset  
Dim stm As ADODB.Stream  
  
Set rs1 = New ADODB.Recordset  
Set rs2 = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
rs1.Open   "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;""", adopenStatic, adLockReadOnly, adCmdText  
rs1.Save "c:\myfolder\mysubfolder\myrs.xml", adPersistXML  
rs1.Save stm, adPersistXML  
rs2.Open stm  
```  
  
## <a name="scenario-2"></a>シナリオ 2  
 このシナリオでは、 **レコードセット** は XML 形式の **ストリーム** に保持されます。 次に、 **ストリーム** を、確認、操作、または表示できる文字列に読み取ります。  
  
```  
Dim rs As ADODB.Recordset  
Dim stm As ADODB.Stream  
Dim strRst As String  
  
Set rs = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
' Open, save, and close the recordset.   
rs.Open "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
rs.Save stm, adPersistXML  
rs.Close  
Set rs = nothing  
  
' Put saved Recordset into a string variable.  
strRst = stm.ReadText(adReadAll)  
  
' Examine, manipulate, or display the XML data.  
...  
```  
  
## <a name="scenario-3"></a>シナリオ 3  
 次のコード例では、ASP コードを使用して、 **レコードセット** を XML として **応答** オブジェクトに直接永続化します。  
  
```  
...  
<%  
response.ContentType = "text/xml"  
  
' Create and open a Recordset.  
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select * from Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
  
' Save Recordset directly into output stream.  
rs.Save Response, adPersistXML   
  
' Close Recordset.  
rs.Close  
Set rs = nothing  
%>  
...  
```  
  
## <a name="scenario-4"></a>シナリオ 4  
 このシナリオでは、ASP コードによって、 **レコードセット** の内容が ADTG 形式でクライアントに書き込まれます。 [OLE DB 用の Microsoft Cursor Service](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)では、このデータを使用して、切断された**レコードセット**を作成できます。  
  
 RDS [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)の新しいプロパティである [URL](../../../ado/reference/rds-api/url-property-rds.md)は、 **レコードセット**を生成する .asp ページを指します。 これは、サーバー側の[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)オブジェクトを使用して、またはビジネスオブジェクトを記述するユーザーを使用しないで、**レコードセット**オブジェクトを取得できることを意味します。 これにより、RDS プログラミングモデルが大幅に簡略化されます。  
  
 サーバー側コード、という名前 https://server/directory/recordset.asp:  
  
```  
<%  
Dim rs   
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select au_fname, au_lname, phone from Authors", ""& _  
        "Provider=sqloledb;Data Source=MyServer;" & _  
        "Initial Catalog=Pubs;Integrated Security=SSPI;"  
response.ContentType = "multipart/mixed"  
rs.Save response, adPersistADTG  
%>  
```  
  
 クライアント側のコード:  
  
```  
<HTML>  
<HEAD>  
<TITLE>RDS Query Page</TITLE>  
</HEAD>  
<body>  
<CENTER>  
<H1>Remote Data Service 2.5</H1>  
<TABLE DATASRC="#DC1">  
   <TR>   
      <TD><SPAN DATAFLD="au_fname"></SPAN></TD>  
      <TD><SPAN DATAFLD="au_lname"></SPAN></TD>  
      <TD><SPAN DATAFLD="phone"></SPAN></TD>  
   </TR>  
</TABLE>  
<BR>  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
    ID=DC1 HEIGHT=1 WIDTH = 1>  
    <PARAM NAME="URL" VALUE="https://server/directory/recordset.asp">  
</OBJECT>  
  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 また、開発者はクライアントで **レコードセット** オブジェクトを使用することもできます。  
  
```  
...  
function GetRs()   
    {  
    rs = CreateObject("ADODB.Recordset");  
    rs.Open "https://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>参照  
 [Open メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Record オブジェクト (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Save メソッド](../../../ado/reference/ado-api/save-method.md)
