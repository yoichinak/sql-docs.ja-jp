---
description: Views Append メソッドの例 (VB)
title: Views Append メソッドの例 (VB) |Microsoft Docs
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
- Append method [ADOX]
ms.assetid: b5b4c082-ac29-4f49-a8b8-e21b554c9b0d
author: rothja
ms.author: jroth
ms.openlocfilehash: 3be71b5bf0ba2e6424d3b90a7165dcc570cc4cda
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982883"
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