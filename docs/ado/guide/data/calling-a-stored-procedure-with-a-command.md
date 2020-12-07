---
description: Command を使用してストアド プロシージャを呼び出す
title: Command | を使用したストアドプロシージャの呼び出しMicrosoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
author: rothja
ms.author: jroth
ms.openlocfilehash: ac6f8388e3f07bf93e00f1d24aa3a782237ca0e5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991583"
---
# <a name="calling-a-stored-procedure-with-a-command"></a>Command を使用してストアド プロシージャを呼び出す
コマンドを使用してストアドプロシージャを呼び出すことができます。 このトピックの最後にあるコードサンプルでは、次のように定義された、Northwind のサンプルデータベースのストアドプロシージャを参照しています。 CustOrdersOrders 例を次に示します。  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 ストアドプロシージャを定義して呼び出す方法の詳細については、SQL Server のドキュメントを参照してください。  
  
 このストアドプロシージャは、 [コマンドオブジェクトパラメーター](./command-object-parameters.md)で使用されるコマンドに似ています。 顧客 ID パラメーターを受け取り、その顧客の注文に関する情報を返します。 次のコードサンプルでは、このストアドプロシージャを ADO **レコードセット**のソースとして使用します。  
  
 ストアドプロシージャを使用すると、ADO の別の機能である **Parameters** コレクション **更新** メソッドにアクセスできます。 このメソッドを使用すると、実行時にコマンドに必要なパラメーターに関するすべての情報が ADO によって自動的に入力されます。 ADO では、パラメーターに関する情報をデータソースに照会する必要があるため、この手法を使用するとパフォーマンスが低下します。  
  
 その他の重要な違いは、次のコードサンプルと [Command オブジェクトパラメーター](./command-object-parameters.md)のコードの間にあり、これらのパラメーターは手動で入力されています。 まず、このコードでは、 **準備** されたプロパティが SQL Server ストアドプロシージャであり、定義によってプリコンパイルされているため、このプロパティは **True** に設定されません。 次に、コマンドオブジェクトの**CommandType**プロパティを2番目の例で**adCmdStoredProc**に変更し **、コマンドが**ストアドプロシージャであったことを ADO に通知します。  
  
 最後に、2番目の例では、値を設定するときにパラメーターをインデックスで参照する必要があります。これは、デザイン時にパラメーターの名前がわからない場合があるためです。 パラメーターの名前がわかっている場合は、 **Command**オブジェクトの新しい[Namedparameters](../../reference/ado-api/namedparameters-property-ado.md)プロパティを True に設定し、プロパティの名前を参照することができます。 ストアドプロシージャに記述されている最初のパラメーターの位置 ( @CustomerID ) が 0 () ではなく1であることがわかり `objCmd(1) = "ALFKI"` ます。 これは、パラメーター0に SQL Server ストアドプロシージャからの戻り値が含まれているためです。  
  
```  
'BeginAutoParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set CommandText equal to the stored procedure name.  
    objCmd.CommandText = "CustOrdersOrders"  
    objCmd.CommandType = adCmdStoredProc  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Automatically fill in parameter info from stored procedure.  
    objCmd.Parameters.Refresh  
  
    ' Set the param value.  
    objCmd(1) = "ALFKI"  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' ...then set new param value, re-execute command, and display.  
    objCmd(1) = "CACTU"  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndAutoParamCmd  
  
'BeginNewConnection  
Private Function GetNewConnection() As ADODB.Connection  
    Dim oCn As New ADODB.Connection  
    Dim sCnStr As String  
  
    sCnStr = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    oCn.Open sCnStr  
  
    If oCn.State = adStateOpen Then  
        Set GetNewConnection = oCn  
    End If  
  
End Function  
'EndNewConnection  
```  
  
## <a name="see-also"></a>参照  
 [サポート技術情報の記事117500](https://go.microsoft.com/fwlink/?LinkId=117500)