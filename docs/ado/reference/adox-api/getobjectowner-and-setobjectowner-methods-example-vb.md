---
description: GetObjectOwner および SetObjectOwner メソッドの例 (VB)
title: GetObjectOwner メソッドと SetObjectOwner メソッドの例 (VB) |Microsoft Docs
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
- SetObjectOwner method [ADOX], Visual Basic example
- GetObjectOwner method [ADOX], Visual Basic example
ms.assetid: e44ec3d4-42ae-447d-aaed-bdea53cb0cca
author: rothja
ms.author: jroth
ms.openlocfilehash: 8c5b5125f65eec46818ba4d43c8b305f6d82d964
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100054217"
---
# <a name="getobjectowner-and-setobjectowner-methods-example-vb"></a>GetObjectOwner および SetObjectOwner メソッドの例 (VB)
この例では、 [GetObjectOwner](./getobjectowner-method-adox.md) メソッドと [SetObjectOwner](./setobjectowner-method.md) メソッドを示します。 このコードは、グループアカウンティングが存在することを前提としています (グループ [とユーザー Append、ChangePassword メソッドの例 (VB)](./groups-and-users-append-changepassword-methods-example-vb.md) を参照して、システムにこのグループを追加する方法を参照してください)。 Categories テーブルの所有者は、Accounting に設定されています。  
  
```  
' BeginOwnersVB  
Sub OwnersX()  
  
    Dim tblLoop As New ADOX.Table  
    Dim cat As New ADOX.Catalog  
    Dim strOwner As String  
  
    ' Open the Catalog.  
    cat.ActiveConnection = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=c:\Program Files\" & _  
        "Microsoft Office\Office\Samples\Northwind.mdb;" & _  
        "jet oledb:system database=" & _  
        "c:\Program Files\Microsoft Office\Office\system.mdw"  
  
    ' Print the original owner of Categories  
    strOwner = cat.GetObjectOwner("Categories", adPermObjTable)  
    Debug.Print "Owner of Categories: " & strOwner  
  
    ' Set the owner of Categories to Accounting  
    cat.SetObjectOwner "Categories", adPermObjTable, "Accounting"  
  
    ' List the owners of all tables and columns in the catalog.  
    For Each tblLoop In cat.Tables  
        Debug.Print "Table: " & tblLoop.Name  
        Debug.Print "   Owner: " & _  
            cat.GetObjectOwner(tblLoop.Name, adPermObjTable)  
    Next tblLoop  
  
    ' Restore the original owner of Categories  
    cat.SetObjectOwner "Categories", adPermObjTable, strOwner  
  
End Sub  
' EndOwnersVB  
```  
  
## <a name="see-also"></a>参照  
 [Catalog オブジェクト (ADOX)](./catalog-object-adox.md)   
 [GetObjectOwner メソッド (ADOX)](./getobjectowner-method-adox.md)   
 [SetObjectOwner メソッド](./setobjectowner-method.md)