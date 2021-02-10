---
description: 手順 3:Fields リスト ボックスに値を設定する
title: '手順 3: フィールドリストボックスにデータを設定する |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
author: rothja
ms.author: jroth
ms.openlocfilehash: 6555f71d210524622e936026c8945168635de140
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100032434"
---
# <a name="step-3-populate-the-fields-list-box"></a>手順 3:Fields リスト ボックスに値を設定する
[フィールド] ボックスを設定するには、の Click イベントハンドラーに次のコードを挿入し `lstMain` ます。  
  
```  
Private Sub lstMain_Click()  
    Dim rec As Record  
    Dim rs As Recordset  
    Set rec = New Record  
    Set rs = New Recordset  
    grs.MoveFirst  
    grs.Move lstMain.ListIndex  
    lstDetails.Clear  
    rec.Open grs  
    Select Case rec.RecordType  
        Case adCollectionRecord:  
            Set rs = rec.GetChildren  
            While Not rs.EOF  
                lstDetails.AddItem rs(0)  
                rs.MoveNext  
            Wend  
        Case adSimpleRecord:  
            recFields rec, lstDetails, txtDetails  
  
        Case adStructDoc:  
    End Select  
  
End Sub  
```  
  
 このコードは、ローカルレコードとレコードセットオブジェクト、およびをそれぞれ宣言してインスタンス化し `rec` `rs` ます。  
  
 で選択されたリソースに対応する行 `lstMain` がの現在の行になり `grs` ます。 次に、[詳細] リストボックスがクリアされ、 `rec` ソースとしての現在の行で開かれ `grs` ます。  
  
 [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)で指定されているように、リソースがコレクションレコードの場合、ローカルのレコードセット `rs` が rec の子で開かれます。次に、 `lstDetails` の行の値がに格納され `rs` ます。  
  
 リソースが単純なレコードの場合 `recFields` は、が呼び出されます。 の詳細については `recFields` 、次の手順を参照してください。  
  
 リソースが構造化ドキュメントである場合、コードは実装されません。  
  
## <a name="see-also"></a>参照  
 [インターネット公開のシナリオ](../../../ado/guide/data/internet-publishing-scenario.md)   
 [手順 2: メインリストボックスを初期化する](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [手順 4:Details テキスト ボックスに値を設定する](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
