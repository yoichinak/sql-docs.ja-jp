---
description: ADO ランタイムエラー
title: ADO エラー |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b1da9cd8e7afd2b56921fa6b413b5d349d7027f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991733"
---
# <a name="ado-run-time-errors"></a>ADO ランタイムエラー
ADO エラーは、実行時エラーとしてプログラムに報告されます。 プログラミング言語のエラートラップ機構を使用して、それらをトラップして処理することができます。 たとえば、Visual Basic では、 **On Error** ステートメントを使用します。 Visual C++ では、ADO ライブラリへのアクセスに使用している方法によって異なります。 #Import では、 **try-catch** ブロックを使用します。 それ以外の場合、C++ プログラマは **GetErrorInfo**を呼び出すことによって、エラーオブジェクトを明示的に取得する必要があります。 次の Visual Basic のサブプロシージャは、ADO エラーのトラップを示しています。

```
' BeginErrorHandlingVB01
Private Sub Form_Load()
' Turn on error handling
On Error GoTo FormLoadError

'Open the database and the recordset for processing.
'
Dim strCnn As String
strCnn = "Provider=sqloledb;" & _
    "Data Source=a-iresmi2000;" & _
    "Initial Catalog=Northwind;Integrated Security=SSPI"

' cnn is a Public Connection Object because
' it was defined WithEvents
Set cnn = New ADODB.Connection
cnn.Open strCnn

' The next line of code intentionally causes
' an error by trying to open a connection
' that has already been opened.
cnn.Open strCnn

' rst is a Public Recordset because it
' was defined WithEvents
Set rst = New ADODB.Recordset
rst.Open "Customers", cnn

Exit Sub

' Error handler
FormLoadError:
    Dim strErr As String
    Select Case Err
        Case adErrObjectOpen
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            strErr = strErr & "Error reported by: " & Err.Source & vbCrLf
            strErr = strErr & "Help File: " & Err.HelpFile & vbCrLf
            strErr = strErr & "Topic ID: " & Err.HelpContext
            MsgBox strErr
            Debug.Print strErr
            Err.Clear
            Resume Next
        ' If some other error occurs that
        ' has nothing to do with ADO, show
        ' the number and description and exit.
        Case Else
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            MsgBox strErr
            Debug.Print strErr
            Unload Me
    End Select
End Sub
' EndErrorHandlingVB01
```

 この **Form_Load** イベントプロシージャは、同じ **接続** オブジェクトを2回開こうとして、意図的にエラーを作成します。 **Open**メソッドが2回目に呼び出されると、エラーハンドラーがアクティブになります。 この場合、エラーの種類は **adErrObjectOpen**であるため、エラーハンドラーはプログラムの実行を再開する前に次のメッセージを表示します。

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 エラーメッセージには、ここでは適用されない**LastDLLError**値を除き、Visual Basic **Err**オブジェクトによって提供される情報の各部分が含まれます。 エラー番号は、発生したエラーを示します。 この説明は、自分でエラーを処理したくない場合に役立ちます。 単にユーザーに渡すことができます。 通常は、アプリケーション用にカスタマイズされたメッセージを使用しますが、すべてのエラーを予測することはできません。説明には、何が問題になったかについての手掛かりが示されています。 サンプルコードでは、 **接続** オブジェクトによってエラーが報告されています。 オブジェクトの種類またはプログラム ID は、変数名ではなく、ここに表示されます。

> [!NOTE]
>  Visual Basic **Err** オブジェクトには、最新のエラーに関する情報のみが含まれます。 **接続**オブジェクトの ado **Errors**コレクションには、最新の ado 操作によって発生したエラーごとに1つの**エラー**オブジェクトが含まれています。 複数のエラーを処理するには、 **Err**オブジェクトではなく**errors**コレクションを使用します。 **Errors**コレクションの詳細については、「[プロバイダーエラー](./provider-errors.md)」を参照してください。 ただし、有効な **接続** オブジェクトがない場合は、ADO エラーに関する情報の唯一のソースとして **Err** オブジェクトが使用されます。

 ADO エラーの原因となる可能性がある操作の種類 ADO の一般的なエラーには、 **接続** または **レコードセット**などのオブジェクトを開いたり、データを更新したり、プロバイダーでサポートされていないメソッドまたはプロパティを呼び出すことが含まれます。

 OLE DB エラーは、 **エラー** コレクションの実行時エラーとしてアプリケーションに渡すこともできます。

 次のトピックでは、ADO エラーの詳細について説明します。

-   [ADO エラー リファレンス](./ado-error-reference.md)