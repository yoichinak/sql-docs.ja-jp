---
description: Columns および Tables Append メソッド、Name プロパティの例 (VB)
title: Columns および Tables Append メソッド、Name プロパティの例 (VB) |Microsoft Docs
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
- Name property [ADOX], Visual Basic example
- Append method [ADOX], Visual Basic example
ms.assetid: 678e5546-df5d-4cd0-bfe9-6cf13cb385c0
author: rothja
ms.author: jroth
ms.openlocfilehash: d6abaa7afda45e7000a18f8080655c9c16ae5ee8
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100050282"
---
# <a name="columns-and-tables-append-methods-name-property-example-vb"></a>Columns および Tables Append メソッド、Name プロパティの例 (VB)
次のコードは、新しいテーブルを作成する方法を示しています。  
  
```  
' BeginCreateTableVB  
Sub Main()  
    On Error GoTo CreateTableError  
  
    Dim tbl As New Table  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    tbl.Name = "MyTable"  
    tbl.Columns.Append "Column1", adInteger  
    tbl.Columns.Append "Column2", adInteger  
    tbl.Columns.Append "Column3", adVarWChar, 50  
    cat.Tables.Append tbl  
    Debug.Print "Table 'MyTable' is added."  
  
    'Delete the table as this is a demonstration.  
    cat.Tables.Delete tbl.Name  
    Debug.Print "Table 'MyTable' is deleted."  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set tbl = Nothing  
    Exit Sub  
  
CreateTableError:  
  
    Set cat = Nothing  
    Set tbl = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateTableVB  
```  
  
## <a name="see-also"></a>参照  
 [Append メソッド (ADOX Columns)](./append-method-adox-columns.md)   
 [Append メソッド (ADOX Tables)](./append-method-adox-tables.md)   
 [Column オブジェクト (ADOX)](./column-object-adox.md)   
 [Columns コレクション (ADOX)](./columns-collection-adox.md)   
 [Name プロパティ (ADOX)](./name-property-adox.md)   
 [Table オブジェクト (ADOX)](./table-object-adox.md)   
 [Tables コレクション (ADOX)](./tables-collection-adox.md)