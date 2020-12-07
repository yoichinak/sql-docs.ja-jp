---
description: Delete メソッドを使用してレコードを削除する
title: Delete メソッドを使用してレコードを削除する |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
author: rothja
ms.author: jroth
ms.openlocfilehash: d01223eae3f72a9a89b5f2e18b19c181a575052b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991403"
---
# <a name="deleting-records-using-the-delete-method"></a>Delete メソッドを使用してレコードを削除する
**Delete**メソッドを使用すると、**レコードセット**オブジェクト内の現在のレコードまたはレコードのグループが削除対象としてマークされます。 レコード **セット** オブジェクトでレコードの削除が許可されていない場合、エラーが発生します。 即時更新モードの場合、削除はすぐにデータベースで発生します。 たとえば、データベースの整合性違反が原因でレコードを正常に削除できない場合、レコードは更新の呼び出し後も編集モードのままになり **ます。** これは、現在のレコードから移動する前に、 [CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md) を使用して更新を取り消す必要があることを意味します (たとえば、 [Close](../../reference/ado-api/close-method-ado.md)、 [Move](../../reference/ado-api/move-method-ado.md)、または [NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)を使用します)。  
  
 バッチ更新モードの場合、レコードはキャッシュから削除対象としてマークされ、実際の削除は、 **UpdateBatch** メソッドを呼び出したときに行われます。 (削除されたレコードを表示するには、 **Delete**が呼び出された後に、 **Filter**プロパティを**adFilterAffectedRecords**に設定します)。  
  
 削除されたレコードからフィールド値を取得しようとすると、エラーが発生します。 現在のレコードを削除すると、別のレコードに移動するまで、削除されたレコードは最新の状態のままになります。 削除されたレコードから移動すると、アクセスできなくなります。  
  
 トランザクションで削除を入れ子にすると、 **RollbackTrans** メソッドを使用して、削除されたレコードを回復できます。 バッチ更新モードの場合は、 **CancelBatch** メソッドを使用して、保留中の削除または保留中の削除のグループを取り消すことができます。  
  
 基になるデータと競合しているためにレコードを削除しようとして失敗した場合 (たとえば、レコードが別のユーザーによって既に削除されている場合)、プロバイダは **Errors** コレクションに警告を返しますが、プログラムの実行を停止することはありません。 実行時エラーは、要求されたすべてのレコードに競合がある場合にのみ発生します。  
  
 **Unique table**動的プロパティが設定されていて、**レコードセット**が複数のテーブルに対して結合操作を実行した結果である場合、 **Delete**メソッドでは、**一意のテーブル**プロパティのという名前のテーブルからのみ行が削除されます。  
  
 **Delete**メソッドは、省略可能な引数を受け取ります。この引数を使用すると、**削除**操作の影響を受けるレコードを指定できます。 この引数の有効な値は、次のいずれかの ADO **AffectEnum** 列挙定数です。  
  
-   **現在の** もの現在のレコードのみに影響します。  
  
-   **adて** います。現在の **フィルター** プロパティの設定に適合するレコードのみに影響します。 このオプションを使用するには、 **filter** プロパティを **filtergroupenum** 値または **ブックマーク** の配列に設定する必要があります。  
  
 次のコードは、 **Delete**メソッドを呼び出すときに、 **adが**指定したグループを指定する例を示しています。 この例では、いくつかのレコードをサンプル **レコードセット** に追加し、データベースを更新します。 次に、 **adFilterAffectedRecords** filter 列挙定数を使用して**レコードセット**をフィルター処理します。これにより、新しく追加されたレコードだけがレコードセットに表示され**ます。** 最後に、 **Delete** メソッドを呼び出し、現在の **フィルター** プロパティの設定 (新しいレコード) を満たすすべてのレコードを削除するように指定します。  
  
```  
'BeginDeleteGroup  
    'add some bogus records  
    With objRs  
        For i = 0 To 8  
            .AddNew  
            .Fields("CompanyName") = "Shipper Number " & i + 1  
            .Fields("Phone") = "(425) 555-000" & (i + 1)  
            .Update  
        Next i  
  
        ' update  
        .UpdateBatch  
  
        'filter on newly added records  
        .Filter = adFilterAffectedRecords  
        Debug.Print "Deleting the " & .RecordCount & _  
                    " records you just added."  
  
        'delete the newly added bogus records  
        .Delete adAffectGroup  
        .Filter = adFilterNone  
        Debug.Print .RecordCount & " records remain."  
    End With  
'EndDeleteGroup  
```