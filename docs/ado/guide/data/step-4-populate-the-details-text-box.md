---
description: 手順 4:Details テキスト ボックスに値を設定する
title: '手順 4: 詳細を入力するテキストボックス |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cb4273e2-c907-4a86-a621-3bf110088228
author: rothja
ms.author: jroth
ms.openlocfilehash: 88a1b2f9487c80f6b92e2d95b1b667cf1618ba27
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100036921"
---
# <a name="step-4-populate-the-details-text-box"></a>手順 4:Details テキスト ボックスに値を設定する
詳細テキストボックスを設定するには、 **Recfields** という名前の新しいサブルーチンを作成し、次のコードを挿入します。  
  
```  
Sub recFields(r As Record, l As ListBox, t As TextBox)  
    Dim f As Field  
    Dim s As Stream  
    Set s = New Stream  
    Dim str As String  
  
    For Each f In r.Fields  
        l.AddItem f.Name & ": " & f.Value  
    Next  
    t.Text = ""  
    If r!RESOURCE_CONTENTCLASS = "text/plain" Then  
        s.Open r, adModeRead, adOpenStreamFromRecord  
        str = s.ReadText(1)  
        s.Position = 0  
        If Asc(Mid(str, 1, 1)) = 63 Then '//63 = "?"  
            s.Charset = "ascii"  
            s.Type = adTypeText  
        End If  
        t.Text = s.ReadText(adReadAll)  
    End If  
End Sub  
```  
  
 このコードは、 `lstDetails` に渡される単純なレコードのフィールドと値を設定し `recFields` ます。 リソースがテキストファイルの場合は、リソースレコードからテキストストリームが開かれます。 このコードは、文字セットが ASCII であるかどうかを判断し、ストリームの内容をにコピーし `txtDetails` ます。  
  
## <a name="see-also"></a>参照  
 [インターネット公開のシナリオ](../../../ado/guide/data/internet-publishing-scenario.md)   
 [手順 3:Fields リスト ボックスに値を設定する](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
