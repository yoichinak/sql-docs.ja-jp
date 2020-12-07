---
description: プロバイダー エラー
title: プロバイダーエラー |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
author: rothja
ms.author: jroth
ms.openlocfilehash: b31f530bafd69d59c98893cc2ead29039372dea9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979983"
---
# <a name="provider-errors"></a>プロバイダー エラー
プロバイダーエラーが発生すると、-2147467259 の実行時エラーが返されます。 このエラーが発生した場合は、アクティブな**接続**オブジェクトの**エラー**コレクションを確認します。これには、発生した問題を説明する1つ以上のエラーが含まれます。  
  
## <a name="the-ado-errors-collection"></a>ADO Errors コレクション  
 特定の ADO 操作によって複数のプロバイダーエラーが生成される可能性があるため、ADO は **接続** オブジェクトを介してエラーオブジェクトのコレクションを公開します。 操作が正常に終了し、問題が発生し、プロバイダーが1つ以上 **のエラーを** 発生させた場合、このコレクションにはオブジェクトが含まれていません。 各エラーオブジェクトを調べて、エラーの正確な原因を特定します。  
  
 発生したエラーの処理が完了するとすぐに、 **clear** メソッドを呼び出してコレクションをクリアできます。 特に、**レコードセット**オブジェクトに対して**Resync**、 **UpdateBatch**、または**CancelBatch**メソッドを呼び出す前、または**接続**オブジェクトで**Open**メソッドを呼び出す前に、 **Errors**コレクションを明示的にクリアしたり、**レコードセット**オブジェクトの**Filter**プロパティを設定したりすることが重要です。 コレクションを明示的にクリアすることによって、コレクション内の **エラー** オブジェクトが前の操作から除外されないようにすることができます。  
  
 一部の操作では、エラーに加えて警告が生成されることがあります。 警告**は、エラーコレクション内の****エラー**オブジェクトによっても表されます。 プロバイダーが警告をコレクションに追加しても、実行時エラーは生成されません。 **エラー**コレクションの**Count**プロパティを調べて、特定の操作によって警告が生成されたかどうかを確認します。 カウントが1つ以上の場合は、 **エラー** オブジェクトがコレクションに追加されています。 **エラーコレクションに**エラーまたは警告が含まれていると判断したら、すぐにコレクションを反復処理し、含まれている各**エラー**オブジェクトに関する情報を取得できます。 次の短い Visual Basic 例では、これを示します。  
  
```  
' BeginErrorHandlingVB02  
Private Function DeleteCustomer(ByVal CompanyName As String) As Long  
    On Error GoTo DeleteCustomerError  
  
    rst.Find "CompanyName='" & CompanyName & "'"  
DeleteCustomerError:  
Dim objError As ADODB.Error  
Dim strError As String  
  
    If cnn.Errors.Count > 0 Then  
        For Each objError In cnn.Errors  
            strError = strError & "Error #" & objError.Number & _  
                " " & objError.Description & vbCrLf & _  
                "NativeError: " & objError.NativeError & vbCrLf & _  
                "SQLState: " & objError.SQLState & vbCrLf & _  
                "Reported by: " & objError.Source & vbCrLf & _  
                "Help file: " & objError.HelpFile & vbCrLf & _  
                "Help Context ID: " & objError.HelpContext  
        Next  
        MsgBox strError  
    End If  
End Function  
' EndErrorHandlingVB02  
```  
  
 エラー処理ルーチンには、 **Errors**コレクション内の各オブジェクトを検査する**for each**ループが含まれています。 この例では、表示するメッセージを累積します。 作業中のプログラムでは、すべての開いているファイルを閉じ、正しいタイミングでプログラムをシャットダウンするなど、各エラーに対して適切なタスクを実行するコードを記述します。  
  
## <a name="the-error-object"></a>Error オブジェクト  
 **エラーオブジェクトを**調べることによって、発生したエラーと、そのエラーの原因となったアプリケーションまたはオブジェクトを特定できます。 **Error**オブジェクトには、次のプロパティがあります。  
  
|プロパティ名|説明|  
|-------------------|-----------------|  
|**説明**|発生したエラーの説明テキスト。|  
|**HelpContext、HelpFile**|発生したエラーの説明を含むヘルプトピックおよびヘルプファイルを参照します。|  
|**NativeError**|プロバイダー固有のエラー番号。|  
|**Number**|発生したエラーの数値 ( **Errorvalueenum**に示されている) を表す長整数。|  
|**ソース**|エラーを生成したオブジェクトまたはアプリケーションの名前を示します。|  
|**SQLState**|SQL ステートメントの処理中にプロバイダーが返す5文字のエラーコード。|  
  
 ADO **Error** オブジェクトは、標準の Visual Basic **Err** オブジェクトと非常によく似ています。 このプロパティは、発生したエラーを示します。 エラーの数に加えて、関連する2つの情報も受け取ります。 "この **エラー** " プロパティには、使用しているプロバイダー固有のエラー番号が含まれています。 前の例では、プロバイダーは SQL Server 用の Microsoft OLE DB プロバイダーなので、このプロバイダーは SQL Server に固有の **エラーを含ん** でいます。 **SQLState**プロパティには、SQL ステートメントのエラーを説明する5文字のコードが含まれています。  
  
## <a name="event-related-errors"></a>イベントに関連するエラー  
 **Error**オブジェクトは、イベント関連のエラーが発生した場合にも使用されます。 イベントパラメーターとして渡された **error** オブジェクトをチェックすることにより、ADO イベントを発生させたプロセスでエラーが発生したかどうかを確認できます。  
  
 イベントの原因となった操作が正常に終了した場合、イベントハンドラーの *adstatus* パラメーターは *adstatusok*に設定されます。 一方、イベントを発生させた操作が失敗した場合、 *adstatus* パラメーターは *Adstatuserrorの curred*に設定されます。 その場合、エラーを説明する**エラー**オブジェクト*が、エラー*メッセージに表示されます。
