---
description: Fields コレクション
title: Fields コレクション |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
author: rothja
ms.author: jroth
ms.openlocfilehash: 45bad5289a33b5b1f76807f1f7a9da62044dafc2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979383"
---
# <a name="the-fields-collection"></a>Fields コレクション
**Fields**コレクションは、ADO の組み込みコレクションの1つです。 コレクションは、1つの単位として参照できる項目の順序付けされたセットです。 ADO コレクションの詳細については、「 [Ado オブジェクトモデル](../../../ado/guide/data/ado-objects-and-collections.md)」を参照してください。  
  
 **Fields**コレクションには、**レコードセット**内のすべてのフィールド (列) の**フィールド**オブジェクトが含まれています。 すべての ADO コレクションと同様に、 **Count** および **Item** プロパティに加えて、 **Append** メソッドと **Refresh** メソッドがあります。 また、他の ADO コレクションでは使用できない、 **CancelUpdate**、 **Delete**、 **Resync**、および **Update** の各メソッドもあります。  
  
## <a name="examining-the-fields-collection"></a>フィールドコレクションの検査  
 このセクションで紹介するサンプル**レコードセット**の**Fields**コレクションについて考えてみましょう。 サンプル **レコードセット** は、SQL ステートメントから派生したものです。  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 このため、 **レコードセットフィールド** コレクションには3つのフィールドが含まれていることがわかります。  
  
```  
'BeginWalkFields  
    Dim objFields As ADODB.Fields  
    Dim intLoop As Integer  
  
    objRs.Open strSQL, strConnStr, adOpenForwardOnly, adLockReadOnly, adCmdText  
  
    Set objFields = objRs.Fields  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
    Next  
'EndWalkFields  
```  
  
 このコードは、 **Count**プロパティを使用して**Fields**コレクション内の**フィールド**オブジェクトの数を特定し、コレクションをループ処理して、各**field**オブジェクトの**Name**プロパティの値を返します。 多くの **フィールド** プロパティを使用して、フィールドに関する情報を取得できます。 **フィールド**のクエリの詳細については、「 [field オブジェクト](../../../ado/guide/data/the-field-object.md)」を参照してください。  
  
## <a name="counting-columns"></a>カウント (列を)  
 予想されるように、 **Count**プロパティは、 **Fields**コレクション内の**フィールド**オブジェクトの実際の数を返します。 コレクションのメンバーの番号はゼロで始まるので、常にゼロのメンバーで始まり、 **Count** プロパティの値から1を引いた値で終わる必要があります。 Microsoft Visual Basic を使用していて、 **Count** プロパティを確認せずにコレクションのメンバーをループする場合は、for each を使用します。 **次** のコマンド。  
  
 **Count**プロパティが0の場合、コレクションにはオブジェクトが存在しません。  
  
## <a name="getting-to-the-field"></a>フィールドへの取得  
 すべての ADO コレクションと同様に、 **Item** プロパティはコレクションの既定のプロパティです。 このメソッドは、渡された名前またはインデックスによって指定された個々の **Field** オブジェクトを返します。 したがって、次のステートメントは、サンプル **レコードセット**と同等です。  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 これらのメソッドが同等の場合は、それが最適ですか。 一概には言えません。 インデックスを使用してコレクションから **フィールド** を取得する方が高速です。これは、文字列参照を実行することなく、 **フィールド** に直接アクセスするためです。 一方、コレクション内の **フィールド** の順序がわかっている必要があります。順序が変更された場合、その **フィールドの** インデックスへの参照は、どこでも変更する必要があります。 わずかに低速ですが、 **フィールド** の名前を使用する方が、コレクション内の **フィールド** の順序に依存しないため、柔軟性が高くなります。  
  
## <a name="using-the-refresh-method"></a>Refresh メソッドの使用  
 他のいくつかの ADO コレクションとは異なり、 **Fields**コレクションで**Refresh**メソッドを使用しても、可視効果はありません。 基になるデータベース構造から変更を取得するには、 **Requery** メソッドを使用する必要があります。また、 **レコードセット** オブジェクトがブックマークをサポートしていない場合は、 **MoveFirst** メソッドを使用すると、コマンドがプロバイダーに対して再度実行されます。  
  
## <a name="adding-fields-to-a-recordset"></a>レコードセットへのフィールドの追加  
 フィールドを**レコードセット**に追加するには、 **Append**メソッドを使用します。  
  
 **Append**メソッドを使用すると、データソースへの接続を開かずに、プログラムによって**レコードセット**を作成できます。 開いている**レコードセット**の**フィールド**コレクションまたは**ActiveConnection**プロパティが設定されている**レコードセット**で**Append**メソッドが呼び出されると、実行時エラーが発生します。 フィールドを追加できるのは、開かれておらず、まだデータソースに接続されていない **レコードセット** だけです。 ただし、新しく追加した **フィールド**の値を指定するには、まず **レコードセット** を開く必要があります。  
  
 多くの場合、開発者は一時的に一部のデータを保存する場所を必要とします。また、ユーザーインターフェイスでデータバインディングに参加できるように、一部のデータをサーバーから送信されたものとして動作させる必要がある場合もあります。 ADO ( [Microsoft Cursor Service for OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)) を使用すると、開発者は列情報を指定して**Open**を呼び出すことによって、空の**レコードセット**オブジェクトを作成できます。 次の例では、新しい **レコードセット** オブジェクトに3つの新しいフィールドが追加されています。 **レコードセット**が開かれ、2つの新しいレコードが追加され、**レコードセット**がファイルに保存されます。 ( **レコードセット** の永続化の詳細については、「 [データの更新と永続](../../../ado/guide/data/updating-and-persisting-data.md)化」を参照してください)。  
  
```  
'BeginFabricate  
    Dim objRs As ADODB.Recordset  
    Set objRs = New ADODB.Recordset  
  
    With objRs.Fields  
        .Append "StudentID", adChar, 11, adFldUpdatable  
        .Append "FullName", adVarChar, 50, adFldUpdatable  
        .Append "PhoneNmbr", adVarChar, 20, adFldUpdatable  
    End With  
  
    With objRs  
        .Open  
  
        .AddNew  
        .Fields(0) = "123-45-6789"  
        .Fields(1) = "John Doe"  
        .Fields(2) = "(425) 555-5555"  
        .Update  
  
        .AddNew  
        .Fields(0) = "123-45-6780"  
        .Fields(1) = "Jane Doe"  
        .Fields(2) = "(615) 555-1212"  
        .Update  
    End With  
  
    objRs.Save App.Path & "FabriTest.adtg", adPersistADTG  
  
    objRs.Close  
'EndFabricate  
```  
  
 **Fields Append**メソッドの使用方法は、**レコードセット**オブジェクトと**レコード**オブジェクトで異なります。 **レコード**オブジェクトの詳細については、「[レコードとストリーム](../../../ado/guide/data/records-and-streams.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [階層レコードセットの作成](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)
