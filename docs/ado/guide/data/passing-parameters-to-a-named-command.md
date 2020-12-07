---
description: 名前付きコマンドにパラメーターを渡す
title: 名前付きコマンドへのパラメーターの引き渡し |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- named commands [ADO]
- commands [ADO], passing parameters to a named command
ms.assetid: 36e0cdbe-7f50-40f5-af0d-700f5d8dc75a
author: rothja
ms.author: jroth
ms.openlocfilehash: 6de01bb420a7e2c5fadd2970064d5e84d22328b3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980143"
---
# <a name="passing-parameters-to-a-named-command"></a>名前付きコマンドにパラメーターを渡す
コマンドの結果が名前付きコマンドの *out* 変数として渡されるのと同じように、パラメーター化されたコマンドのパラメーターを *、変数と* して名前付きコマンドに渡すことができます。  
  
 次のコード例では、 **CustomerID** が Northwind データベースの "ALKFI" である顧客によって配置されたすべての注文を取得しようとしています。 **CustomerID**の値は、名前付きコマンドが呼び出された時点で指定されます。  
  
```  
Const DS = "MySqlServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
CommandText = "SELECT OrderID, OrderDate, " & _  
                     "RequiredDate, ShippedDate " & _  
                     "FROM Orders " & _  
                     "WHERE CustomerID = ? " & _  
                     "ORDER BY OrderID"  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a named command.  
objComm.CommandText = CommandText  
objComm.CommandType = adCmdText  
objComm.Name = "GetOrdersOf"  
Set objComm.ActiveConnection = objConn  
  
' Call the named command, passing a CustomerID value  
' as the input parameter.   
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
objConn.GetOrdersOf "ALKFI", objRs  
  
' Display the result.  
Debug.Print "All orders by ALFKI:"  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
Loop  
  
' Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
Set objComm = Nothing  
```  
  
 すべての入力パラメーターが出力変数の前にある必要があり、パラメーターのデータ型が一致しているか、対応するフィールドのデータ型に変換できることに注意してください。 次のステートメント  
  
```  
objConn.GetOrdersOf 12345, objRs  
```  
  
 -必要な入力パラメーターが**整数**型ではなく**文字列**型であるため、データ型が一致しないというエラーが発生します。  
  
 次の呼び出し:  
  
```  
objConn.GetOrdersOf "12345", objRs  
```  
  
 -は有効ですが、データベース内にそのようなレコードが存在しないため、空の結果セットが生成されます。  
  
## <a name="see-also"></a>参照  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
