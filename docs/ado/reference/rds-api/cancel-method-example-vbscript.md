---
description: Cancel メソッドの例 (VBScript)
title: Cancel メソッドの例 (VBScript) |Microsoft Docs
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
- Cancel method [ADO], VBScript example
ms.assetid: 4ade106d-063d-486e-bc4d-a1a6b6e0bea9
author: rothja
ms.author: jroth
ms.openlocfilehash: b7ffdb6c63baf87834258722c869148cba33579b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100053343"
---
# <a name="cancel-method-example-vbscript"></a>Cancel メソッドの例 (VBScript)
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 次の例は、実行時に [Cancel](../ado-api/cancel-method-ado.md) メソッドを読み取る方法を示しています。 次のコードを切り取ってメモ帳または別のテキストエディターに貼り付け、CancelVBS. asp として保存します。 結果は任意のクライアントブラウザーで表示できます。  
  
```  
<!-- BeginCancelVBS -->  
<Script Language="VBScript">  
<!--  
Sub cmdCancelAsync_OnClick  
   ' Terminates currently running AsyncExecute,  
   ' ReadyState property set to adcReadyStateLoaded,  
   ' Recordset set to Nothing  
  ADC.Cancel  
End Sub  
  
Sub cmdRefreshTable_OnClick  
   ADC.Refresh  
End Sub  
-->  
</Script>  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="ADC">  
.  
   <PARAM NAME="SQL" VALUE="Select FirstName, LastName from Employees">  
   <PARAM NAME="CONNECT" VALUE="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'">  
   <PARAM NAME="Server" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
.  
</OBJECT>  
  
<TABLE DATASRC=#ADC>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
  
<FORM>  
<INPUT type="button" value="Refresh" id=cmdRefreshTable name=cmdRefreshTable>  
<INPUT type="button" value="Cancel" id=cmdCancelAsync name=cmdCancelAsync>  
</FORM>  
<!-- EndCancelVBS -->  
```  
  
## <a name="see-also"></a>参照  
 [Cancel メソッド (ADO)](../ado-api/cancel-method-ado.md)