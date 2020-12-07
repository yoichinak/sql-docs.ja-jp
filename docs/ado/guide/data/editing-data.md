---
description: データの編集
title: データの編集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, editing data
- AdUseClient [ADO]
- editing data [ADO]
ms.assetid: ef514f85-c446-4f05-824e-c9313b2ffae1
author: rothja
ms.author: jroth
ms.openlocfilehash: b39e62f1d7fc55c2d58b382677efa41e4df784a3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991343"
---
# <a name="editing-data"></a>データの編集
ADO を使用してデータソースに接続し、コマンドを実行して、 **レコードセット** オブジェクトの結果を取得し、 **レコードセット**内を移動する方法について説明しました。 このセクションでは、データの編集に関する次の基本的な ADO 操作について説明します。  
  
 このセクションでは、[データの検査](./examining-data.md)で導入されたサンプル**レコードセット**を使用します。重要な変更点が1つあります。 **レコードセット**を開くには、次のコードを使用します。  
  
```  
'BeginEditIntro  
    Dim strSQL As String  
    Dim objRs1 As ADODB.Recordset  
  
    strSQL = "SELECT * FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
  
    objRs1.Open strSQL, GetNewConnection, adOpenStatic, _  
                adLockBatchOptimistic, adCmdText  
  
    ' Disconnect the Recordset from the Connection object.  
    Set objRs1.ActiveConnection = Nothing  
'EndEditIntro  
```  
  
 このコードの重要な変更点は、 *Getnewconnection*関数の**AdUseClient**に等しい**接続**オブジェクトの**cursor location**プロパティを設定することです (次の例を参照)。これは、クライアントカーソルの使用を示します。 クライアント側とサーバー側のカーソルの相違点の詳細については、「 [カーソルとロック](./understanding-cursors-and-locks.md)について」を参照してください。  
  
 Cursor **location** プロパティの **adUseClient** 設定によって、カーソルの位置がデータソース (この場合は SQL Server) からクライアントコード (デスクトップワークステーション) の場所に移動します。 この設定では、カーソルを作成して管理するために、クライアント上の OLE DB のクライアントカーソルエンジンが ADO によって強制的に呼び出されます。  
  
 **Open**メソッドの**LockType**パラメーターが**adlockbatchoptimistic**に変更されたことにも気が付きます。 バッチモードでカーソルが開きます。 (プロバイダーによって複数の変更がキャッシュされ、 **UpdateBatch** メソッドを呼び出すと、基になるデータソースに書き込まれます)。この **レコードセット** に加えられた変更は、 **UpdateBatch** メソッドが呼び出されるまでデータベースで更新されません。  
  
 最後に、このセクションのコードでは、GetNewConnection 関数の変更バージョンを使用します。 このバージョンの関数では、クライアント側のカーソルが返されるようになりました。 関数は次のようになります。  
  
```  
'BeginNewConnection  
Public Function GetNewConnection() As ADODB.Connection  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim strConnStr As String  
  
    strConnStr = "Provider='SQLOLEDB';Initial Catalog='Northwind';" & _  
                 "Data Source='MySqlServer';Integrated Security='SSPI';"  
  
    objConn.ConnectionString = strConnStr  
    objConn.CursorLocation = adUseClient  
    objConn.Open  
  
    Set GetNewConnection = objConn  
  
    Exit Function  
  
ErrHandler:  
    Set objConn = Nothing  
    Set GetNewConnection = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Function  
'EndNewConnection  
```  
  
 このセクションでは、次のトピックを扱います。  
  
-   [既存のレコードの編集](./editing-existing-records.md)  
  
-   [レコードの追加](./adding-records.md)  
  
-   [サポートされている機能を特定する](./determining-what-is-supported.md)  
  
-   [Delete メソッドを使用してレコードを削除する](./deleting-records-using-the-delete-method.md)  
  
-   [代替: SQL ステートメントの使用](./alternatives-using-sql-statements.md)