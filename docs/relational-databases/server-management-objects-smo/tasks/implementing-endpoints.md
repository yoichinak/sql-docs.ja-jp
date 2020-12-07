---
description: エンドポイントの実装
title: エンドポイントの実装
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- endpoints [SMO]
ms.assetid: f8674dbb-9bc0-488f-9def-e9e0ce1ddf86
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9d5f21bf8c3bcf9ca189097fd9c51c02df123a84
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448083"
---
# <a name="implementing-endpoints"></a>エンドポイントの実装
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  エンドポイントは、要求をネイティブにリッスンできるサービスです。 SMO は、<xref:Microsoft.SqlServer.Management.Smo.Endpoint> オブジェクトを使用することで、さまざまな種類のエンドポイントをサポートしています。 <xref:Microsoft.SqlServer.Management.Smo.Endpoint> オブジェクトのインスタンスを作成し、そのプロパティを設定することで、特定のプロトコルを必要とする特定の種類のペイロードを処理するためのエンドポイント サービスを作成できます。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Endpoint.EndpointType%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Endpoint> プロパティを使用して、次の種類のペイロードの 1 つを指定することができます。  
  
-   データベース ミラーリング  
  
-   SOAP (SOAP エンドポイントは、 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] および以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でサポートされます)  
  
-   Service Broker  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)]  
  
 また、<xref:Microsoft.SqlServer.Management.Smo.Endpoint.ProtocolType%2A> プロパティを使用して、サポートされている次の 2 つのプロトコルを指定することができます。  
  
-   HTTP プロトコル  
  
-   TCP プロトコル  
  
 ペイロードの種類を指定すると、<xref:Microsoft.SqlServer.Management.Smo.Endpoint.Payload%2A> オブジェクト プロパティを使用して実際のペイロードを設定することができます。 <xref:Microsoft.SqlServer.Management.Smo.Payload> オブジェクト プロパティは、プロパティを変更できる、指定された種類のペイロード オブジェクトへの参照を提供します。  
  
 <xref:Microsoft.SqlServer.Management.Smo.DatabaseMirroringPayload> オブジェクトに対して、ミラーリング ロール、および暗号化が有効であるかどうかを指定する必要があります。 <xref:Microsoft.SqlServer.Management.Smo.ServiceBrokerPayload> オブジェクトには、メッセージ転送、許可される最大接続数、および認証モードに関する情報が必要です。 <xref:Microsoft.SqlServer.Management.Smo.SoapPayloadMethod.%23ctor%2A> オブジェクトでは、さまざまなプロパティの設定が必要です。これには、クライアントが使用できる SOAP ペイロード メソッド (ストアド プロシージャおよびユーザー定義関数) を指定する、<xref:Microsoft.SqlServer.Management.Smo.SoapPayloadMethodCollection.Add%2A> オブジェクト プロパティなどがあります。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Endpoint.Protocol%2A> オブジェクト プロパティを使用すると、<xref:Microsoft.SqlServer.Management.Smo.Endpoint.ProtocolType%2A> プロパティで指定された型のプロトコル オブジェクトを参照して、実際のプロトコルを設定することができます。 <xref:Microsoft.SqlServer.Management.Smo.HttpProtocol> オブジェクトには、制限された IP アドレス、ポート、Web サイト、および認証情報のリストが必要です。 また、<xref:Microsoft.SqlServer.Management.Smo.TcpProtocol> オブジェクトには、制限された IP アドレスおよびポート情報のリストも必要です。  
  
 エンドポイントを作成して定義を完了したら、データベース ユーザー、グループ、ロール、およびログオンに対して、アクセスの許可、取り消し、および拒否を行うことができます。  
  
## <a name="example"></a>例  
 次のコード例では、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio .net で Visual C&#35; SMO プロジェクトを作成する](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-visual-basic"></a>Visual Basic でのデータベース ミラーリング エンドポイント サービスの作成  
 コード例では、SMO でデータベース ミラーリング エンドポイントを作成する方法を示します。 これは、データベース ミラーを作成する前に必要な操作です。 <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Database> プロパティおよびその他のプロパティを使用して、データベース ミラーを作成します。  
  
```VBNET
'Set up a database mirroring endpoint on the server before setting up a database mirror.
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define an Endpoint object variable for database mirroring.
Dim ep As Endpoint
ep = New Endpoint(srv, "Mirroring_Endpoint")
ep.ProtocolType = ProtocolType.Tcp
ep.EndpointType = EndpointType.DatabaseMirroring
'Specify the protocol ports.
ep.Protocol.Http.SslPort = 5024
ep.Protocol.Tcp.ListenerPort = 6666
'Specify the role of the payload.
ep.Payload.DatabaseMirroring.ServerMirroringRole = ServerMirroringRole.All
'Create the endpoint on the instance of SQL Server.
ep.Create()
'Start the endpoint.
ep.Start()
Console.WriteLine(ep.EndpointState)
``` 
  
## <a name="creating-a-database-mirroring-endpoint-service-in-visual-c"></a>Visual C# でのデータベース ミラーリング エンドポイント サービスの作成  
 コード例では、SMO でデータベース ミラーリング エンドポイントを作成する方法を示します。 これは、データベース ミラーを作成する前に必要な操作です。 <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Database> プロパティおよびその他のプロパティを使用して、データベース ミラーを作成します。  
  
```csharp  
{  
            //Set up a database mirroring endpoint on the server before   
        //setting up a database mirror.   
        //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Define an Endpoint object variable for database mirroring.   
            Endpoint ep = default(Endpoint);  
            ep = new Endpoint(srv, "Mirroring_Endpoint");  
            ep.ProtocolType = ProtocolType.Tcp;  
            ep.EndpointType = EndpointType.DatabaseMirroring;  
            //Specify the protocol ports.   
            ep.Protocol.Http.SslPort = 5024;  
            ep.Protocol.Tcp.ListenerPort = 6666;  
            //Specify the role of the payload.   
            ep.Payload.DatabaseMirroring.ServerMirroringRole = ServerMirroringRole.All;  
            //Create the endpoint on the instance of SQL Server.   
            ep.Create();  
            //Start the endpoint.   
            ep.Start();  
            Console.WriteLine(ep.EndpointState);  
        }  
```  
  
## <a name="creating-a-database-mirroring-endpoint-service-in-powershell"></a>PowerShell でのデータベース ミラーリング エンドポイント サービスの作成  
 コード例では、SMO でデータベース ミラーリング エンドポイントを作成する方法を示します。 これは、データベース ミラーを作成する前に必要な操作です。 <xref:Microsoft.SqlServer.Management.Smo.Database.IsMirroringEnabled%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Database> プロパティおよびその他のプロパティを使用して、データベース ミラーを作成します。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Get a new endpoint to congure and add  
$ep = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Endpoint -argumentlist $srv,"Mirroring_Endpoint"  
  
#Set some properties  
$ep.ProtocolType = [Microsoft.SqlServer.Management.SMO.ProtocolType]::Tcp  
$ep.EndpointType = [Microsoft.SqlServer.Management.SMO.EndpointType]::DatabaseMirroring  
$ep.Protocol.Http.SslPort = 5024  
$ep.Protocol.Tcp.ListenerPort = 6666 #inline comment  
$ep.Payload.DatabaseMirroring.ServerMirroringRole = [Microsoft.SqlServer.Management.SMO.ServerMirroringRole]::All  
  
# Create the endpoint on the instance  
$ep.Create()  
  
# Start the endpoint  
$ep.Start()  
  
# Report its state  
$ep.EndpointState;  
```  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
