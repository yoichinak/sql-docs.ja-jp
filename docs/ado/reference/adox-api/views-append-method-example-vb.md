---
description: Views Append メソッドの例 (VB)
title: Views Append メソッドの例 (VB) |Microsoft Docs
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
- Append method [ADOX]
ms.assetid: b5b4c082-ac29-4f49-a8b8-e21b554c9b0d
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f4c065edf9e779887e38f4c09634f6a0bc6a58c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99163939"
---
# <a name="views-append-method-example-vb"></a>Views Append メソッドの例 (VB)
次のコードは、 [コマンド](../ado-api/command-object-ado.md) オブジェクトと [Views](./views-collection-adox.md) collection [Append](./append-method-adox-views.md) メソッドを使用して、基になるデータソースに新しいビューを作成する方法を示しています。  
  
```  
' BeginCreateViewVB  
Sub Main()  
    On Error GoTo CreateViewError  
  
    Dim cmd As New ADODB.Command  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Create the command representing the view.  
    cmd.CommandText = "Select * From Customers"  
  
    ' Create the new View  
    cat.Views.Append "AllCustomers", cmd  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set cmd = Nothing  
    Exit Sub  
  
CreateViewError:  
  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateViewVB  
```  
  
## <a name="see-also"></a>参照  
 [ActiveConnection プロパティ (ADOX)](./activeconnection-property-adox.md)   
 [Append メソッド (ADOX Views)](./append-method-adox-views.md)   
 [Catalog オブジェクト (ADOX)](./catalog-object-adox.md)   
 [View オブジェクト (ADOX)](./view-object-adox.md)   
 [Views コレクション (ADOX)](./views-collection-adox.md)