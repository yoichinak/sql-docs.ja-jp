---
description: 手順 2:サーバー プログラムを呼び出す (RDS チュートリアル)
title: '手順 2: サーバープログラムを起動する (RDS チュートリアル) |Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
author: rothja
ms.author: jroth
ms.openlocfilehash: a9238fa208a5ce415986fee05045dc7ea34e0d67
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91723003"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>手順 2:サーバー プログラムを呼び出す (RDS チュートリアル)
クライアント *プロキシ*でメソッドを呼び出すと、サーバー上の実際のプログラムによってメソッドが実行されます。 この手順では、サーバーでクエリを実行します。  
  
> [!IMPORTANT]
>  Windows 8 と windows Server 2012 以降では、RDS サーバーコンポーネントが Windows オペレーティングシステムに含まれなくなりました (詳細については、「Windows 8 および [Windows server 2012 の互換性に関するクックブック](https://www.microsoft.com/download/details.aspx?id=27416) 」を参照してください)。 RDS クライアントコンポーネントは、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションは、 [WCF Data Service](/dotnet/framework/wcf/)に移行する必要があります。  
  
 **パート A** このチュートリアルで RDSServer を使用して [い](../../reference/rds-api/datafactory-object-rdsserver.md) ない場合、この手順を実行する最も便利な方法は、RDS を使用することです。 [DataControl](../../reference/rds-api/datacontrol-object-rds.md) オブジェクト。 **RDS。DataControl**は、プロキシを作成する前の手順を結合します。この手順では、クエリを発行します。  
  
 RDS を設定し **ます。** サーバープログラムをインスタンス化する必要がある場所を識別する DataControl Object [サーバー](../../reference/rds-api/server-property-rds.md) プロパティ。接続 [プロパティを](../../reference/rds-api/connect-property-rds.md) 使用して、データソースにアクセスするための接続文字列を指定します。クエリコマンドテキストを指定する [SQL](../../reference/rds-api/sql-property.md) プロパティ。 次に、 [Refresh](../../reference/rds-api/refresh-method-rds.md) メソッドを発行して、サーバープログラムがデータソースに接続し、クエリで指定された行を取得し、 **レコードセット** オブジェクトをクライアントに返すようにします。  
  
 このチュートリアルでは、RDS は使用しません **。DataControl**ですが、次のようになります。  
  
```vb
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "https://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 また、このチュートリアルでは ADO オブジェクトを使用して RDS を呼び出しますが、次のようになります。  
  
```vb
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=https://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **パート B** この手順を実行する一般的な方法は、 **DataFactory** オブジェクト [クエリ](../../reference/rds-api/query-method-rds.md) メソッドを呼び出すことです。 このメソッドは、データソースへの接続に使用される接続文字列と、データソースから返される行を指定するために使用されるコマンドテキストを受け取ります。  
  
 このチュートリアルでは、 **DataFactory** object **クエリ** メソッドを使用します。  
  
```vb
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>参照  
 [手順 3: サーバーがレコードセットを取得する (RDS チュートリアル)](./step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [RDS のチュートリアル (VBScript)](./rds-tutorial-vbscript.md)