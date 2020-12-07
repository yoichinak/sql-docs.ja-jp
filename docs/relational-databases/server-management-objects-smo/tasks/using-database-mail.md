---
description: データベース メールの使用
title: データベースメール | を使用するMicrosoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- e-mail [SMO]
- Database Mail [SMO]
- mail [SMO]
ms.assetid: 7605390f-b485-48cc-8d97-e364a066067b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 43a49f3ec79b75aeef6fe4282a2933616af723ae
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420176"
---
# <a name="using-database-mail"></a>データベース メールの使用
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  SMO では、<xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> プロパティによって参照される <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> オブジェクトで、データベース メール サブシステムを表現します。 SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトを使用すると、データベース メール サブシステムを構成して、プロファイルおよびメール アカウントを管理することができます。 SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトは **サーバー** オブジェクトに属しています。つまり、メールアカウントのスコープがサーバーレベルであることを意味します。  
  
## <a name="examples"></a>例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio .net で Visual C&#35; SMO プロジェクトを作成する](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
 データベースメールを使用するプログラムでは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 、Mail 名前空間を修飾する **Imports** ステートメントを含める必要があります。 アプリケーションの宣言の前、かつ他の **Imports** ステートメントの後に、次のようにステートメントを挿入します。  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Mail`  
  
## <a name="creating-a-database-mail-account-by-using-visual-basic"></a>Visual Basic によるデータベース メール アカウントの作成  
 このコード例では、SMO で電子メール アカウントを作成する方法を示します。 データベース メールは <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトで表現され、<xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Server> プロパティによって参照されます。 SMO は、プログラムでデータベース メールを構成するために使用することはできますが、電子メールを送信したり、受信した電子メールを処理したりするために使用することはできません。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server()
'Define the Database Mail service with a SqlMail object variable and reference it using the Server Mail property.
Dim sm As SqlMail
sm = srv.Mail
'Define and create a mail account by supplying the Database Mail service, name, description, display name, and email address arguments in the constructor.
Dim a As MailAccount
a = New MailAccount(sm, "AdventureWorks Administrator", "AdventureWorks Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com")
a.Create()
```
  
## <a name="creating-a-database-mail-account-by-using-visual-c"></a>Visual C# によるデータベース メール アカウントの作成  
 このコード例では、SMO で電子メール アカウントを作成する方法を示します。 データベース メールは <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトで表現され、<xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Server> プロパティによって参照されます。 SMO は、プログラムでデータベース メールを構成するために使用することはできますが、電子メールを送信したり、受信した電子メールを処理したりするために使用することはできません。  
  
```csharp  
{  
         //Connect to the local, default instance of SQL Server.  
         Server srv = default(Server);   
           srv = new Server();   
           //Define the Database Mail service with a SqlMail object variable   
           //and reference it using the Server Mail property.   
           SqlMail sm;   
           sm = srv.Mail;   
           //Define and create a mail account by supplying the Database Mail  
           //service, name, description, display name, and email address  
           //arguments in the constructor.   
           MailAccount a = default(MailAccount);   
           a = new MailAccount(sm, "AdventureWorks2012 Administrator", "AdventureWorks2012 Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com");   
           a.Create();    
}  
```  
  
## <a name="creating-a-database-mail-account-by-using-powershell"></a>PowerShell によるデータベース メール アカウントの作成  
 このコード例では、SMO で電子メール アカウントを作成する方法を示します。 データベース メールは <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトで表現され、<xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Server> プロパティによって参照されます。 SMO は、プログラムでデータベース メールを構成するために使用することはできますが、電子メールを送信したり、受信した電子メールを処理したりするために使用することはできません。  
  
  
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define the Database Mail; reference it using the Server Mail property.  
$sm = $srv.Mail  
  
#Define and create a mail account by supplying the Database Mail service,  
#name, description, display name, and email address arguments in the constructor.  
$a = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Mail.MailAccount -argumentlist $sm, `  
"Adventure Works Administrator", "Adventure Works Automated Mailer",`  
 "Mail account for administrative e-mail.", "dba@Adventure-Works.com"  
$a.Create()  
```  
  
  
