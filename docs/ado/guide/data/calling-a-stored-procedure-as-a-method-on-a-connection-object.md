---
description: Connection オブジェクトに対するメソッドとしてストアド プロシージャを呼び出す
title: 接続オブジェクトのメソッドとしてストアドプロシージャを呼び出す |Microsoft Docs
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
ms.assetid: 35ffdb79-a931-4271-a3bb-0cd804cf173e
author: rothja
ms.author: jroth
ms.openlocfilehash: 887730cdedd1dca884bca18bb6df449fdec2e1dc
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90989955"
---
# <a name="calling-a-stored-procedure-as-a-method-on-a-connection-object"></a>Connection オブジェクトに対するメソッドとしてストアド プロシージャを呼び出す
ストアドプロシージャは、関連付けられた開いている **接続** オブジェクトでネイティブメソッドであるかのように呼び出すことができます。 これは、 **接続** オブジェクトで名前付きコマンドを呼び出す場合と似ています。  
  
 次の Visual Basic コード例では、CustOrdersOrders Northwind サンプルデータベースのストアドプロシージャを呼び出します。このデータベースは、便宜上、ここに記載されています。  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 次のコード例では、ストアドプロシージャが、関連付けられた開いている **接続** オブジェクトでネイティブメソッドであるかのように呼び出す方法を示します。  
  
```  
Const DS = "MySQLServer"  
Const DB = "Northwind"  
Const DP = "SQLOLEDB"  
  
Dim objConn As New ADODB.Connection  
Dim objRs As New ADODB.Recordset  
Dim objComm As New ADODB.Command  
  
ConnectionString = "Provider=" & DP & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;"  
  
' Connect to the data source.  
objConn.Open ConnectionString  
  
' Set a stored procedure  
  
Set objComm.ActiveConnection = objConn  
  
' Execute the stored procedure on  
' the active connection object...  
'    "ALFKI" is the required input parameter,  
'    objRs is the resultant output variable.  
objComm(1) = "ALFKI"
Set objRs = objComm.Execute

' Display the result.  
Debug.Print "Results returned from sp_CustOrdersOrders for ALFKI: "  
Do While Not objRs.EOF  
    Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                objRs(2) & vbTab & objRs(3)  
    objRs.MoveNext  
 Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
Set objComm = Nothing  
```  
  
## <a name="see-also"></a>参照  
 [Connection オブジェクト (ADO)](../../reference/ado-api/connection-object-ado.md)
