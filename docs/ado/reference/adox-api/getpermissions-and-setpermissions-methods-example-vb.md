---
description: GetPermissions および SetPermissions メソッドの例 (VB)
title: GetPermissions および SetPermissions メソッドの例 (VB) |Microsoft Docs
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
- SetPermissions method [ADOX], Visual Basic example
- GetPermissions method [ADOX], Visual Basic example
ms.assetid: aa366d98-8c7a-4189-bdd8-1d663b243d33
author: rothja
ms.author: jroth
ms.openlocfilehash: dd933007e37f193b9574999137ebd75371f8dda9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984453"
---
# <a name="getpermissions-and-setpermissions-methods-example-vb"></a>GetPermissions および SetPermissions メソッドの例 (VB)
この例では、 [Getpermissions](./getpermissions-method-adox.md) メソッドと [SetPermissions](./setpermissions-method-adox.md) メソッドを示します。 次のコードでは、Orders テーブルへのフルアクセスが管理者ユーザーに与えられます。  
  
```  
' BeginGrantPermissionsVB  
Sub GrantPermissions()  
    On Error GoTo GrantPermissionsError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim lngPerm As Long  
  
    ' Opens a connection to the northwind database  
    ' using the Microsoft Jet 4.0 provider  
    cnn.Provider = "Microsoft.Jet.OLEDB.4.0"  
    cnn.Open "Data Source='Northwind.mdb';" & _  
        "jet oledb:system database=" & _  
        "'system.mdw'"  
  
    Set cat.ActiveConnection = cnn  
  
    ' Retrieve original permissions  
    lngPerm = cat.Users("admin").GetPermissions("Orders", adPermObjTable)  
    Debug.Print "Original permissions: " & Str(lngPerm)  
  
    ' Revoke all permissions  
    cat.Users("admin").SetPermissions "Orders", adPermObjTable, _  
        adAccessRevoke, adRightFull  
  
    ' Display permissions  
    Debug.Print "Revoked permissions: " & _  
        Str(cat.Users("admin").GetPermissions("Orders", adPermObjTable))  
  
    ' Give the Admin user full rights on the orders object  
    cat.Users("admin").SetPermissions "Orders", adPermObjTable, _  
        adAccessSet, adRightFull  
  
    ' Display permissions  
    Debug.Print "Full permissions: " & _  
        Str(cat.Users("admin").GetPermissions("Orders", adPermObjTable))  
  
    ' Restore original permissions  
    cat.Users("admin").SetPermissions "Orders", adPermObjTable, _  
        adAccessSet, lngPerm  
  
    ' Display permissions  
    Debug.Print "Final permissions: " & _  
        Str(cat.Users("admin").GetPermissions("Orders", adPermObjTable))  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
GrantPermissionsError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndGrantPermissionsVB  
```  
  
## <a name="see-also"></a>参照  
 [Catalog オブジェクト (ADOX)](./catalog-object-adox.md)   
 [GetPermissions メソッド (ADOX)](./getpermissions-method-adox.md)   
 [SetPermissions メソッド (ADOX)](./setpermissions-method-adox.md)   
 [User オブジェクト (ADOX)](./user-object-adox.md)   
 [Users コレクション (ADOX)](./users-collection-adox.md)