---
description: 階層レコードセット内の行へのアクセス (例)
title: 階層レコードセット内の行へのアクセス |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
author: rothja
ms.author: jroth
ms.openlocfilehash: 36ad54e1768b5164294d5de9767757ef3f376144
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991783"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>階層レコードセット内の行へのアクセス (例)
次の例は、階層 [レコードセット](../../reference/ado-api/recordset-object-ado.md)内の行にアクセスするために必要な手順を示しています。

1.  **Authors**テーブルと**Titleauthor**テーブルの**レコードセット**オブジェクトは、作成者 ID によって関連付けられます。

2.  外側のループでは、各作成者の姓、州、および id が表示されます。

3.  各行の追加された **レコードセット** は、 [Fields](../../reference/ado-api/fields-collection-ado.md) コレクションから取得され、 *rstTitleAuthor*に割り当てられます。

4.  内側のループでは、追加された **レコードセット**の各行に4つのフィールドが表示されます。

 [StayInSync](../../reference/ado-api/stayinsync-property.md)プロパティは、説明のために**false**に設定されています。これにより、外側のループの各反復でチャプターが明示的に変更されます。 コード例の効率を高めるために、手順 3. の割り当てを手順2の最初の行の前に移動すると、割り当てが1回だけ実行されるようになります。 次に、 [StayInSync](../../reference/ado-api/stayinsync-property.md)プロパティを**true**に設定します。これにより、 *rst*が新しい行に移動するたびに、 *rstTitleAuthor*が暗黙的に対応する章に自動的に変更されます。

## <a name="example"></a>例

```
Sub datashape()
   Dim cnn As New ADODB.Connection
   Dim rst As New ADODB.Recordset
   Dim rstTitleAuthor As New ADODB.Recordset

   cnn.Provider = "MSDataShape"
   cnn.Open    "Data Provider=MSDASQL;" & _
               "Data Source=SRV;Integrated Security=SSPI;Database=Pubs"
' STEP 1
   rst.StayInSync = FALSE
   rst.Open    "SHAPE  {select * from authors} "  & _
               "APPEND ({select * from titleauthor} " & _
               "RELATE au_id TO au_id) AS chapTitleAuthor", _
               cnn
' STEP 2
   While Not rst.EOF
      Debug.Print    rst("au_fname"), rst("au_lname"), _
                     rst("state"), rst("au_id")
' STEP 3
      Set rstTitleAuthor = rst("chapTitleAuthor").Value
' STEP 4
      While Not rstTitleAuthor.EOF
         Debug.Print rstTitleAuthor(0), rstTitleAuthor(1), _
                     rstTitleAuthor(2), rstTitleAuthor(3)
         rstTitleAuthor.MoveNext
      Wend
      rst.MoveNext
   Wend
End Sub
```

## <a name="see-also"></a>参照
 [データシェイプの概要](./data-shaping-overview.md)[フィールドオブジェクト](../../reference/ado-api/field-object.md)[フィールドコレクション (ado)](../../reference/ado-api/fields-collection-ado.md)の[仮形の文法](./formal-shape-grammar.md) [Microsoft data OLE DB For (ado サービスプロバイダー)](../appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [レコードセットオブジェクト (ado)](../../reference/ado-api/recordset-object-ado.md) [データ](./required-providers-for-data-shaping.md)シェイプ[図形の追加句を追加](./shape-append-clause.md)するには、[一般的な](./shape-commands-in-general.md)shape [COMPUTE 句](./shape-compute-clause.md)のコマンド[Visual Basic for Applications 関数](./visual-basic-for-applications-functions.md)