---
description: ブックマークを使用する
title: ブックマークを使用する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
author: rothja
ms.author: jroth
ms.openlocfilehash: 34fc17275609dbf08ffa02a1bc89902c904cac85
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979042"
---
# <a name="using-bookmarks"></a>ブックマークを使用する
場合によっては、レコード **セット** 内を移動した後に特定のレコードに直接戻ると、すべてのレコードをスクロールして値を比較する必要がなくなります。 たとえば、 **Find** メソッドを使用してレコードを検索しようとしても、レコードが返されない場合は、レコード **セット**の両端に自動的に配置されます。 プロバイダーでサポートされている場合は、 **検索** メソッドを使用する前にブックマークを使用して、場所に戻ることができます。 ブックマークは、レコード**セット**オブジェクト内のレコードを一意に識別する**バリアント**型の値です。  
  
 レコード **セットフィルター** メソッドを使用して、一連のブックマークのバリアント配列を使用して、選択したレコードのセットをフィルター処理することもできます。 この手法の詳細については、このセクションで後述する「 [レコードセットの](../../../ado/guide/data/working-with-recordsets.md)使用」の「結果のフィルター処理」を参照してください。  
  
 **Bookmark**プロパティを使用すると、レコードのブックマークを取得できます。また、レコード**セット**オブジェクトの現在のレコードを、有効なブックマークで識別されるレコードに設定することもできます。 次のコードでは、 **bookmark** プロパティを使用してブックマークを設定し、他のレコードに移動した後にブックマークを付けたレコードに戻ります。 **レコードセット**でブックマークがサポートされているかどうかを判断するには、**サポート**メソッドを使用します。  
  
```  
'BeginBookmarkEg  
Dim varBookmark As Variant  
Dim blnCanBkmrk As Boolean  
  
objRs.Open strSQL, strConnStr, adOpenStatic, adLockOptimistic, adCmdText  
  
If objRs.RecordCount > 4 Then  
    objRs.Move 4                       ' move to the fifth record  
    blnCanBkmrk = objRs.Supports(adBookmark)  
    If blnCanBkmrk = True Then  
        varBookmark = objRs.Bookmark   ' record the bookmark  
        objRs.MoveLast                 ' move to a different record  
        objRs.Bookmark = varBookmark   ' return to the bookmarked (sixth) record  
    End If  
End If  
'EndBookmarkEg  
```  
  
 [サポート](../../../ado/reference/ado-api/supports-method.md)メソッドの詳細については、後で詳しく説明します。  
  
 複製された **レコードセット**の場合を除き、ブックマークは、同じコマンドが使用されている場合でも、作成された **レコードセット** に対して一意です。 つまり、1つの**レコードセット**から取得した**ブックマーク**を使用して、同じコマンドで開かれた2番目のレコード**セット**内の同じレコードに移動することはできません。
