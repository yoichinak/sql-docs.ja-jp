---
description: Command オブジェクトのパラメーター
title: Command オブジェクトのパラメーター |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], parameters
ms.assetid: 10e7ef4a-78bf-4e91-931e-cbc6c065dd4c
author: rothja
ms.author: jroth
ms.openlocfilehash: 2adb1e8d6dc516de2077416ce7e866efa6a03c54
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991553"
---
# <a name="command-object-parameters"></a>Command オブジェクトのパラメーター
前のトピックでは、 [単純なコマンドの作成と実行に](./creating-and-executing-a-simple-command.md)ついて説明しました。 [コマンド](../../reference/ado-api/command-object-ado.md)オブジェクトのより興味深い使用方法を次の例に示します。この例では、SQL コマンドがパラメーター化されています。 この変更により、コマンドを再利用し、毎回パラメーターに別の値を渡すことができます。 **Command**オブジェクトの[準備済みプロパティ](../../reference/ado-api/prepared-property-ado.md)プロパティが**true**に設定されているため、ADO では、最初に実行する前に、 [CommandText](../../reference/ado-api/commandtext-property-ado.md)で指定されたコマンドをコンパイルする必要があります。 また、コンパイルされたコマンドをメモリ内に保持します。 これにより、準備に必要なオーバーヘッドによってコマンドの初回実行時の処理が少し遅くなりますが、その後、コマンドが呼び出されるたびにパフォーマンスが向上します。 したがって、コマンドは、複数回使用する場合にのみ準備する必要があります。  
  
```  
'BeginManualParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set the CommandText as a parameterized SQL query.  
    objCmd.CommandText = "SELECT OrderID, OrderDate, " & _  
                         "RequiredDate, ShippedDate " & _  
                         "FROM Orders " & _  
                         "WHERE CustomerID = ? " & _  
                         "ORDER BY OrderID"  
    objCmd.CommandType = adCmdText  
  
    ' Prepare command because we will be executing it more than once.  
    objCmd.Prepared = True  
  
    ' Create new parameter for CustomerID. Initial value is ALFKI.  
    Set objParm1 = objCmd.CreateParameter("CustId", adChar, _  
                    adParamInput, 5, "ALFKI")  
    objCmd.Parameters.Append objParm1  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Execute once and display.  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' .Set new param value, re-execute command, and display.  
    objCmd("CustId") = "CACTU"  
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
'EndManualParamCmd  
  
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
  
 すべてのプロバイダーが準備コマンドをサポートしているわけではありません。 プロバイダーがコマンドの準備をサポートしていない場合、このプロパティが **True**に設定されるとすぐにエラーが返されることがあります。 エラーが返されない場合は、コマンドを準備する要求を無視し、 **準備** されたプロパティを **false**に設定します。