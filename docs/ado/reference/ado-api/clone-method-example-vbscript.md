---
description: Clone メソッドの例 (VBScript)
title: Clone メソッドの例 (VBScript) |Microsoft Docs
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
- Clone method [ADO], VBScript example
ms.assetid: 36b96e3d-8cb0-4b79-bd93-ea5e0eb5679f
author: rothja
ms.author: jroth
ms.openlocfilehash: af5f0a49c2bf126dbba4f0c40d88e15f0d71a187
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975403"
---
# <a name="clone-method-example-vbscript"></a>Clone メソッドの例 (VBScript)
この例では、 [Clone](./clone-method-ado.md) メソッドを使用して [レコードセット](./recordset-object-ado.md) のコピーを作成し、ユーザーが各コピーのレコードポインターを個別に配置できるようにします。  
  
 Active Server ページ (ASP) で次の例を使用します。 この例では、Microsoft Access と共に配布される **Northwind** データベースを使用します。 次のコードを切り取ってメモ帳などのテキストエディターに貼り付け、CloneVBS として保存します。 結果は任意のクライアントブラウザーで表示できます。  
  
 この例を実行するには、行をに変更して、 `RsCustomerList.Source = "Customers"` `RsCustomerList.Source = "Products"` より大きなテーブルをカウントします。  
  
```  
<!-- BeginCloneVBS -->  
<% Language = VBScript %>  
<%' use this meta tag instead of adovbs.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<HTML>  
<HEAD>  
<TITLE>ADO Clone Method</TITLE>  
</HEAD>  
  
<BODY>  
  
<H1 align="center">ADO Clone Method</H1>  
<HR>  
<% ' to integrate/test this code replace the   
   ' Data Source value in the Connection string%>  
<%   
    ' connection and recordset variables  
    Dim Cnxn, strCnxn  
    Dim rsCustomers, strSQLCustomers  
    Dim rsFirst, rsLast, rsCount  
    Dim rsClone  
    Dim CloneFirst, CloneLast, CloneCount  
  
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
  
    rsCustomers.MoveFirst  
    rsCount = rsCustomers.RecordCount  
    rsFirst = rsCustomers("CompanyName")  
    rsCustomers.MoveLast  
    rsLast = rsCustomers("CompanyName")  
  
    ' create clone  
    Set rsClone = rsCustomers.Clone  
    rsClone.MoveFirst  
    CloneCount = rsClone.RecordCount  
    CloneFirst = rsClone("CompanyName")  
    rsClone.MoveLast  
    CloneLast = rsClone("CompanyName")  
%>  
  
<!-- Display Results -->  
<H3>There Are <%=rsCount%> Records in the original recordset</H3>  
<H3>The first record is <%=rsFirst%> and the last record is <%=rsLast%></H3>  
<BR><HR>  
<H3>There Are <%=CloneCount%> Records in the original recordset</H3>  
<H3>The first record is <%=CloneFirst%> and the last record is <%=CloneLast%></H3>  
<BR><HR>  
<H4>Location of OLEDB Database</H4>  
  
<%  
    ' Show location of DSN data source  
    Response.Write(Cnxn)  
  
    ' Clean up  
    If rsCustomers.State = adStateOpen then  
       rsCustomers.Close  
    End If  
    If rsClone.State = adStateOpen then  
       rsClone.Close  
    End If  
    If Cnxn.State = adStateOpen then  
       Cnxn.Close  
    End If  
    Set rsCustomers = Nothing  
    Set rsClone = Nothing  
    Set Cnxn = Nothing  
%>  
</BODY>  
</HTML>  
<!-- EndCloneVBS -->  
```  
  
## <a name="see-also"></a>参照  
 [Clone メソッド (ADO)](./clone-method-ado.md)   
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)