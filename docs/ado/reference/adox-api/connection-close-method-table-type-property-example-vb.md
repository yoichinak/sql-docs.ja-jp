---
description: Connection Close メソッド、Table Type プロパティの例 (VB)
title: Connection Close メソッド、Table Type プロパティの例 (VB) |Microsoft Docs
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
- Close method [ADOX], Visual Basic example
- Type property [ADOX], Visual Basic example
ms.assetid: f88e7a3b-19ed-46e2-b2ce-3b611d9b8166
author: rothja
ms.author: jroth
ms.openlocfilehash: 00b3758db44e89d4c14b3a57bea8a7e7e3bdd158
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100054337"
---
# <a name="connection-close-method-table-type-property-example-vb"></a>Connection Close メソッド、Table Type プロパティの例 (VB)
[ActiveConnection](./activeconnection-property-adox.md)プロパティを **Nothing** に設定する場合は、カタログへの接続を閉じる必要があります。 関連付けられたコレクションは空になります。 カタログ内のスキーマオブジェクトから作成されたオブジェクトは孤立します。 キャッシュされているオブジェクトのプロパティは引き続き利用できますが、プロバイダーの呼び出しを必要とするプロパティの読み取りは失敗します。  
  
```  
' BeginCloseConnectionVB  
Sub Main()  
    On Error GoTo CloseConnectionByNothingError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tbl As ADOX.Table  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Set tbl = cat.Tables(0)  
    Debug.Print tbl.Type    ' Cache tbl.Type info  
    Set cat.ActiveConnection = Nothing  
    Debug.Print tbl.Type    ' tbl is orphaned  
    ' Previous line will succeed if this info was cached.  
    Debug.Print tbl.Columns(0).DefinedSize  
    ' Previous line will fail if this info has not been cached.  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CloseConnectionByNothingError:  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCloseConnectionVB  
```  
  
 カタログを開くために使用された [接続](../ado-api/connection-object-ado.md) オブジェクトを閉じるには、 **ActiveConnection** プロパティを **Nothing** に設定するのと同じ効果が得られます。  
  
```  
Attribute VB_Name = "Connection"  
```  
  
## <a name="see-also"></a>参照  
 [ActiveConnection プロパティ (ADOX)](./activeconnection-property-adox.md)   
 [Catalog オブジェクト (ADOX)](./catalog-object-adox.md)   
 [Column オブジェクト (ADOX)](./column-object-adox.md)   
 [Columns コレクション (ADOX)](./columns-collection-adox.md)   
 [Table オブジェクト (ADOX)](./table-object-adox.md)   
 [Tables コレクション (ADOX)](./tables-collection-adox.md)   
 [Type プロパティ (テーブル) (ADOX)](./type-property-table-adox.md)