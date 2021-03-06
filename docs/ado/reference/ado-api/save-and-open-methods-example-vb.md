---
description: Save および Open メソッドの例 (VB)
title: Save および Open メソッドの例 (VB) |Microsoft Docs
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
- Save method [ADO], Visual Basic example
- Open method [ADO]
ms.assetid: ddccdf58-9c57-4c9b-8b7f-0cf193f955fb
author: rothja
ms.author: jroth
ms.openlocfilehash: 0eafd067cdad9c107c591d09b5b5f50fdc6bc501
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100040692"
---
# <a name="save-and-open-methods-example-vb"></a>Save および Open メソッドの例 (VB)
次の3つの例は、 [Save](./save-method.md) メソッドと [Open](./open-method-ado-recordset.md) メソッドを一緒に使用する方法を示しています。  
  
 データベースからテーブルを使用して、事業旅行を行っているとします。 前に、データを [レコードセット](./recordset-object-ado.md) としてアクセスし、転送可能な形式で保存します。 宛先に到達すると、 **レコードセット** にローカルの切断された **レコードセット** としてアクセスします。 **レコードセット** に変更を加え、再度保存します。 最後に、home を返したときに、もう一度データベースに接続し、その時点で行った変更を反映して更新します。  
  
 まず、 ***Authors*** テーブルにアクセスして保存します。  
  
```  
'BeginSaveVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstAuthors As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_id, au_lname, au_fname, city, phone FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenDynamic, adLockOptimistic, adCmdText  
  
    'For sake of illustration, save the Recordset to a diskette in XML format  
    rstAuthors.Save "c:\Pubs.xml", adPersistXML  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    'clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndSaveVB  
```  
  
 この時点で、宛先に到達しました。 ***Authors** _ テーブルには、ローカルの接続されていない _ * レコードセット * * としてアクセスします。 保存したファイルへのアクセスに使用しているコンピューターに、a:\Pubs.xml の **Mspersist** プロバイダーが必要です。  
  
```  
Attribute VB_Name = "Save"  
```  
  
 最後に、[ホーム] を返します。 次に、変更を使用してデータベースを更新します。  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>参照  
 [Open メソッド (ADO Recordset)](./open-method-ado-recordset.md)   
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)   
 [レコードセットの永続性の詳細](../../guide/data/more-about-recordset-persistence.md)   
 [Save メソッド](./save-method.md)