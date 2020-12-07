---
description: Keys Append メソッド、Key Type、RelatedColumn、RelatedTable、UpdateRule プロパティの例 (VB)
title: テーブル間に新しい外部キーリレーションシップを作成する例 (VB) |Microsoft Docs
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
- Key Type property [ADOX], Visual Basic example
- RelatedTable property [ADOX], Visual Basic example
- Keys Append method [ADOX], Visual Basic example
- UpdateRule property [ADOX], Visual Basic example
- RelatedColumn property [ADOX], Visual Basic example
ms.assetid: 13b5b1c3-6af6-439e-bb65-976578ba6bc2
author: rothja
ms.author: jroth
ms.openlocfilehash: edc38c1506e472eddb6640c9d7ca121154dcc4cb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984063"
---
# <a name="keys-append-method-key-type-relatedcolumn-relatedtable-and-updaterule-properties-example-vb"></a>Keys Append メソッド、Key Type、RelatedColumn、RelatedTable、UpdateRule プロパティの例 (VB)
次のコードは、 **Customers** と **Orders**という名前の2つの既存のテーブル間に新しい外部キーリレーションシップを作成する方法を示しています。  
  
```  
' BeginCreateKeyVB  
Sub Main()  
    On Error GoTo CreateKeyError  
  
    Dim kyForeign As New ADOX.Key  
    Dim cat As New ADOX.Catalog  
  
    ' Connect to the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Define the foreign key.  
    kyForeign.Name = "CustOrder"  
    kyForeign.Type = adKeyForeign  
    kyForeign.RelatedTable = "Customers"  
    kyForeign.Columns.Append "CustomerId"  
    kyForeign.Columns("CustomerId").RelatedColumn = "CustomerId"  
    kyForeign.UpdateRule = adRICascade  
  
    ' Append the foreign key to the keys collection.  
    cat.Tables("Orders").Keys.Append kyForeign  
  
    'Delete the key t demonstrate the Delete method.  
    cat.Tables("Orders").Keys.Delete kyForeign.Name  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set kyForeign = Nothing  
    Exit Sub  
  
CreateKeyError:  
    Set cat = Nothing  
    Set kyForeign = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndCreateKeyVB  
```  
  
## <a name="see-also"></a>参照  
 [Append メソッド (ADOX Columns)](./append-method-adox-columns.md)   
 [Append メソッド (ADOX Keys)](./append-method-adox-keys.md)   
 [Catalog オブジェクト (ADOX)](./catalog-object-adox.md)   
 [Column オブジェクト (ADOX)](./column-object-adox.md)   
 [Columns コレクション (ADOX)](./columns-collection-adox.md)   
 [Key オブジェクト (ADOX)](./key-object-adox.md)   
 [Keys コレクション (ADOX)](./keys-collection-adox.md)   
 [Name プロパティ (ADOX)](./name-property-adox.md)   
 ["関連性列" プロパティ (ADOX)](./relatedcolumn-property-adox.md)   
 ["関連性テーブル" プロパティ (ADOX)](./relatedtable-property-adox.md)   
 [Table オブジェクト (ADOX)](./table-object-adox.md)   
 [Tables コレクション (ADOX)](./tables-collection-adox.md)   
 [Type プロパティ (キー) (ADOX)](./type-property-key-adox.md)   
 [UpdateRule プロパティ (ADOX)](./updaterule-property-adox.md)