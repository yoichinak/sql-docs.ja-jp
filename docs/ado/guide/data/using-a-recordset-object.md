---
description: レコードセット オブジェクトを使用する
title: レコードセットオブジェクトを使用する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
ms.assetid: 01c630d8-eb35-4bd0-a99f-7c0f85316cc1
author: rothja
ms.author: jroth
ms.openlocfilehash: 44fc7a242887419ba3013113632c8d1acd2a3337
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100032304"
---
# <a name="using-a-recordset-object"></a>レコードセット オブジェクトを使用する
または、 **レコードセット** を使用して、暗黙的に接続を確立し、1回の操作でその接続に対してコマンドを発行することもできます。 たとえば、Visual Basic の場合は次のようになります。  
  
```  
Dim oRs As ADODB.Recordset  
Dim sConn As String  
Dim sSQL as String  
  
sConn = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _             "Initial Catalog='Northwind';Integrated Security='SSPI';"  
  
sSQL = "SELECT ProductID, ProductName, CategoryID, UnitPrice " & _  
             "FROM Products"  
  
' Create and Open the Recordset object.  
Set oRs = New ADODB.Recordset  
oRs.CursorLocation = adUseClient  
oRs.Open sSQL, sConn, adOpenStatic, _  
               adLockBatchOptimistic, adCmdText  
  
MsgBox oRs.RecordCount  
  
oRs.MarshalOptions = adMarshalModifiedOnly  
' Disconnect the Recordset.  
Set oRs.ActiveConnection = Nothing  
oRs.Close          
Set oRs = Nothing  
```  
  
 **ActiveConnection** パラメーターの値として **接続** オブジェクト (*oconn*) の代わりに接続文字列 (*sconn*) が実行されることに注意してください **。** また、クライアント側のカーソルの種類は、**レコードセット** オブジェクトの **cursor location** プロパティを設定することによって適用されます。 ここでも、 **HelloData** の例と比較してください。
