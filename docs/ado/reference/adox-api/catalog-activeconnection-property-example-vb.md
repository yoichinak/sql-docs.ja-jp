---
description: カタログ ActiveConnection プロパティの例 (VB)
title: Catalog ActiveConnection プロパティの例 (VB) |Microsoft Docs
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
- ActiveConnection property [ADOX], Visual Basic example
ms.assetid: bb3274b1-764d-43a7-a49f-ef55680ecd26
author: rothja
ms.author: jroth
ms.openlocfilehash: 7d79ad455184a8cb97a92c7dcc458e7fff2eddf0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99172257"
---
# <a name="catalog-activeconnection-property-example-vb"></a>カタログ ActiveConnection プロパティの例 (VB)
[ActiveConnection](./activeconnection-property-adox.md)プロパティを有効な開いている接続に設定すると、カタログが開きます。 開いているカタログから、そのカタログ内に含まれているスキーマオブジェクトにアクセスできます。  
  
```  
' BeginOpenConnectionVB  
Sub Main()  
    On Error GoTo OpenConnectionError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Debug.Print cat.Tables(0).Type  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
OpenConnectionError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndOpenConnectionVB  
```  
  
 **ActiveConnection** プロパティを有効な接続文字列に設定すると、カタログも "開く" ことができます。  
  
```  
Attribute VB_Name = "Catalog"  
```  
  
## <a name="see-also"></a>参照  
 [ActiveConnection プロパティ (ADOX)](./activeconnection-property-adox.md)   
 [Catalog オブジェクト (ADOX)](./catalog-object-adox.md)   
 [Table オブジェクト (ADOX)](./table-object-adox.md)   
 [Tables コレクション (ADOX)](./tables-collection-adox.md)   
 [Type プロパティ (テーブル) (ADOX)](./type-property-table-adox.md)