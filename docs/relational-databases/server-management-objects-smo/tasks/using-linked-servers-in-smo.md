---
description: SMO でのリンク サーバーの使用
title: SMO でのリンクサーバーの使用 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e71d4601c594062b0ab4a2ac26510c5354ee8362
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420236"
---
# <a name="using-linked-servers-in-smo"></a>SMO でのリンク サーバーの使用
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  リンク サーバーはリモート サーバー上の OLE DB データ ソースを表します。 リモート OLE DB データ ソースは、<xref:Microsoft.SqlServer.Management.Smo.LinkedServer> オブジェクトを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスにリンクされます。  
  
 リモートデータベースサーバーは、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] OLE DB プロバイダーを使用して、の現在のインスタンスにリンクすることができ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ます。 SMO では、リンク サーバーは <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> オブジェクトで表現されます。 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> プロパティは <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> オブジェクトのコレクションを参照します。 これらのオブジェクトには、リンク サーバーとの接続の確立に必要となるログオン資格情報が格納されます。  
  
## <a name="ole-db-providers"></a>OLE DB プロバイダー  
 SMO では、インストールされた OLE DB プロバイダーは <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> オブジェクトのコレクションで表されます。  
  
## <a name="example"></a>例  
 次のコード例では、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio .net で Visual C&#35; SMO プロジェクトを作成する](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>Visual C# での OLE DB プロバイダー サーバーへのリンクの作成  
 コード例では、<xref:Microsoft.SqlServer.Management.Smo.LinkedServer> オブジェクトを使用して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 異種データ ソースへのリンクを作成する方法を示しています。 製品名として [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を指定することで、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用の正式な OLE DB プロバイダーである [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client OLE DB プロバイダーを使用して、リンク サーバーのデータへのアクセスが行われます。  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
   Server srv = new Server();   
   //Create a linked server.   
   LinkedServer lsrv = default(LinkedServer);   
   lsrv = new LinkedServer(srv, "OLEDBSRV");   
   //When the product name is SQL Server the remaining properties are   
   //not required to be set.   
   lsrv.ProductName = "SQL Server";   
   lsrv.Create();   
}   
```  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-powershell"></a>PowerShell での OLE DB プロバイダー サーバーへのリンクの作成  
 コード例では、<xref:Microsoft.SqlServer.Management.Smo.LinkedServer> オブジェクトを使用して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 異種データ ソースへのリンクを作成する方法を示しています。 製品名として [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を指定することで、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用の正式な OLE DB プロバイダーである [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client OLE DB プロバイダーを使用して、リンク サーバーのデータへのアクセスが行われます。  
  
```powershell  
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -argumentlist $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.   
$lsvr.ProductName = "SQL Server"  
  
#Create the Database Object  
$lsvr.Create()   
```  
  
  
