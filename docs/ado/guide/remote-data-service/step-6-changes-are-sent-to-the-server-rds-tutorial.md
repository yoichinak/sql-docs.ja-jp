---
description: 手順 6:変更がサーバーに送信される (RDS チュートリアル)
title: '手順 6: 変更がサーバーに送信される (RDS チュートリアル) |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
author: rothja
ms.author: jroth
ms.openlocfilehash: 9929177baaf1efd486cb9f628034158b370badc7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722863"
---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>手順 6:変更がサーバーに送信される (RDS チュートリアル)
**Recordset**オブジェクトが編集されている場合は、変更 (追加、変更、または削除された行) をサーバーに送り返すことができます。  
  
> [!NOTE]
>  RDS の既定の動作は、ADO オブジェクトと Microsoft OLE DB リモート処理プロバイダーを使用して暗黙的に呼び出すことができます。 クエリは **レコードセット**を返すことができ、編集された **レコードセット**はデータソースを更新できます。 このチュートリアルでは、ADO オブジェクトを使用した RDS は呼び出されませんが、次のようになります。  
  
```vb
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=https://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **パート A** この場合、RDS のみを使用していると仮定し [ます。DataControl](../../reference/rds-api/datacontrol-object-rds.md) で、 **レコードセット** オブジェクトが RDS に関連付けられていることを確認し **ます。DataControl**。 [SubmitChanges](../../reference/rds-api/submitchanges-method-rds.md)メソッドは、[サーバー](../../reference/rds-api/server-property-rds.md)と[接続](../../reference/rds-api/connect-property-rds.md)のプロパティがまだ設定されている場合に、**レコードセット**オブジェクトを変更してデータソースを更新します。  
  
```vb
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "https://yourServer"  
DC. = "DSN=Pubs"  
DC. = "SELECT * FROM Authors"  
DC.  
...  
Set RS = DC.  
   ' Edit the Recordset.  
...  
DC.  
...  
```  
  
 **パート B**または、接続と**レコードセット**オブジェクトを指定して、 [RDSServer. DataFactory](../../reference/rds-api/datafactory-object-rdsserver.md)オブジェクトを使用してサーバーを更新することもできます。  
  
```vb
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **これは、チュートリアルの最後です。**  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
## <a name="see-also"></a>参照  
 [Microsoft OLE DB リモート処理プロバイダー (ADO サービスプロバイダー)](../appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [RDS チュートリアル](./rds-tutorial.md)   
 [RDS のチュートリアル (VBScript)](./rds-tutorial-vbscript.md)