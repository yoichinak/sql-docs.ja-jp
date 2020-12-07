---
description: 競合の検出および解決
title: 競合の検出と解決Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
author: rothja
ms.author: jroth
ms.openlocfilehash: a28fa775c834725504075907f09dc00e95bce1ee
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991393"
---
# <a name="detecting-and-resolving-conflicts"></a>競合の検出および解決
イミディエイトモードでレコードセットを処理する場合、同時実行の問題が発生する可能性は非常に低くなります。 一方、アプリケーションでバッチモードの更新を使用している場合、同じレコードを編集している別のユーザーが行った変更が保存される前に、1人のユーザーがレコードを変更する可能性があります。 このような場合は、アプリケーションで競合を適切に処理する必要があります。 最後のユーザーがサーバーに更新プログラムを送信することになります。 または、競合する2つの値のいずれかを選択することによって、優先する更新プログラムを最新のユーザーが判断できるようにすることもできます。  
  
 どのような場合でも、ADO では Field オブジェクトの UnderlyingValue プロパティと OriginalValue プロパティを使用して、これらの種類の競合を処理します。 これらのプロパティは、レコードセットの Resync メソッドおよび Filter プロパティと組み合わせて使用します。  
  
## <a name="remarks"></a>解説  
 ADO でバッチ更新中に競合が発生すると、エラーコレクションに警告が追加されます。 そのため、BatchUpdate を呼び出した直後にエラーを確認し、問題が見つかった場合は、競合が発生したと仮定してテストを開始する必要があります。 最初の手順では、レコードセットの Filter プロパティを Adfilter衝突 Tingrecords に設定します。 これにより、レコードセットのビューが競合しているレコードのみに制限されます。 この手順の後に RecordCount プロパティが0に等しい場合は、競合以外の方法でエラーが発生したことがわかります。  
  
 BatchUpdate を呼び出すと、ADO およびプロバイダーが、データソースに対する更新を実行する SQL ステートメントを生成しています。 特定のデータソースでは、WHERE 句で使用できる列の型に制限があることに注意してください。  
  
 次に、レコードセットの再同期メソッドを呼び出します。この引数は、ResyncValues 引数を adResyncUnderlyingValues に等しい値に設定します。 再同期メソッドは、基になるデータベースから現在のレコードセットオブジェクトのデータを更新します。 Adを使用すると、現在のフィルター設定で表示できるレコード (競合するレコードのみ) がデータベースと再同期されるようにすることができます。 これにより、大きなレコードセットを扱う場合に、パフォーマンスが大幅に変わる可能性があります。 再同期を呼び出すときに ResyncValues 引数を adResyncUnderlyingValues に設定すると、UnderlyingValue プロパティにデータベースからの (競合している) 値が格納され、ユーザーが入力した値が Value プロパティに保持されます。また、OriginalValue プロパティは、フィールドの元の値 (最後に成功した UpdateBatch 呼び出しが行われてからの値) を保持します これらの値を使用して、プログラムによって競合を解決したり、使用する値をユーザーが選択するように要求したりすることができます。  
  
 この手法を次のコード例に示します。 この例では、別のレコードセットを使用して競合を作成し、UpdateBatch が呼び出される前に基になるテーブルの値を変更しています。  
  
```  
'BeginConflicts  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT * FROM Shippers WHERE ShipperID = 2"  
  
    'Open Rs and change a value  
    Set objRs1 = New ADODB.Recordset  
    Set objRs2 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Introduce a conflict at the db...  
    objRs2.Open strSQL, strConn, adOpenKeyset, adLockOptimistic, adCmdText  
    objRs2("Phone") = "(999) 555-9999"  
    objRs2.Update  
    objRs2.Close  
    Set objRs2 = Nothing  
  
    On Error Resume Next  
    objRs1.UpdateBatch  
  
    If objRs1.ActiveConnection.Errors.Count <> 0 Then  
        Dim intConflicts As Integer  
  
        intConflicts = 0  
  
        objRs1.Filter = adFilterConflictingRecords  
  
        intConflicts = objRs1.RecordCount  
  
        'Resync so we can see the UnderlyingValue and offer user a choice.  
        'This sample only displays all three values and resets to original.  
        objRs1.Resync adAffectGroup, adResyncUnderlyingValues  
  
        If intConflicts > 0 Then  
            strMsg = "A conflict occurred with updates for " & intConflicts & _  
                     " record(s)." & vbCrLf & "The values will be restored" & _  
                     " to their original values." & vbCrLf & vbCrLf  
  
            objRs1.MoveFirst  
            While Not objRs1.EOF  
              strMsg = strMsg & "SHIPPER = " & objRs1("CompanyName") & vbCrLf  
              strMsg = strMsg & "Value = " & objRs1("Phone").Value & vbCrLf  
              strMsg = strMsg & "UnderlyingValue = " & _  
                                 objRs1("Phone").UnderlyingValue & vbCrLf  
              strMsg = strMsg & "OriginalValue = " & _  
                                 objRs1("Phone").OriginalValue & vbCrLf  
              strMsg = strMsg & vbCrLf & "Original value has been restored."  
  
              MsgBox strMsg, vbOKOnly, _  
                    "Conflict " & objRs1.AbsolutePosition & _  
                    " of " & intConflicts  
  
              objRs1("Phone").Value = objRs1("Phone").OriginalValue  
              objRs1.MoveNext  
            Wend  
  
            objRs1.UpdateBatch adAffectGroup  
        Else  
            'Other error occurred. Minimal handling in this example.  
             strMsg = "Errors occurred during the update. " & _  
                        objRs1.ActiveConnection.Errors(0).Number & " " & _  
                        objRs1.ActiveConnection.Errors(0).Description  
        End If  
  
        On Error GoTo 0  
    End If  
  
    objRs1.MoveFirst  
    objRs1.Close  
    Set objRs1 = Nothing  
'EndConflicts  
```  
  
 現在のレコードまたは特定のフィールドの Status プロパティを使用して、発生した競合の種類を特定できます。  
  
 エラー処理の詳細については、「 [エラー処理](./error-handling.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [バッチ モード](./batch-mode.md)