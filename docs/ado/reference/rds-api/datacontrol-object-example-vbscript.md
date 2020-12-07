---
description: DataControl オブジェクトの例 (VBScript)
title: DataControl オブジェクトの例 (VBScript) |Microsoft Docs
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
- DataControl object [ADO], VBScript example
ms.assetid: 4f306a51-d5a4-4785-b426-487639cda164
author: rothja
ms.author: jroth
ms.openlocfilehash: dd908cf997a2bdc006067ea7d0422e33bd8cee91
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721133"
---
# <a name="datacontrol-object-example-vbscript"></a>DataControl オブジェクトの例 (VBScript)
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 次のコードは、RDS を設定する方法を示して [います。](./datacontrol-object-rds.md) デザイン時にパラメーターを DataControl し、データを認識するコントロールにバインドします。 このコードを \<Body> 通常の HTML ドキュメントのタグとタグの間で切り取って貼り付け、 \</Body> **DataControlDesignVBS**という名前を付けます。 ASP スクリプトによってサーバーが識別されます。  
  
```  
<!-- BeginDataControlDesignVBS -->  
<%@ Language=VBScript %>  
<HTML>  
<HEAD>  
<META name="VI60_DefaultClientScript"  content=VBScript>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<title>RDS DataControl</title>  
  
    <%' local style sheet used for display%>  
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
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Remote Data Service</H3>  
<TABLE DATASRC=#RDS>  
<TBODY>  
   <TR>  
      <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
      <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
   </TR>  
</TBODY>  
</TABLE>  
<!-- Remote Data Service with Parameters set at Design Time -->  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDS>  
   <PARAM NAME="SQL" VALUE="Select * from Employees for browse">  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'">  
</OBJECT>  
  
</BODY>  
</HTML>  
<!-- EndDataControlDesignVBS -->  
```  
  
 次の例は、RDS の必要なパラメーターを設定する方法を示して **います。** 実行時に DataControl。 この例をテストするには、 \<Body> \</Body> 通常の HTML ドキュメントのタグとタグの間でこのコードを**DataControlRuntimeVBS.asp**切り取って貼り付け、DataControlRuntimeVBS という名前を付けます。 ASP スクリプトによってサーバーが識別されます。  
  
```  
<!-- BeginDataControlRuntimeVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Data Control Object Example (VBScript)</title>  
  
    <%' local style sheet used for display%>  
<style>  
<!--  
body {  
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
</style>  
</head>  
  
<body>  
<h1>Data Control Object Example (VBScript)</h1>  
  
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Remote Data Service Run Time</H3>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="au_lname"></SPAN></TD>  
    <TD><SPAN DATAFLD="au_fname"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
<% ' RDS.DataControl with no parameters set at design time %>  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDS HEIGHT=1 WIDTH=1></OBJECT>  
  
<FORM name="frmInput">  
<HR>  
<Input Size="70" Name="txtServer" Value="https://<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
<Input Size="100" Name="txtConnect" Value="Provider='sqloledb';Data Source=<%=Request.ServerVariables("SERVER_NAME")%>;Initial Catalog='Pubs';Integrated Security='SSPI';">  
<BR>  
<Input Size="70" Name="txtSQL" Value="Select * from Authors">  
<HR>  
<INPUT TYPE="BUTTON" NAME="Run" VALUE="Run"><BR>  
<H4>Show grid with these values or change them to see data from another ODBC data source on your server</H4>  
</FORM>  
  
<Script Language="VBScript">  
  
' Set parameters of RDS.DataControl at Run Time  
Sub Run_OnClick  
  
   RDS.Server = document.frmInput.txtServer.Value  
   RDS.Connect = document.frmInput.txtConnect.Value  
   RDS.SQL = document.frmInput.txtSQL.Value  
  
   RDS.Refresh  
  
End Sub  
  
</Script>  
  
</body>  
</html>  
<!-- EndDataControlRuntimeVBS -->  
```  
  
## <a name="see-also"></a>参照  
 [DataControl オブジェクト (RDS)](./datacontrol-object-rds.md)