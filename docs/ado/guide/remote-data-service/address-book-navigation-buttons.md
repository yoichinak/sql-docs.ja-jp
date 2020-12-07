---
description: アドレス帳のナビゲーション ボタン
title: アドレス帳のナビゲーションボタン |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], navigation buttons
- address book application scenario [ADO], navigation buttons
ms.assetid: f0dd84c6-5c33-4ab9-82b4-4c42dfdd2277
author: rothja
ms.author: jroth
ms.openlocfilehash: 65d5686dc605e1ba254f4b7c39e879eb59733d79
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724843"
---
# <a name="address-book-navigation-buttons"></a>アドレス帳のナビゲーション ボタン
アドレス帳アプリケーションでは、Web ページの下部にナビゲーションボタンが表示されます。 ナビゲーションボタンを使用すると、データの最初の行または最後の行、または現在の選択範囲に隣接する行を選択することにより、HTML グリッドの表示でデータを移動できます。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="navigation-sub-procedures"></a>ナビゲーションサブプロシージャ  
 アドレス帳アプリケーションには、ユーザーが **最初**、 **次**、 **前**へ、および **最後** のボタンをクリックしてデータを移動できるようにするためのいくつかの手順が含まれています。  
  
 たとえば、 **最初** のボタンをクリックすると、VBScript の First_OnClick サブプロシージャがアクティブ化されます。 プロシージャは、 [MoveFirst](../../reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) メソッドを実行します。これにより、データの最初の行が現在の選択範囲になります。 **最後**のボタンをクリックすると、Last_OnClick サブプロシージャがアクティブになります。これにより、 [MoveLast](../../reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)メソッドが呼び出され、データの最後の行が現在の選択範囲になります。 残りのナビゲーションボタンは同様の方法で動作します。  
  
```vb
' Move to the first record in the bound Recordset.  
Sub First_OnClick  
   DC1.Recordset.MoveFirst  
End Sub  
  
' Move to the next record from the current position   
' in the bound Recordset.  
Sub Next_OnClick  
   If Not DC1.Recordset.EOF Then    ' Cannot move beyond bottom record.  
      DC1.Recordset.MoveNext  
      Exit Sub  
   End If     
End Sub  
  
' Move to the previous record from the current position in the bound   
' Recordset.  
Sub Prev_OnClick  
   If Not DC1.Recordset.BOF Then    ' Cannot move beyond top record.  
      DC1.Recordset.MovePrevious  
      Exit Sub  
   End If  
End Sub  
  
' Move to the last record in the bound Recordset.  
Sub Last_OnClick  
   DC1.Recordset.MoveLast  
End Sub  
```  
  
## <a name="see-also"></a>参照  
 [DataControl オブジェクト (RDS)](../../reference/rds-api/datacontrol-object-rds.md)   
 [MoveFirst、MoveLast、MoveNext、MovePrevious メソッド (RDS)](../../reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)