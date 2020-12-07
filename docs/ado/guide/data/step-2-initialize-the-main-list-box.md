---
description: 手順 2:Main リスト ボックスを初期化する
title: '手順 2: メインリストボックスを初期化する |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
author: rothja
ms.author: jroth
ms.openlocfilehash: 63dd3524ddd70885495c116ff875369ac34784ef
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979533"
---
# <a name="step-2-initialize-the-main-list-box"></a>手順 2:Main リスト ボックスを初期化する
グローバルレコードとレコードセットオブジェクトを宣言するには、Form1 の (宣言) に次のコードを挿入します。  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 このコードは、このシナリオで後ほど使用するレコードおよびレコードセットオブジェクトのグローバルオブジェクト参照を宣言します。  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>URL に接続して lstMain を設定するには  
 Form1 のフォーム読み込みイベントハンドラーに次のコードを挿入します。  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=https://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 このコードは、グローバルレコードとレコードセットオブジェクトをインスタンス化します。 レコードオブジェクトは、 `grec` ActiveConnection として指定された URL で開かれます。 URL が存在する場合は、それが開かれます。まだ存在しない場合は、作成されます。 は、 `https://servername/foldername/` 実際の環境の有効な URL に置き換える必要があることに注意してください。  
  
 レコードセットオブジェクトは、 `grs` レコードの子で開かれ `grec` ます。 次に、 `lstMain` URL に発行されたリソースのファイル名を入力します。  
  
## <a name="see-also"></a>参照  
 [インターネット公開のシナリオ](../../../ado/guide/data/internet-publishing-scenario.md)   
 [手順 1: Visual Basic プロジェクトを設定する](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [手順 3:Fields リスト ボックスに値を設定する](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
