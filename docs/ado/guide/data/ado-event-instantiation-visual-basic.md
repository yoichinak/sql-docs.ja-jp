---
description: 'ADO イベントのインスタンス化: Visual Basic'
title: 'ADO イベントのインスタンス化: Visual Basic |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
ms.assetid: dce0a2a3-326f-4aaf-a822-6c5549833afa
author: rothja
ms.author: jroth
ms.openlocfilehash: 32b4c4e9da14c264913ed477059fa00eed093e1b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991683"
---
# <a name="ado-event-instantiation-visual-basic"></a>ADO イベントのインスタンス化: Visual Basic
Microsoft® Visual Basic®で ADO イベントを処理するには、 **WithEvents** キーワードを使用してモジュールレベルの変数を宣言する必要があります。 変数は、クラスモジュールの一部としてのみ宣言でき、モジュールレベルで宣言する必要があります。 ただし、Visual Basic **フォーム** オブジェクトもクラスであるため、このような制限はありません。 ADO イベントを処理する最も簡単な方法は、 **WithEvents**を使用して変数を宣言することです。 次の例では、**接続**オブジェクトの**connectcomplete**イベントを処理します。  
  
```  
' BeginEventExampleVB02  
Dim WithEvents connEvent As Connection  
Attribute connEvent.VB_VarHelpID = -1  
  
Private Sub Form_Load()  
Dim strConn As String  
  
   ' Create a new object with event  
   ' handling enabled.  
   strConn = "Provider=sqloledb;" & _  
      "Data Source=MyServer;" & _  
      "Initial Catalog=Northwind;" & _  
      "Integrated Security=SSPI;"  
   Set connEvent = New ADODB.Connection  
   connEvent.Open strConn  
End Sub  
  
Private Sub connEvent_ConnectComplete(ByVal pError As ADODB.Error, _  
    adStatus As ADODB.EventStatusEnum, _  
    ByVal pConnection As ADODB.Connection)  
Dim strMsg As String  
  
   If adStatus = adStatusErrorsOccurred Then  
      Select Case pError.Number  
         Case adErrOperationCancelled  
            ' The operation was cancelled in the  
            ' Will event. Notify the user and exit.  
            strMsg = "I'm sorry you can't connect right now." & vbCrLf  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
         Case Else  
            strMsg = "Error " & Format(pError.Number) & vbCrLf  
            strMsg = strMsg & pError.Description  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
      End Select  
   End If  
   frmWait.btnOK.Enabled = True  
End Sub  
' EndEventExampleVB02  
```  
  
 イベント処理を有効にするには、 **WithEvents**キーワードを使用して、**接続**オブジェクトを**フォーム**レベルで宣言します。 Form_Load イベントハンドラーは、新しい **接続** オブジェクトを *connEvent* に割り当て、接続を開くことによって、実際にオブジェクトを作成します。 もちろん、実際のアプリケーションでは、ここで示したよりも Form_Load イベントハンドラーでの処理が多くなります。
