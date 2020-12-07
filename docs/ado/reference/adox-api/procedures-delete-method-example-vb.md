---
description: Procedures Delete メソッドの例 (VB)
title: Procedures Delete メソッドの例 (VB) |Microsoft Docs
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
- Delete method [ADOX], Visual Basic example
ms.assetid: 94f1ac93-e778-4a40-a85e-94bce5316ac7
author: rothja
ms.author: jroth
ms.openlocfilehash: 16fe01770c486287ff2a188a9c682ffc1e230452
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983523"
---
# <a name="procedures-delete-method-example-vb"></a>Procedures Delete メソッドの例 (VB)
次のコード[は、プロシージャコレクションの](./procedures-collection-adox.md) [delete](./delete-method-adox-collections.md)メソッドを使用してプロシージャを削除する方法を示しています。  
  
```  
' BeginDeleteProcedureVB  
Sub Main()  
    On Error GoTo DeleteProcedureError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog.  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Delete the procedure.  
    cat.Procedures.Delete "CustomerById"  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
DeleteProcedureError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndDeleteProcedureVB  
```  
  
## <a name="see-also"></a>参照  
 [ActiveConnection プロパティ (ADOX)](./activeconnection-property-adox.md)   
 [Catalog オブジェクト (ADOX)](./catalog-object-adox.md)   
 [Delete メソッド (ADOX Collections)](./delete-method-adox-collections.md)   
 [プロシージャオブジェクト (ADOX)](./procedure-object-adox.md)   
 [Procedures コレクション (ADOX)](./procedures-collection-adox.md)