---
description: SQL Server のインスタンスからの切断
title: SQL Server のインスタンスからの切断 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2e98180b877fb81c5d32f908a2f8e9cdc131a45a
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868609"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>SQL Server のインスタンスからの切断
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理オブジェクト (SMO) オブジェクトを手動で閉じたり切断する処理は必要ありません。 接続を開いたり閉じたりする操作は、必要に応じて行われます。  
  
## <a name="connection-pooling"></a>接続のプール  
 [Connect](/previous-versions/sql/sql-server-2014/ms199449(v=sql.120))メソッドを呼び出すと、接続は自動的には解放されません。 接続プールへの接続を解放するには、 [Disconnect](/previous-versions/sql/sql-server-2014/ms199428(v=sql.120)) メソッドを明示的に呼び出す必要があります。 また、プールされていない接続を要求することもできます。 これを行うには、 [NonPooledConnection](/previous-versions/sql/sql-server-2014/ms214357(v=sql.120)) <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> [serverconnection](/previous-versions/sql/sql-server-2014/ms218641(v=sql.120))オブジェクトを参照するプロパティの nonpooledconnection プロパティを設定します。  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>RMO の SQL Server のインスタンスからの切断  
 RMO を使ったプログラミングでサーバー接続を閉じる方法は、SMO とは若干異なります。  
  
 RMO オブジェクトのサーバー接続は [Serverconnection](/previous-versions/sql/sql-server-2014/ms218641(v=sql.120)) オブジェクトによって維持されるため、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] rmo を使用してプログラムを作成するときに、このオブジェクトはのインスタンスから切断するときにも使用されます。 [Serverconnection](/previous-versions/sql/sql-server-2014/ms218641(v=sql.120))オブジェクトを使用して接続を閉じるには、rmo オブジェクトの[Disconnect](/previous-versions/sql/sql-server-2014/ms199428(v=sql.120))メソッドを呼び出します。 接続が閉じられた後は、RMO オブジェクトを使用することはできません。  
  
## <a name="example"></a>例  
提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio .net で Visual C&#35; SMO プロジェクトを作成する](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
 
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>Visual Basic で SMO オブジェクトを閉じたり切断する処理を行う方法  
 このコード例では、オブジェクトプロパティの [Nonpooledconnection](/previous-versions/sql/sql-server-2014/ms214357(v=sql.120)) プロパティを設定して、プールされていない接続を要求する方法を示し <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> ます。  
  
```VBNET
Dim srv As Server
srv = New Server
'Disable automatic disconnection.
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect
'Connect to the local, default instance of SQL Server.
srv.ConnectionContext.Connect()
'The actual connection is made when a property is retrieved.
Console.WriteLine(srv.Information.Version)
'Disconnect explicitly.
srv.ConnectionContext.Disconnect()
```
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>Visual C# で SMO オブジェクトを閉じたり切断する処理を行う方法  
 このコード例では、オブジェクトプロパティの [Nonpooledconnection](/previous-versions/sql/sql-server-2014/ms214357(v=sql.120)) プロパティを設定して、プールされていない接続を要求する方法を示し <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> ます。  
  
```csharp  
{   
Server srv;   
srv = new Server();   
//Disable automatic disconnection.   
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect;   
//Connect to the local, default instance of SQL Server.   
srv.ConnectionContext.Connect();   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
//Disconnect explicitly.   
srv.ConnectionContext.Disconnect();  
}  
```  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 [Microsoft.sqlserver.management.common.serverconnection>](/previous-versions/sql/sql-server-2014/ms218641(v=sql.120))  
  
