---
description: '更新プログラムの送信: UpdateBatch メソッド'
title: '更新プログラムを送信しています: UpdateBatch メソッド |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
author: rothja
ms.author: jroth
ms.openlocfilehash: 88e441fd0ff58f63cf5ac701ec2620c29048b1e6
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100032494"
---
# <a name="sending-the-updates-updatebatch-method"></a>更新プログラムの送信: UpdateBatch メソッド
次のコードでは、LockType プロパティを adLockBatchOptimistic に設定し、カーソル位置を adUseClient に設定することによって、レコードセットをバッチモードで開きます。 2つの新しいレコードを追加し、既存のレコードのフィールドの値を変更して元の値を保存した後、UpdateBatch を呼び出して変更内容をデータソースに送り返します。  
  
## <a name="remarks"></a>解説  
  
```  
'BeginBatchUpdate  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT ShipperId, CompanyName, Phone FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
  
    ' Change value of Phone field for first record in Recordset, saving value  
    ' for later restoration.  
    intId = objRs1("ShipperId")  
    sPhone = objRs1("Phone")  
  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Add two new records  
    For i = 0 To 1  
        objRs1.AddNew  
        objRs1(1) = "New Shipper #" & CStr((i + 1))  
        objRs1(2) = "(nnn) 555-" & i & i & i & i  
    Next i  
  
    ' Send the updates  
    objRs1.UpdateBatch  
'EndBatchUpdate  
```  
  
 現在のレコードを編集している場合、または UpdateBatch メソッドを呼び出したときに新しいレコードを追加している場合、ADO は Update メソッドを自動的に呼び出して、保留中の変更を現在のレコードに保存してから、バッチされた変更をプロバイダーに送信します。  
  
## <a name="see-also"></a>参照  
 [バッチ モード](../../../ado/guide/data/batch-mode.md)
